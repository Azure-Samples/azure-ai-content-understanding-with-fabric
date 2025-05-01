# Content Understanding Fabric Template Pipeline Tutorial

This tutorial will show you how to use a Fabric Pipeline template to process your document, video, image, or audio content with Azure AI Content Understanding and save your results in a Fabric LakeHouse.

## Prerequisites

- **An Active Azure Subscription**: If you don’t have one, you can [create one for free](https://azure.microsoft.com/en-us/free/).
- [**An Azure AI Services Resource**](https://portal.azure.com/#create/Microsoft.CognitiveServicesAIServices): Ensure that your resource is in one of these regions where Content Understanding is available: West US 2, Sweden Central, and Australia East. Learn more on how to create an Azure AI Services Resource [here](https://review.learn.microsoft.com/en-us/azure/ai-services/content-understanding/how-to/create-multi-service-resource?branch=main). 
- [**An Azure Blob Storage Account**](https://portal.azure.com/#create/Microsoft.StorageAccount-ARM): This is where you will store your input files and JSON outputs from content understanding before you write them to Fabric Lakehouse. [Create two containers](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal#create-a-container) in your Blob Storage account for inputs and results:
  - **Source container**: This container is where you upload input files.
  - **Outputs container**: This container is where results from the Content Understanding API will be stored.
- [**A Microsoft Fabric Account**](https://www.microsoft.com/en-us/microsoft-fabric/getting-started?msockid=1f49fc914c6d66271d89ec164dde676e)

## How to Use the Template

### Create a Lakehouse Item to Store Structured Outputs

1. Go to your preferred Fabric Workspace and click on “New item” in the top left corner. Then look for “LakeHouse”. Name your Lakehouse item and create it.
2. Go to the LakeHouse item and create a new subfolder under Files. This is the directory where your JSON outputs from Content Understanding will be stored.

### Import and Configure the Content Understanding Field Extraction Notebook

1. Download the Notebook from GitHub onto your computer. Go to your Fabric Workspace and click on “Import” near the top left and select Notebook.
2. Open the Notebook once it is imported. Inside the Notebook, follow instructions to enter your credentials:
   - Azure AI Services Resource Endpoint
   - Azure AI Services Resource Key
   - Azure Blob Storage Account Name
   - Azure Blob Storage Account SAS Token
   - Azure Blob Storage Container for Inputs
   - Azure Blob Storage Container for Outputs
3. Run each cell and check the output to ensure that the Notebook is running correctly before proceeding to the next steps below.

### Import the Pipeline Template

1. Download the Pipeline Template zip file from GitHub.
2. Go to your Fabric Workspace and click on “New Item” in the top left corner. Then look for the “Data pipeline” item before clicking on it to create a new pipeline.
3. Once the pipeline is created, click on the Import arrow near the top left corner which will prompt you to select the template zip file. Select the downloaded zip file then click on “Use this template” button.

### Configure Pipeline Activities

#### Select Notebook

1. Click on the Notebook Activity. Under Settings, click on the Notebook dropdown and ensure that the Field Extraction Template Notebook is selected.

#### Connect Azure Blobs as Copy Data Source

1. Click on the Copy data activity and go to the source tab. Under connection, click on the dropdown then select more. Search for blobs when prompted to choose a data source.
2. Click on Azure Blobs and connect your Azure Blob Storage Account by entering your storage account name and Shared Access Signature (SAS). This should be the same Blob Storage account that was used in the Notebook above. You can learn more about setting up an Azure Blob Storage connection in Fabric [here](https://learn.microsoft.com/en-us/azure/storage/blobs/).

3. Once your Blob Storage connection is created and added to the Copy data activity, select “Wildcard file path” in file path type and in "Container", enter the name of the Blob Storage outputs Container where your Content Understanding results are stored. In File format, ensure that “JSON” is selected from the dropdown.

#### Connect LakeHouse as Copy Data Destination

1. Click on the Destination tab of the Copy data activity. In connection, click on the dropdown and filter by searching for the LakeHouse item you created earlier.
2. When your LakeHouse item is selected, click on Files for Root folder and enter the target LakeHouse directory before selecting “JSON” as the File format.

### Run the Pipeline

1. Now that the activities are configured, click on “Run” to run the pipeline.
2. Upon success, verify that your LakeHouse now contains JSON result files from Content Understanding.
3. In case of failure, check the pipeline output for error messages, copy the error message and investigate with copilot to find a solution or reach out to us directly.

## Next Steps: Put Your Data to Work

With your structured outputs from Azure Content Understanding now available in a Fabric LakeHouse, you can:

- **Visualize**: Build dashboards in Power BI from extracted insights.
- **Query**: Use SQL to filter, join, or summarize results.
- **Automate**: Trigger workflows based on keywords or metadata.
- **Enrich**: Add tags or categories to files for easy search.
- **Train**: Feed data into AI or ML models.
