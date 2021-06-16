![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/main/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Machine Learning
</div>

<div class="MCWHeader2">
Before the hands-on lab setup guide
</div>

<div class="MCWHeader3">
February 2021
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

&copy; 2021 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Machine Learning before the hands-on lab setup guide](#machine-learning-before-the-hands-on-lab-setup-guide)
  - [Requirements](#requirements)
  - [Before the hands-on lab](#before-the-hands-on-lab)
    - [Task 1: Create your Azure Databricks Account](#task-1-create-your-azure-databricks-account)
    - [Task 2: Create an Azure Databricks cluster](#task-2-create-an-azure-databricks-cluster)
    - [Task 3: Install libraries on the Azure Databricks Cluster](#task-3-install-libraries-on-the-azure-databricks-cluster)
    - [Task 4: Upload the Databricks notebook archive](#task-4-upload-the-databricks-notebook-archive)
    - [Task 5: Create your Azure Machine Learning Workspace](#task-5-create-your-azure-machine-learning-workspace)

<!-- /TOC -->

# Machine Learning before the hands-on lab setup guide

## Requirements

1. Microsoft Azure subscription must be pay-as-you-go or MSDN

    - Trial subscriptions will not work. You will run into issues with Azure resource quota limits.

    - Subscriptions with access limited to a single resource group will not work. You will need the ability to deploy multiple resource groups.

## Before the hands-on lab

Duration: 30 minutes

### Task 1: Create your Azure Databricks Account

Azure Databricks is an Apache Spark-based analytics platform optimized for Azure that supports data engineering and machine learning and deep learning workloads.

1. In the [Azure Portal](https://portal.azure.com), select **+ Create a resource**, then type "Azure Databricks <inject key="DeploymentID" />" into the search bar. Select Azure Databricks from the results.

    ![Azure Databricks is entered into the search field. Azure Databricks is selected from the search results list type-ahead suggestion.](images/create-azure-databricks-resource-01.png 'Create a resource')

2. Select **Create**.

    ![On the Azure Databricks resource overview page, the Create button is highlighted.](image/../images/create-azure-databricks-resource-02.png 'Create an Azure Databricks workspace')

3. Set the following configuration on the Azure Databricks Service creation form:

    - **Workspace name**: Enter a unique name, this will be indicated by a green check mark.

    - **Subscription**: Select the subscription you are using for this hands-on lab.

    - **Resource Group**: Select **Create new** and provide the name `MCW-Machine-Learning`.

    - **Location**: Select a region close to you. ***(If you are using an Azure Pass, select South Central US.)***

    - **Pricing**: Select **Premium (+ Role-based access controls)**.

    ![The Azure Databricks Service creation form is populated with the values outlined above.](images/azure-databricks-create-blade.png 'Azure Databricks Service Creation Dialog')

4. Select **Review + Create** and then select **Create** when the form values passes validation.

### Task 2: Create an Azure Databricks cluster

You have provisioned an Azure Databricks workspace, and now you need to create a new cluster within the workspace.

1. From within Azure portal navigate to your resource group name (e.g., `MCW-Machine-Learning`).

2. Next, select your Azure Databricks service from the list.

    ![The Azure Databricks service is selected from your lab resource group.](images/select-azure-databricks-service.png 'Azure Databricks Service')

3. In the Overview pane of the Azure Databricks service, select **Launch Workspace**.

    ![The Launch Workspace button is highlighted in the Azure Databricks service overview pane.](images/azure-databricks-launch-workspace.png 'Launch Workspace')

    Azure Databricks will automatically log you in using Azure Active Directory Single Sign On.

    ![Azure Databricks Azure Active Directory Single Sign On dialog.](images/azure-databricks-aad.png 'Sign In to Databricks')

4. Select **Clusters** (1) from the menu, then select **Create Cluster** (2).

    ![Clusters is selected from the left menu and the Create Cluster button is highlighted on the Clusters screen.](images/azure-databricks-create-cluster-button.png 'Create Cluster')

5. On the Create New Cluster form, provide the following:

    - **Cluster Name**: `lab`

    - **Cluster Mode**: **Standard**

    - **Databricks Runtime Version**: **Runtime: 7.3 LTS (Scala 2.12, Spark 3.0.1)**

    - **Enable autoscaling**: **Uncheck** this option.

    - **Terminate after ___ minutes of inactivity**: Leave **checked** and in the text box enter `120`.

    - **Worker Type**: **Standard_DS3_v2**

    - **Workers**: `1`

    - **Driver Type**: **Same as worker**

   ![The New Cluster form is populated with the values outlined above.](images/azure-databricks-create-cluster-form.png 'Create New Cluster Dialog')

6. Select **Create Cluster**. It will take few minutes to create the cluster. Please ensure that the cluster state is running before proceeding further.

### Task 3: Install libraries on the Azure Databricks Cluster

The notebooks you will run depends on certain Python libraries that will need to be installed in your cluster. The following steps walk you through adding these dependencies.

1. From the left-hand menu in your Workspace, select **Clusters**.

    ![The Clusters menu option is selected from the left menu.](images/azure-databricks-clusters.png "Clusters")

2. In the list of clusters, select your cluster. Make sure the state of the cluster is `Running`.

    ![The list of Interactive Clusters is shown with the lab cluster highlighted having a state of Running.](images/azure-databricks-clusters-list.png "Interactive Clusters")

3. Select the **Libraries** link and then select **Install New**.

    ![In the lab cluster, the Libraries tab is selected and the Install New button is highlighted.](images/azure-databricks-cluster-libraries.png "Install New")

4. In the Library Source, select **PyPi** and in the Package text box type `azureml-sdk[databricks]` and select **Install**.

    ![The Install Library dialog showing the PyPi item selected as the source and the azureml-sdk value entered in the package textbox.](images/azure-databricks-install-library.png "Install Library")

5. An entry for azureml-sdk will appear in the list. The install will progress first with a status of installing followed by the status of installed.

### Task 4: Upload the Databricks notebook archive

1. Select the link below to download the `Databricks notebook archive` file to your local computer:

   [AI with Databricks and AML.dbc](https://github.com/microsoft/MCW-Machine-Learning/blob/master/Hands-on%20lab/notebooks/AI%20with%20Databricks%20and%20AML.dbc?raw=true)

2. Within the Azure Databricks Workspace, using the command bar on the left, select **Workspace**, **Users** and select your username (the entry with house icon).

3. In the blade that appears, select the downwards pointing chevron next to your name, and select **Import**.

    ![The Import menu item can be accessed by selecting your username from the list of users in the workspace.](images/azure-databricks-import-menu.png "Import Menu")

4. On the Import Notebooks dialog, browse and open the `AI with Databricks and AML.dbc` file from your local computer and then select **Import**.

    ![Obtaining a zip archive of the repository to access the notebook for upload into the Databricks workspace.](images/download-zip-repository-2.png "Obtaining a local copy of the repository")

5. A folder named after the archive should appear. Select that folder.

6. The folder will contain one or more notebooks. These are the notebooks you will use in completing this lab.

### Task 5: Create your Azure Machine Learning Workspace

1. In the [Azure Portal](https://portal.azure.com), select **+ Create a resource**, then type `Machine Learning` into the search bar.

    ![Machine Learning is entered into the search field.](images/create-aml-resource-01.png 'Create a resource')

2. Select **Create**.

    ![The Create button is selected on the Machine Learning resource page.](images/create-aml-resource-02.png 'Create an Azure Machine Learning workspace')

3. In the Create Machine Learning Workspace dialog that appears, provide the following values:

    - **Subscription**: Choose your Azure subscription.

    - **Resource group**: Select the resource group in which you deployed your Azure Databricks workspace.

    - **Workspace Name**: `mcwmachinelearning`

    - **Region**: Choose a region closest to you (it is OK if the Azure Databricks Workspace and the Azure Machine Learning Workspace are in different locations).

    ![The Machine Learning Create form is populated with the values outlined above. The Review + Create button is highlighted at the bottom of the form.](images/create-aml-workspace.png 'Azure Machine Learning Workspace Creation Dialog')

4. Select **Review + Create** and then select **Create** when the form values passes validation.

You should follow all these steps provided _before_ attending the Hands-on lab.
