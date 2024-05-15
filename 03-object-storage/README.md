# Object Storage

## Step 1 - Create Object Bucket Claim

Create an object bucket claim for your application.
The creation of the object bucket claim will automatically generate a Configmap and Secret in your namespace with the required information.

## Step 2 - Deploy the application for 01-recap-and-pvcs
Redeploy (or reuse) the application for 01.
Add the snippet below so the container trusts the certificate on the bucket endpoint

```
env:
- name: AWS_CA_BUNDLE
  value: /run/secrets/kubernetes.io/serviceaccount/service-ca.crt
```

## Step 3 - Adjust the deployment to use object storage instead of block storage
* Remove the volume mount and volume from your deployment
* Expose the key value pairs in the configmap and secret of the object bucket claim as environment variables in the photo-album deployment. The application will automatically read these variables and use them as the storage backend.

Use `envFrom`

## Step 4 - Test App
* If configured correctly the page should now display `Serving files from S3 storage.`
* Go to the URL of the photo-album app and upload a picture
* Restart the pod to see if the picture was written to object storage

## Step 5 - Interact with Object Storage manually
* Deploy the pod in `./awscli.yaml` 
* Use the remote shell of the pod `oc rsh <PODNAME>`
* Use the command `aws s3 ls --endpoint-url http://${BUCKET_HOST}` to check if the bucket exists
* Use the command ` aws s3 ls --endpoint-url http://${BUCKET_HOST} s3://<INSERT BUCKET NAME>` to check your file.
* You can play some more if you want.

## Resources

* [Expose Config Map as environment variable | Kubernetes Docs](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#configure-all-key-value-pairs-in-a-configmap-as-container-environment-variables)
* [Expose Secret as environment variable | Kubernetes Docs](https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#configure-all-key-value-pairs-in-a-secret-as-container-environment-variables)
