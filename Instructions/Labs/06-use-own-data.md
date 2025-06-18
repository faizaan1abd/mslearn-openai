# Lab 06:  Add your data for RAG with Azure OpenAI Service

## Estimated Duration: 75 minutes

## Lab scenario
The Azure OpenAI Service enables you to use your own data with the intelligence of the underlying LLM. You can limit the model to only use your data for pertinent topics or blend it with results from the pre-trained model.

## Lab objectives

In this lab, you will complete the following tasks:

- Task 1: Observe normal chat behavior without adding your own data
- Task 2: Connect your data in the chat playground
- Task 3: Chat with a model grounded in your data
- Task 4: Set up an application in Cloud Shell
- Task 5: Configure your application
- Task 6: Run your application

### Task 1: Observe normal chat behavior without adding your own data

Before connecting Azure OpenAI to your data, first observe how the base model responds to queries without any grounding data.

1. In the **Playgrounds** section, select the **Chat (1)** page. The **Chat** playground page consists of two main sections:

     - **Setup (2)** - used to set the context for the model's responses.
     - **Chat session (3)** - used to submit chat messages and view responses.

        ![](../media/dev-genai-june-11.png)

2. In the **deployment** section, ensure that your model deployment **my-gpt-model** is selected.

3. In the **Setup** area, the default system message is set to *You are an AI assistant that helps people find information*.

4. In the **Chat session**, submit the following queries, and review the responses:

    ```
    I'd like to take a trip to New York. Where should I stay?
    ```

    ```
    What are some facts about New York?
    ```

    Try similar questions about tourism and places to stay for other locations that will be included in our grounding data, such as London, or San Francisco. You'll likely get complete responses about areas or neighbourhoods, and some general facts about the city.


### Task 2: Connect your data in the chat playground

In this task, you will observe how the base model responds to queries without any grounding data before connecting Azure OpenAI to your data.

1. Copy the URL (https://aka.ms/own-data-brochures) and paste it in the browser. Extract the PDFs in the `.zip` that get downloaded.
   
1. In the **Azure portal**, search for **Storage Account** and select **Storage Account**.

   ![](../media/L6T2S2-0205.png)

1. On **Storage Account** page, click on **+ Create**.

   ![](../media/L6T2S3-0205.png)

1. To create a **Storage Account** resource enter the following details and click on **Next (7)**:

   | Settings | Action |
   | -- | -- |
   | **Subscription** | Default - Pre-assigned subscription (1) |
   | **Resource group** | openai-<inject key="DeploymentID" enableCopy="false"></inject> (2) |
   | **Region** | Select <inject key="Region" enableCopy="false" /> (4) |
   | **Storage account name (4)** | storage1<inject key="DeploymentID" enableCopy="false"></inject> (3) |
   | **Primary Service** | Azure Blob Storage or Azure Data Lake Storage Gen 2 (5) |
   | **Redundancy** | Locally-redundant storage (LRS) (6) |
  
    ![](../media/dev-genai-june-12.png "Create storage account")

1. Under the **Advanced** section, provide the following details:

   | Settings | Action |
   | -- | -- |
   | **Allow enable anonymous access on individual containers (1)** | Check in the box to enable under **Advanced** section. |
   | Click on **Review + create (2)**  and subsequently click on **Create**. |

    ![](../media/dev-genai-june-13.png "allow blob access")

1. Wait until the storage account is created before you proceed to the next task. This should take about a minute.

1. On the deployment blade, click **Go to resource**.

    ![](../media/L6T2S6-0205.png "upload files")

1. On **Storage Account**, go to **Container (1)** blade under Data Storage and click on **+ Container (2)** to create a new container.

     ![](../media/L6T2S7-0205-1.png "upload files")

1. Create a container with the name **openaidatasource (1)**, enable **Anonymous access level for container (2)** and click on **Create (3)**.

      ![](../media/L6T2S8-0205.png "create container")

1. Select the **openaidatasource** container, on the **openaidatasource** container blade, click on **Upload**. 

      ![](../media/L6T2S9-0205-1.png "upload files")

1. From the right pane, click on **Browse for files**.

      ![](../media/L6T2S9-0205-5.png)

1. Search for and go to location `C:\AllFiles\mslearn-openai-main\Labfiles\06-use-own-data\data` (1). Select all the **pdf files (2)** and click on **Open (3)**. Then click on **Upload** to upload all pdf files. 

    ![](../media/L6T2S9-0205-3.png)

1. Verify **openaidatasource** container after all files are uploaded.

    ![](../media/L6T2S9.1-0205.png "upload files")

1. In the **Azure portal**, search for **AI search (1)** and select **AI search (2)**.

    ![](../media/L6T2S9-0205-4.png)

1. On **AI Foundry | AI search (1)** blade, click on **+ Create (2)**.

    [](../media/L6T2S11-0205-2.png "upload files")

1. Create an **AI Search** resource with the following settings and click on **Review + create (5)** and subsequently click on **Create**.


   | Settings | Action |
   | -- | -- |
   | **Subscription** | Default - Pre-assigned subscription |
   | **Resource group (1)** | **openai-<inject key="DeploymentID" enableCopy="false"></inject>** |
   | **Service name (2)** | **cognitive-search-<inject key="DeploymentID" enableCopy="false"></inject>** |
   | **Location (3)** | Select **<inject key="Region" enableCopy="false" />** |
   | **Pricing tier (4)** | Change the Pricing tier to **Basic** |

    ![](../media/L6T2S12-0205.png "Create cognitive search resource")

1. Wait until your search resource has been deployed.

1. Navigate to the **cognitive-search-<inject key="DeploymentID	" enableCopy="false"></inject>** and in the overview page copy the URL and paste it in a text editor such as notepad for later use.

    ![](../media/L6T2S14-0205.png)

1. From the left navigation pane, click on **Keys** and copy the primary key or secondary key and paste it in a notepad file for later use.

      ![](../media/L6T2S15-0205.png)

1. In **Azure AI Foundry portal**, navigate to the **Chat (1)** playground followed by select **Add your data (2)** in the setup pane and click on **+ Add a data source (3)**.

    ![](../media/chat_playground-1.png)
   
1. In the **Add data**, enter the following values for your data source and then click on **Next (7)** to proceed with **Data Management**.

   | Setting | Action |
   | -- | -- |
   | **Select data source (1)** | Azure Blob Storage (preview) |
   | **Select Azure Blob storage resource (2)** | *Choose the storage resource **storage1<inject key="DeploymentID" enableCopy="false"></inject>** you created* (If it isn’t visible, try clicking Refresh next to the storage account) |
   | **Select Storage container (3)** | openaidatasource |
   | **Select Azure AI Search resource (4)** | *Choose **cognitive-search-<inject key="DeploymentID	" enableCopy="false"></inject>** search resource you created* |
   | **Enter the index name (5)** | margiestravel |
   | **Indexer schedule (6)** | Once |
   
    ![](../media/image4-8-1.png "Add data configurations")
   
1. On the **Data management** page select the **Keyword (1)** search type from the drop-down, and then select **Next (2)**.

    ![](../media/lab6-g4-1.png "Add data")

1. On the **Data connection** page select the **API key (1)** , Click on the **Next (2)**

    ![](../media/API_key-1.png "Add data")
   
1. On the **Review and finish** page select **Save and close**, which will add your data. Once completed, verify if the data source, search resource, and index specified **margiestravel** is present under the **Add your data(preview)** tab in **Assistant setup** pane.

    ![](../media/review-1.png "Add data")

 - This may take a few minutes, during which you need to leave your window open.
       
    ![](../media/review-2.png)
  
 - Once completed, verify if the data source, search resource, and index specified **margiestravel** is present under the **Add your data** tab in **Assistant setup** pane.

    ![](../media/review-3.png)   

### Task 3: Chat with a model grounded in your data

In this task, you will ask the same questions as before after adding your data, and observe how the responses differ.

   ```
   I'd like to take a trip to New York. Where should I stay?
   ```

   ```
   What are some facts about New York?
   ```

You'll notice a very different response this time, with specifics about certain hotels and a mention of Margie's Travel, as well as references to where the information provided came from. If you open the PDF reference listed in the response, you'll see the same hotels as the model provided.

Try asking it about other cities included in the grounding data, which are Dubai, Las Vegas, London, and San Francisco.

> **Note**: **Add your data** is still in preview and might not always behave as expected for this feature, such as giving the incorrect reference for a city not included in the grounding data.

### Task 4: Set up an application in Cloud Shell

In this task, you will use a short command-line application running in Cloud Shell on Azure to demonstrate integration with an Azure OpenAI model. Open a new browser tab to access Cloud Shell.

1. In the [Azure portal](https://portal.azure.com?azure-portal=true), select the **[>_]** (*Cloud Shell*) button at the top of the page to the right of the search box. A Cloud Shell pane will open at the bottom of the portal.

      ![Screenshot of starting Cloud Shell by clicking on the icon to the right of the top search box.](../media/cloudshell-launch-portal.png)

2. Make sure the type of shell indicated on the top left of the Cloud Shell pane is **Switch to PowerShell**. If it's *Bash*, select **Switch to Bash** and choose **Confirm** from the pop up box.

    ![](../media/dev-genai-june-4.png)

3. Once the terminal opens, click on **Settings** and select **Go to Classic version**.

   ![](../media/classic-cloudshell.png)

4. Once the terminal starts, enter the following command to download the sample application and save it to a folder called `azure-openai`.

    ```bash
   rm -r azure-openai -f
   git clone https://github.com/MicrosoftLearning/mslearn-openai azure-openai
    ```

5. The files are downloaded to a folder named **azure-openai**. Navigate to the lab files for this exercise using the following command.

    ```bash
   cd azure-openai/Labfiles/06-use-own-data
    ```

    Applications for both C# and Python have been provided, as well as sample code we'll be using in this lab.

6. Open the built-in code editor, and you can observe the code files we'll be using in `sample-code`. Use the following command to open the lab files in the code editor.

    ```bash
   code .
    ```

### Task 5: Configure your application

In this task, you will complete key parts of the application to enable it to use your Azure OpenAI resource.

1. In the code editor, expand the language folder for your preferred language.

2. Open the configuration file for your language.

    - **C#**: `appsettings.json`
    - **Python**: `.env`

3. Update the configuration values to include:
    - The  **endpoint** and a **key** from the Azure OpenAI resource you created (Which you copied in the previous task alternatively it is available on the **Keys and Endpoint** page for your Azure OpenAI resource in the Azure portal)
    - The **deployment name** you specified for your model deployment (available in the **Deployments** page in Azure AI Foundry portal that is **my-gpt-model**).
    - The endpoint for your AI search service (Which you copied in the previous task alternatively it is available in the **Url** value on the overview page for your AI search resource in the Azure portal).
    - A **key** for your search resource (available in the **Keys** page for your AI search resource in the Azure portal - you can use either of the admin keys)
    - The name of the search index (which should be `margiestravel`).

         ![](../media/x676.png)

1. If your using **C#**, navigate to `CSharp.csproj`, delete the existing code, then replace it with the following code and then press **Ctrl+S** to save the file.

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
     <PackageReference Include="Microsoft.Extensions.Configuration" Version="8.0.404" />
     <PackageReference Include="Microsoft.Extensions.Configuration.Json" Version="8.0.404" />
     </ItemGroup>

     <ItemGroup>
       <None Update="appsettings.json">
         <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
        </None>
     </ItemGroup>

    </Project>
    ```    

     ![](../media/u47upd.png)    

1. Navigate to the **CSharp** folder and install the necessary packages.

     **C#**:

    ```
    cd CSharp
    export DOTNET_ROOT=$HOME/.dotnet
    export PATH=$DOTNET_ROOT:$PATH
    mkdir -p $DOTNET_ROOT
    ```     

     >**Note**: Azure Cloud Shell often does not have admin privileges, so you need to install .NET in your home directory. So here you are creating a separate `.dotnet` directory under your home directory to isolate your configuration.
     - `DOTNET_ROOT` specifies where your .NET runtime and SDK are located (in your `$HOME/.dotnet directory`).
     - `PATH=$DOTNET_ROOT:$PATH` ensures that the locally installed .NET SDK can be accessed globally by your terminal.
     - `mkdir -p $DOTNET_ROOT` this creates the directory where the .NET runtime and SDK will be installed.

1. Run the following command to install the required SDK version locally:     

     ```
     wget https://dotnet.microsoft.com/download/dotnet/scripts/v1/dotnet-install.sh
     chmod +x dotnet-install.sh
     ./dotnet-install.sh --version 8.0.404 --install-dir $DOTNET_ROOT
     ```

      >**Note**: These commands download and prepare the official `.NET` installation script, grant it execute permissions, and install the required .NET SDK version (8.0.404) in the `$DOTNET_ROOT` directory as we don't have the admin privileges to install it globally.

1. Enter the following command to restore the workload.

    ```
    dotnet workload restore
    ```

     >**Note**: Restores any required workloads for your project, such as additional tools or libraries that are part of the .NET SDK.
    
1. Enter the following command to add the `Azure.AI.OpenAI` NuGet package to your project, which is necessary for integrating with Azure OpenAI services.

    ```
    dotnet add package Azure.AI.OpenAI --version 1.0.0-beta.14
    ```

1. If your using **Python**, navigate to `ownData.py`, delete the existing code, then replace it with the following code and then press **Ctrl+S** to save the file.

    ```
    import os
    import json
    from dotenv import load_dotenv
    import openai
    
    def main():
        try:
            # Flag to show citations
            show_citations = False
    
            # Load configuration settings from .env file
            load_dotenv()
            azure_oai_endpoint = os.getenv("AZURE_OAI_ENDPOINT")
            azure_oai_key = os.getenv("AZURE_OAI_KEY")
            azure_oai_deployment = os.getenv("AZURE_OAI_DEPLOYMENT")
            azure_search_endpoint = os.getenv("AZURE_SEARCH_ENDPOINT")
            azure_search_key = os.getenv("AZURE_SEARCH_KEY")
            azure_search_index = os.getenv("AZURE_SEARCH_INDEX")
    
            # Configure OpenAI for Azure
            openai.api_type = "azure"
            openai.api_base = azure_oai_endpoint
            openai.api_key = azure_oai_key
            openai.api_version = "2023-09-01-preview"
    
            # Get user input
            text = input('\nEnter a question:\n')
    
            # Define the request payload with extension (Cognitive Search)
            headers = {
                "Content-Type": "application/json",
                "api-key": azure_oai_key
            }
    
            # "extensions" is not supported directly by openai SDK
            # Instead, construct the request using requests module
            import requests
    
            endpoint_url = f"{azure_oai_endpoint}/openai/deployments/{azure_oai_deployment}/extensions/chat/completions?api-version=2023-09-01-preview"
    
            payload = {
                "messages": [
                    {"role": "system", "content": "You are a helpful travel agent."},
                    {"role": "user", "content": text}
                ],
                "temperature": 0.5,
                "max_tokens": 1000,
                "dataSources": [
                    {
                        "type": "AzureCognitiveSearch",
                        "parameters": {
                            "endpoint": azure_search_endpoint,
                            "key": azure_search_key,
                            "indexName": azure_search_index
                        }
                    }
                ]
            }
    
            print("\n...Sending request to Azure OpenAI with data source...\n")
            response = requests.post(endpoint_url, headers=headers, json=payload)
            response.raise_for_status()
            result = response.json()
    
            print("Response:\n")
            print(result["choices"][0]["message"]["content"])
    
            if show_citations and "citations" in result["choices"][0]["message"]:
                print("\nCitations:")
                for citation in result["choices"][0]["message"]["citations"]:
                    print(f"  Title: {citation.get('title', 'N/A')}")
                    print(f"  URL: {citation.get('url', 'N/A')}")
    
        except Exception as ex:
            print("Error:", ex)
    
    if __name__ == '__main__':
        main()            
    ```    

    ![](../media/x676-1.png)


1. Navigate to the **Python** folder and install the necessary packages.

    **Python**:

    ```
    cd ..
    cd Python
    pip install python-dotenv
    pip install openai==1.56.2
    pip install openai requests python-dotenv
    ```
      > **Note:** If you receive a permission error after executing the installation command as shown in the image, please run the below command for installation.
      >    ![](../media/L2T3S9python-0205.png)
      > ```bash
      > pip install --user python-dotenv
      > pip install --user openai==1.56.2
      > pip install --user openai requests python-dotenv
      > ```

1. Open the code file for **C#**, and replace the comment ***Configure your data source*** with code to add the Azure OpenAI SDK library:

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

6. Review the rest of the code, noting the use of the *extensions* in the request body that is used to provide information about the data source settings.

7. Save the changes to the code file.

## Task 6: Run your application

In this task, you will run your configured app to send a request to your model and observe the response, noting that the only difference between options is the prompt content while all other parameters (such as token count and temperature) remain consistent.

In this task, you will run the reviewed code to generate some images.

1. In the Cloud Shell bash terminal, navigate to the folder for your preferred language.

2. In the interactive terminal pane, ensure the folder context is the folder for your preferred language. Then enter the following command to run the application.

    - **C#**: `dotnet run`
    - **Python**: `python ownData.py`

    > **Tip**: You can use the **Maximize panel size** (**^**) icon in the terminal toolbar to see more of the console text.

3. Review the response to the prompt `Tell me about London`, which should include an answer as well as some details of the data used to ground the prompt, which was obtained from your search service.

    ![](../media/dev-genai-june-14.png "upload files")

## Summary

In this lab, you have accomplished the following:

- Used the power of OpenAI models to generate responses limited to a custom ingested data.

## Congratulations on successfully completing the lab! Click Next >> to continue to the next lab.