# Install postgreSQL in IBM Cloud

'PostgreSQL is a powerful, open source object-relational database system that uses and extends the SQL language'. It would be a great idea to have this database system in your IBM Cloud. This documentation will guide you on how to install postgreSQL on the IBM Cloud using the Kubernetes Service. Simple and effective.

## Pre-requisites

You must have an account created in IBM Cloud. The account needs to be either be *Pay-As-You-Go* or *Subscription*. Click [here](https://cloud.ibm.com/docs/account?topic=account-accounts "here") to read more.
If you have a Lite account, you can upgrade it. Click [here](https://cloud.ibm.com/docs/account?topic=account-account-getting-started#account-gs-upgrade "here") to learn how to upgrade.

## Step 1: Provision Kubernetes Cluster

* Click on the search section at the top of the main page, type Kubernetes, and then choose Kubernetes Service.

![](Kubernetes1.PNG)

* In the new window, select between the free and standard type under "Pricing plan". Once selected, click on create.

![Screenshot](KubernetesPaid1.PNG)

We'll choose the Standard Plan for this documentation as the Free Plan may fall short of resources when deploying your pods. We highly recommend using a Standard Plan with the hardware that suits you the best. If you're selecting the Standard Plan, please make sure you select the adequate requirements,

* Select your Kubernetes Version to be the latest available or the required one by your application. In this example, we have set it to be '1.18.13'.
* Select Infrastructure as 'Classic'.
* Leave Resource Group to 'Default'.
* Select Geography to the one that suits you better or that fits your infrastructure.
* Select Availability to be 'Single Zone' or 'Multi Zone' depending on your needs.
* Select a Worker Zone that suits you better or that fits your infrastructure.

![Screenshot](KubernetesPaid2.PNG)

* Select the number of workers in Worker Pool.
* Give your Worker Pool a name.
* Leave the Encrypt Local Disk option 'On'
* Choose 'Both private and public endpoints' on Master Service Endpoint

![Screenshot](KubernetesPaid4.PNG)

* Give your cluster a name in 'cluster-name'
* Provide the tags to your cluster and click on Create.

![Screenshot](KubernetesPaid5.PNG)

Wait a few minutes while your cluster is deployed.

![Screenshot](KubernetesPaid3.PNG)

The following checkmark and the word 'normal' will appear once the Kubernetes Cluster is deployed. You can check it under your cluster section which is located in your *Resources List*.

![Screenshot](KubernetesPaid6.PNG)


## Step 2:  Deploy IBM Cloud Block Storage plug-in

* Click on the search section at the top of the main page, select IBM Cloud Block Storage, and click on it.

![Screenshot](StoragePaid1.PNG)

* A new window opens, select the cluster and enter the name you want for this workspace, in this case, it will be called _storage-example_, accept the terms, click *Install* and wait a few minutes.

![Screenshot](StoragePaid2.PNG)


## Step 3: Install postgreSQL

* Click on the search section at the top of the main page, type postgreSQL, and click on it.

![Screenshot](post1.PNG)

* A new window opens, select the cluster and enter the name you want for the PostgreSQL workspace; in this case, it will be called _postgresql-example_; then, go to the bottom to find the workspace parameters.

You can modify the different installation parameters at the bottom. We will leave them by default except for the user password, which you will need to access your PostgreSQL console and work with your databases. You can read more about setting up the parameters [here](https://cloud.ibm.com/catalog/content/postgresql "here").

Make sure you set up a password in the _postgresqlPostgresPassword_ variable. 

![Screenshot](post4.PNG)

You can create an additional non-admin user if you edit the _postgresqlUsername_ variable. The admin user will continue to be 'Postgres.' 

![Screenshot](post3.PNG)

When you're done, accept the terms, and click on *Install*.

![Screenshot](post2.PNG)


## Step 4: Verify Installation

* Go to *Resources List* in the Left Navigation Menu and click on *Kubernetes*.

![Screenshot](test1.png)

* Click the *Actions* button and select *Web terminal*.

![Screenshot](test2.PNG)

* A window opens to install the web terminal, click on install and wait a few minutes. The window will pop up at the buttom If the web terminal is already installed.

![Screenshot](test3.PNG)

![Screenshot](test7.PNG)

* Once you have installed the terminal, open it and type the following command. It will show you the workspaces of your cluster. You can see *postgresql-example* is now active.

`$ kubectl get ns`

![Screenshot](textpost1.PNG)

* You can then obtain more data about the service and it's pods.

`$ kubectl get pod -n NAMESERVICE -o wide`

![Screenshot](textpost2.PNG)

* Find the port the main pod is using, you will need it to start using PostgreSQL.

`$ kubectl get service -n NAME SERVICE`

![Screenshot](textpost3.PNG)

* Select the pod within your service using bash so you can start using PostgreSQL from the terminal.

`$ kubectl exec --stdin --tty PODNAME -n NAMESPACE -- /bin/bash`

![Screenshot](textpost4.PNG)

* Once you're inside the pod terminal, you can execute the following command to login into PostgreSQL and create and manage your databases. Use your previously created password.

`$ psql -h localhost -U postgres --password -p 5432`

![Screenshot](textpost5.PNG)

You have finished the installation, enjoy your PostgreSQL installation!
