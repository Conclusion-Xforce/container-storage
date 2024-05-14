# Snapshots

## Step 1 - Create Deployment & Persistent Volume Claim

Deploy the `./persistentvoluleclaim.yaml` en `./deployment.yaml`

## Step 2 - Fill mysql database with data

* Start a shell in the pod
` oc rsh <pod name>`

* Login to mysql
`mysql -h 127.0.0.1 -ptest -u root`

* Fill the database with data
```
CREATE DATABASE prod;
USE prod
CREATE TABLE persons(PersonID int, LastName varchar(255), FirstName varchar(255), Address varchar(255), City varchar(255));
INSERT INTO persons(PersonID, FirstName, Lastname, Address, City) VALUES('1', 'Seven', 'Koimen', 'edison 30', 'nieuwegein');
INSERT INTO persons(PersonID, FirstName, Lastname, Address, City) VALUES('1', 'Willem', 'Pens', 'New Even 30', 'rotterdam');
```

* Test if the database is fill with data
` SELECT * FROM persons; `

## Step 3 - Create a volume snapshot

Create a VolumeSnapshot and wait until is has the status `Ready`

## Step 4 - Delete PVC and Deployment

Delete both the PVC and the deployment

## Step 5 -  Restore PVC

Restore the VolumeSnapshot as new PVC

## Step 6 - Redeploy Deployment

Redeploy the deployment at `./deployment.yaml`. Change the persistent volume name if necessary.

## Step 7 - Check if data is back

* Start a shell in the pod
` oc rsh <pod name>`

* Login to mysql
`mysql -h 127.0.0.1 -ptest -u root`

* Test if the database is fill with data
` SELECT * FROM persons; `

