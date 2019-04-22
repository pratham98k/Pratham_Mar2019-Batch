#Dynamically create and use a persistent volume with Azure disks in Azure Kubernetes Service (AKS)

A persistent volume represents a piece of storage that has been provisioned for use with Kubernetes pods. A persistent volume can be used by one or many pods, and can be dynamically or statically provisioned.

#Built in storage classes

Each AKS cluster includes two pre-created storage classes, both configured to work with Azure disks:

The default storage class provisions a standard Azure disk.
Standard storage is backed by HDDs, and delivers cost-effective storage while still being performant. Standard disks are ideal for a cost effective dev and test workload.

The managed-premium storage class provisions a premium Azure disk.
Premium disks are backed by SSD-based high-performance, low-latency disk. Perfect for VMs running production workload. If the AKS nodes in your cluster use premium storage, select the managed-premium class.

'''
$ kubectl get sc

NAME                PROVISIONER                AGE
default (default)   kubernetes.io/azure-disk   1h
managed-premium     kubernetes.io/azure-disk   1h

'''

#Create a persistent volume claim

A persistent volume claim (PVC) is used to automatically provision storage based on a storage class. In this case, a PVC can use one of the pre-created storage classes to create a standard or premium Azure managed disk.

use azure-premium.yaml


'''
piVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azure-managed-disk
  spec:
    accessModes:
      - ReadWriteOnce
        storageClassName: managed-premium
	  resources:
	      requests:
	            storage: 5Gi
		 '''

#Use the persistent volume

Once the persistent volume claim has been created and the disk successfully provisioned, a pod can be created with access to the disk. The following manifest creates a basic NGINX pod that uses the persistent volume claim named azure-managed-disk to mount the Azure disk at the path /mnt/azure.

Create a file named azure-pvc-disk.yaml, and copy in the following manifest.

'''
kind: Pod
apiVersion: v1
metadata:
  name: mypod
  spec:
    containers:
      - name: mypod
          image: nginx:1.15.5
	      resources:
	            requests:
		            cpu: 100m
			            memory: 128Mi
				          limits:
					          cpu: 250m
						          memory: 256Mi
							      volumeMounts:
							          - mountPath: "/mnt/azure"
								        name: volume
									  volumes:
									      - name: volume
									            persistentVolumeClaim:
										            claimName: azure-managed-disk
											    '''
