# Lab 01: Use your own data with Azure OpenAI

### Estimated Duration: 45 minutes

## Lab scenario
The Azure OpenAI Service enables you to use your own data with the intelligence of the underlying LLM. You can limit the model to only use your data for pertinent topics, or blend it with results from the pre-trained model.

## Lab objectives
In this lab, you will complete the following tasks:

- Task 1: Provision an Azure OpenAI resource
- Task 2: Deploy a model
- Task 3: Observe normal chat behavior without adding your own data
- Task 4: Connect your data in the chat playground
- Task 5: Chat with a model grounded in your data
- Task 6: Set up an application in Cloud Shell
- Task 7: Configure your application
- Task 8: Run your application

### Task 1: Provision an Azure OpenAI resource

Before you can use Azure OpenAI models, you must provision an Azure OpenAI resource in your Azure subscription.

1. In the **Azure portal**, search for **Azure OpenAI (1)** and select **Azure OpenAI (2)**.

   ![](../media/search.png)

2. On **Azure OpenAI services | Azure OpenAI (1)** blade, click on **Create (2)**.

   ![](../media/openai_create.png)

3. Create an **Azure OpenAI** resource with the following settings and then click on **Next (6)** thrice.
   
    - Subscription: **Default - Pre-assigned subscription (1)**.
    - Resource group: **openai-<inject key="DeploymentID" enableCopy="false"></inject> (2)**
    - Region: Select **East US 2 (3)**
    - Name: **OpenAI-Lab06-<inject key="DeploymentID" enableCopy="false"></inject> (4)**
    - Pricing tier: **Standard S0 (5)**
  
      ![](../media/u1.png "Create Azure OpenAI resource")
    
4. Click on **Create**.

5. Wait for deployment to complete. Then click on **Go to resource group**.

   ![](../media/u2.png)

6. To capture the Keys and Endpoints values, on **OpenAI-Lab06-<inject key="DeploymentID" enableCopy="false"></inject>** blade:
   
      - Select **Keys and Endpoint (1)** under **Resource Management**.
      - Click on **Show Keys (2)**.
      - Copy **Key 1 (3)** and ensure to paste it in a text editor such as notepad for future reference.
      - Finally copy the **Endpoint (4)** API URL by clicking on copy to clipboard. Paste it in a text editor such as notepad for later use.

      ![](../media/u4.png "Keys and Endpoints")


   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:    
   - If you receive a success message, you can proceed to the next task.
   - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

   <validation step="8b72507c-7e1f-49a4-b1a7-68ce5f2e3aee" />

### Task 2: Deploy a model

To chat with the Azure OpenAI, you must first deploy a model to use through the **Azure AI Foundry portal**. Once deployed, we will use the model with the playground and use our data to ground its responses.

1. In the **Azure portal**, search for **Azure OpenAI (1)** and select **Azure OpenAI (2)**.

      ![](../media/search.png)

2. On **Azure AI Services | Azure OpenAI (1)** blade, select **OpenAI-Lab06-<inject key="DeploymentID" enableCopy="false"></inject> (2)**.

      ![](../media/openai.png)

3. In the Azure OpenAI resource pane, **Overview (1)** section, click on **Go to Azure AI Foundry portal (2)** it will navigate to **Azure AI Foundry portal**.

      ![](../media/update08.png)

4. After navigating to Azure AI Foundry portal, click on **Close** pop-up on the top.

5. Click on **Deployments (1)** from the left navigation pane, click on **+ Deploy model** , select **Deploy base Model (2)**.  

   ![](../media/ui1.png)

6. In the **Select a model** window, select **gpt-35-turbo (1)** and click on **Confirm (2)**.

   ![](../media/mew5.png)

7. Within the **Deploy model** pop-up interface, enter the following details:
    
    - **Deployment name**: **text-turbo (1)**
    - **Deployment type**: **Standard (2)**
    - **Model version**: **0125 (3)** ( Check the Deployement name after changing the model version, if it is changed please update it to **text-turbo**)
    - Click on customize to reduce **Tokens per Minute Rate Limit (thousands)**: **10K (4)**
    - Click on **Deploy (5)**
  
      ![](../media/u5.png)

8. This will deploy a model that you will be playing around with as you proceed.

   ![](../media/u6.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:      
- If you receive a success message, you can proceed to the next task.
- If not, carefully read the error message and retry the step, following the instructions in the lab guide.
- If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.
     
<validation step="b04e38bd-81d8-4651-882b-bb5b0139fee8" />


### Task 3: Observe normal chat behavior without adding your own data

Before connecting Azure OpenAI to your data, first observe how the base model responds to queries without any grounding data.

1. In the **Playground** section, select the **Chat** page. 

   ![](../media/u7.png)

2. The **Chat** playground page consists of three main sections:

    - **Setup** - used to set the context for the model's responses.
    - **Chat session** - used to submit chat messages and view responses.
    - **Configuration** - used to configure settings for the model deployment.

3. In the **Configuration** section, ensure that your model deployment **`text-turbo(version:0125)`(1)** is selected.

4. In the **Setup** area, select the Default system message to set the context for the chat session. The default system message is **`You are an AI assistant that helps people find information`(2)**.

      ![](../media/u8.png)
   
      >**Note:** On the **Update system message?** pop-up, select **Continue**.

6. In the **Chat session**, submit the following queries **(1)**, click the send button **(2)** and review the responses:

      ```
      I'd like to take a trip to New York. Where should I stay?
      ```

      ```
      What are some facts about New York?
      ```

      ![](../media/u9.png)   

      ![](../media/u10.png)   

      >**Note:** Try similar questions about tourism and places to stay for other locations that will be included in our grounding data, such as London, or San Francisco. You'll likely get complete responses about areas or neighborhoods, and some general facts about the city.


### Task 4: Connect your data in the chat playground

Next, add your data in the chat playground to see how it responds with your data as grounding

1. Copy the URL (https://aka.ms/own-data-brochures) and paste it in the browser. Extract the PDFs in the `.zip` that get downloaded.

      - Click on the **File Explorer**, from the bottom taskbar.
      - Navigate to `C:\Users\azureuser\Downloads\` press **Enter**.
      - Right click on **brochures (1)** file and then click on **Extract all (2)**

        ![](../media/u11.png)

      - Click on **Extract**.

        ![](../media/u12.png)      

        ![](../media/u13.png)

1. In the **Azure portal**, search for **Storage Account** and select **Storage Account**.

      ![](../media/1.png)

1. On **Storage Account** page, click on **+ Create**.

      ![](../media/2.png)

1. Create a **Storage Account** resource with the following settings:

    - **Subscription**: Default - Pre-assigned subscription
    - **Resource group**: openai-<inject key="DeploymentID" enableCopy="false"></inject>
    - **Storage account name**: storage<inject key="DeploymentID" enableCopy="false"></inject>
    - **Region**: Select <inject key="Region" enableCopy="false" />
    - **Redundancy**: Locally-redundant storage (LRS)

    - Select **Next**
  
         ![](../media/openai-lab06_t4_s4.png "Create storage account")

    - **Allow enable anonymous access on individual containers**: check in the box to enable under advance section. Click on **Review + Create**  and subsequently click on **Create**

         ![](../media/image4.5.png "allow blob access")

1. Wait until the storage account is created before you proceed to the next task. This should take about a minute.

1. On the deployment blade, click **Go to resource**.

      ![](../media/3.png "upload files")

1. On the **Storage Account** blade, from the left navigation, select **Containers (1)**.

1. On **Storage Account | Containers** blade, click on **+ Containers (2)**.

      ![](../media/storage-container.png "upload files")

1. Create a container with the name "**openaidatasource**", and under **Anonymous access level** select **Container**. Select **Create**.

      ![](../media/image4.6.png "create container")

1. Select the **openaidatasource** container, and select **Upload**.

1. Upload all the files into the container which are downlaoded and extracted during the first step of Task 4.

      ![](../media/image4.7.png "upload files")

1. In the **Azure portal**, search for **AI search** and select **AI search**.

2.  On **Azure AI services | AI search (1)** blade, click on **Create (2)**.

      ![](../media/ai_search_create.png "upload files")

3. Create an **AI Search** resource with the following settings and click on **Review + create** and subsequenly click on **Create**

    - **Subscription**: Default - Pre-assigned subscription
    - **Resource group**: **openai-<inject key="DeploymentID" enableCopy="false"></inject>**
    - **Service name**: **cognitive-search-<inject key="DeploymentID" enableCopy="false"></inject>**
    - **Location**: Select **<inject key="Region" enableCopy="false" />**
    - **Pricing tier**: Basic

      ![](../media/openai-lab06_t4_s5.png "Create cognitive search resource")

1. Wait until your search resource has been deployed. Select **Go to resources**.

1. Navigate to the **cognitive-search-<inject key="DeploymentID" enableCopy="false"></inject>** and in the overview page copy the URL and paste it in a text editor such as notepad for later use.

      ![](../media/x689.png)

1. From the left navigation pane, under **Settings**, click on **Keys** and copy the primary key or secondary key and paste it in a notepad file for later use.

      ![](../media/keys-cognitive.png)

1. Navigate to the **Chat (1)** playground followed by select **Add your data(2)** in the setup pane and click on **+ Add a data source (3)**.

      ![](../media/add_data1.png "Add your data in setup pane")
   
1. In the **Add data**, enter the following values for your data source and then click on **Next**.

    - **Select data source (1)**: Azure Blob Storage
    - **Select Azure Blob storage resouce (2)**: *Choose the storage resource you created*
    - **Select storage container (3)**: *Choose the storage container you created*
    - **Select Azure AI Search resource (4)**: *Choose the search resource you created*
    - **Enter the index name (5)**: margiestravel
    - **Indexer schedule (6)**: Once
    - Click on **Next (7)**

      
     ![](../media/data_source-1.png "Add data configurations")
   
   
1. On the **Data management** page select the **1024(default)** search type from the drop-down, and then select **Next**.

      ![](../media/data_management-1.png "Add data")

1. On the **Data Connection** page, select **API key** and then click **Next**.
   
      ![](../media/api_key.png "Add data")
   
1. On the **Review and finish** page select **Save and close**, which will add your data. This may take a few minutes, during which you need to leave your window open. Once completed, verify if the data source, search resource, and index specified **margiestravel** is present under the **Add your data** tab in **Assistant setup** pane.
   
      ![](../media/save&close.png "Add data")
   
> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:      
- If you receive a success message, you can proceed to the next task.
- If not, carefully read the error message and retry the step, following the instructions in the lab guide.
- If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.
  
<validation step="f6630936-2440-4068-8b5e-3d93f1443da0" />


### Task 5: Chat with a model grounded in your data

1. Now that you've added your data, ask the same questions as you did previously, and see how the response differs.

   ```
   I'd like to take a trip to New York. Where should I stay?
   ```

   ```
   What are some facts about New York?
   ```

      >**Note:** You'll notice a very different response this time, with specifics about certain hotels and a mention of Margie's Travel, as well as references to where the information provided came from. If you open the PDF reference listed in the response, you'll see the same hotels as the model provided.
      
      >**Note:** If you encounter any errors, try refreshing the browser and repeating the process from step 1.

1. Try asking it about other cities included in the grounding data, which are Dubai, Las Vegas, London, and San Francisco.

      >**Note**: **Add your data** is still in preview and might not always behave as expected for this feature, such as giving the incorrect reference for a city not included in the grounding data.

### Task 6: Set up an application in Cloud Shell

To show how to integrate with an Azure OpenAI model, we'll use a short command-line application that runs in Cloud Shell on Azure. Open up a new browser tab to work with Cloud Shell.

1. In the [Azure portal](https://portal.azure.com?azure-portal=true), select the **[>_]** (*Cloud Shell*) button at the top of the page to the right of the search box. A Cloud Shell pane will open at the bottom of the portal.

      ![Screenshot of starting Cloud Shell by clicking on the icon to the right of the top search box.](../media/cloudshell-launch-portal.png)

2. The first time you open the Cloud Shell, you may be prompted to choose the type of shell you want to use (*Bash* or *PowerShell*). Select **Bash**.

3. Within the Getting Started pane, select **Mount storage account**, select your **Storage account subscription** from the dropdown and click **Apply**.

      ![](../media/cloudshell-getting-started.png)

4. Within the **Mount storage account** pane, select **I want to create a storage account** and click **Next**.

      ![](../media/cloudshell-mount-strg-account.png)


4. Within the **Advanced settings** pane, enter the following details:
    - **Subscription**: Default- Choose the only existing subscription assigned for this lab (1).
    - **CloudShell region**: East US (2)
    - **Resource group**: Select **Use existing**.(3)
      - openai-<inject key="DeploymentID" enableCopy="false"></inject>
    - **Storage account**: Select **Create new**.(4)
      - str<inject key="DeploymentID" enableCopy="false"></inject>
    - **File share**: Create a new file share named **none** (5)
    - Click **Create storage** (6)

      ![](../media/cloudshell-advanced-settings.png "Create storage advanced settings")

5. Make sure the type of shell indicated on the top left of the Cloud Shell pane is switched to *Bash*. If it's *PowerShell*, switch to *Bash* by using the drop-down menu.

6. Once the terminal starts, enter the following command to download the sample application and save it to a folder called `azure-openai`.

    ```bash
   rm -r azure-openai -f
   git clone https://github.com/MicrosoftLearning/mslearn-openai azure-openai
    ```

7. The files are downloaded to a folder named **azure-openai**. Navigate to the lab files for this exercise using the following command.

    ```bash
   cd azure-openai/Labfiles/06-use-own-data
    ```

    Applications for both C# and Python have been provided, as well as sample code we'll be using in this lab.

8. Open the built-in code editor, and you can observe the code files we'll be using in `sample-code`. Use the following command to open the lab files in the code editor.

    ```bash
   code .
    ```
    
   > **Note**: If you receive a popup to **Switch to Classic Cloud Shell** while running the **code .** command, click **Confirm**. Re-run commands from **steps 7 and 8** to and make sure you are in the correct project path.

      ![](../media/classic-cloudshell-prompt.png)
   
### Task 7: Configure your application

For this exercise, you'll complete some key parts of the application to enable using your Azure OpenAI resource.

1. In the code editor, expand the language folder for your preferred language.

2. Open the configuration file for your language.

    - **C#**: `appsettings.json`
    - **Python**: `.env`

3. Navigate to the folder for your preferred language and install the necessary packages.

     **C#**:

    ```
    cd CSharp
    dotnet add package Azure.AI.OpenAI --version 1.0.0-beta.14
    ```

    **Python**:

    ```
    cd Python
    pip install python-dotenv
    pip install openai==1.55.3
    ```

4. In the code editor from the left navigation pane, in the **CSharp** or **Python** folder, open the configuration file for your preferred language

    - **C#**: appsettings.json
    - **Python**: .env

5. Update the configuration values to include:
    - The  **endpoint** and a **key** from the Azure OpenAI resource you created (Which you copied in the previous task alternatively it is available on the **Keys and Endpoint** page for your Azure OpenAI resource in the Azure portal)
    
    - The **deployment name** you specified for your model deployment (available in the **Deployments** page in Azure AI Foundry portal that is **text-turbo**).
    
    - The endpoint for your AI search service (Which you copied in the previous task alternatively it is available in the **Url** value on the overview page for your AI search resource in the Azure portal).
    
    - A **key** for your search resource (available in the **Keys** page for your AI search resource in the Azure portal - you can use either of the admin keys)
    - The name of the search index (which should be `margiestravel`).

    - Press **Ctrl + S** on your keyboard to save the file.

      ![](../media/x676.png)

6. Open the code file for your preferred language, and replace the comment ***Configure your data source*** with code to add the Azure OpenAI SDK library:

    **C#**: OwnData.cs

    ```csharp
    // Configure your data source
    AzureSearchChatExtensionConfiguration ownDataConfig = new()
    {
            SearchEndpoint = new Uri(azureSearchEndpoint),
            Authentication = new OnYourDataApiKeyAuthenticationOptions(azureSearchKey),
            IndexName = azureSearchIndex
    };
    ```

    **Python**: ownData.py

    ```python
    # Configure your data source
    extension_config = dict(dataSources = [  
            { 
                "type": "AzureCognitiveSearch", 
                "parameters": { 
                    "endpoint":azure_search_endpoint, 
                    "key": azure_search_key, 
                    "indexName": azure_search_index,
                }
            }]
        )
    ```
      >**Note**: Ensure that the indentation is correct after pasting the code into the editor; it should align with the previous line.

7. Review the rest of the code, noting the use of the *extensions* in the request body that is used to provide information about the data source settings.

8. Press **Ctrl + S** on your keyboard to save the file.


## Task 8: Run your application

Now that your app has been configured, run it to send your request to your model and observe the response. You'll notice the only difference between the different options is the content of the prompt, all other parameters (such as token count and temperature) remain the same for each request.

1. If your using as **C#** language kindly open **CSharp.csproj** file replace with following code and save the file.

   ```
   <Project Sdk="Microsoft.NET.Sdk">
   
   <PropertyGroup>
   <OutputType>Exe</OutputType>
   <TargetFramework>net8.0</TargetFramework>
   <ImplicitUsings>enable</ImplicitUsings>
   <Nullable>enable</Nullable>
   </PropertyGroup>
   
    <ItemGroup>
    <PackageReference Include="Azure.AI.OpenAI" Version="1.0.0-beta.14" />
    <PackageReference Include="Microsoft.Extensions.Configuration" Version="8.0.*" />
    <PackageReference Include="Microsoft.Extensions.Configuration.Json" Version="8.0.*" />
    </ItemGroup>
   
    <ItemGroup>
      <None Update="appsettings.json">
        <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
       </None>
     </ItemGroup>
   
    </Project> 

   ```

1. In the interactive terminal pane, ensure the folder context is the folder for your preferred language. Then enter the following command to run the application.

    - **C#**: `dotnet run`
    - **Python**: `python ownData.py`

     ![](../media/python-output-1.png)

   > **Tip**: You can use the **Maximize panel size** (**^**) icon in the terminal toolbar to see more of the console text.

2. Review the response to the prompt `Tell me about London`, which should include an answer as well as some details of the data used to ground the prompt, which was obtained from your search service.

### Summary

In this lab, you have accomplished the following:
-   Provisioned an Azure OpenAI resource
-   Deployed an OpenAI model within the Azure AI Foundry portal
-   Used the power of OpenAI models to generate responses limited to a custom ingested data.

### You have successfully finished the lab. Click **Next** to continue to the next lab.
