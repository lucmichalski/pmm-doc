#########
PMM DBaaS
#########

This page is where you view, add, and delete Kubernetes and Database clusters.

To access it, select *PMM > PMM DBaaS*.

.. image:: /_images/PMM_DBaaS_Kubernetes_Cluster_Panel.jpg

************************
Add a Kubernetes cluster
************************

1. Select the *Kubernetes Cluster* tab.

2. Click *Add new Kubernetes Cluster*

3. Enter values for the *Kubernetes Cluster Name* and *Kubeconfig file* in the relevant fields.

   .. image:: /_images/PMM_DBaaS_Kubernetes_Cluster_Details.jpg

4. Click *Add*.

***************************
Delete a Kubernetes cluster
***************************

1. Identify the cluster to be deleted and click *Delete*.

2. Confirm the action by clicking *Proceed*, or abandon by clicking *Cancel*.

   .. image:: /_images/PMM_DBaaS_Kubernetes_Cluster_Delete.jpg

**********************
Add a Database Cluster
**********************

1. Add at least one Kubernetes cluster.

2. Select the *DB Cluster* tab.

3. Click *Create DB Cluster*

4. Enter a value for *Cluster Name*. The name must:

   - consist of lower case alphanumeric characters;
   - start and end with a lowercase alphanumeric character.

   It may contain the characters ``-`` (dash) and ``.`` (period).

5. Click and select an item from the *Kubernetes Cluster* menu.

6. Click and select an item from the *Database Type* menu.

   .. note::

      MySQL is currently the only supported option.

7. Click *Create Cluster*.
