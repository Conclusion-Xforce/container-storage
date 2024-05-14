# Recap and Persistent Volume Claims

## Step 1 - Create Application Deployment
Create a deployment, service and route resource for the photo-album app. For this step you do not need to configure persistent storage:
Image: `quay.io/redhattraining/image-tool:latest`
Port: `5000`
Port vanuit buiten: `443`

## Step 2 - Use the App
Go to the URL, check if the application is working and upload a photo.
Delete the pod and refresh the URL. Is the photo still there?

## Step 3 - Create a persistent storage
Create a persistent volume claim and let the pod mount the volume.
mountPath: `/var/storage/`
Size: `5GB`

## Step 4 - Redo step 2
Redo the steps in Step 2. Is the photo still there this time?

## Resources

* [Persistent Volume references | Kubernetes Docs](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
* [ Deployment | Kubernetes Docs](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
