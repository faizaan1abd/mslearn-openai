# Lab 01: Generate and improve code with Azure OpenAI Service

### Estimated Duration: 120 minutes

## Lab scenario
The Azure OpenAI Service models can generate code for you using natural language prompts, fixing bugs in completed code, and providing code comments. These models can also explain and simplify existing code to help you understand what it does and how to improve it.

## Lab objectives
In this lab, you will complete the following tasks:

- Task 1: Deploy a model
- Task 2: Generate code in chat playground
- Task 3: Set up an application in Cloud Shell
- Task 4: Configure your application
- Task 5: Run your application
  
### Task 1: Deploy a model

To use the Azure OpenAI API for code generation, you must first deploy a model to use through the **Azure OpenAI Studio**. Once deployed, we will use the model with the playground and reference that model in our app.

1. In the **Azure portal**, search for **OpenAI** and select **Azure OpenAI**.

   ![](../media/msi-image2.png)

1. On **Azure AI Services | Azure OpenAI** blade, select **openai-<inject key="DeploymentID" enableCopy="false"></inject>**

   ![](../media/msi-image3.png)

1. To capture the Keys and Endpoints values, on **openai-<inject key="DeploymentID" enableCopy="false"></inject>** blade:
      - Select **Keys and Endpoint (1)** under **Resource Management**.
      - Click on **Show Keys (2)**.
      - Copy **Key 1 (3)** and ensure to paste it into a text editor such as Notepad for future reference.
      - Finally, copy the **Endpoint (4)** API URL by clicking on copy to clipboard. Paste it in a text editor such as Notepad for later use.

        ![](../media/openai-endpoint-new.png "Keys and Endpoints")

1. In the Azure OpenAI resource pane, click on **Go to Azure OpenAI Studio** it will navigate to **Azure AI Studio**.

   ![](../media/msi-image4.png)

1. In the prompt select **Close** on **Discover an even better Azure AI Studio experience**. 

1. In the **Deployments (1)** page, click on **+ Deploy model** , Choose **Deploy base Model (2)**.

      ![](../media/Openai-04.png)

1. Search and select **GPT-35-TURBO-16K**, click on **Confirm**

      ![](../media/Openai-05.png)

1. Within the **Deploy model** pop-up interface, enter the following details:

    - **Deployment name**: 35turbo
    - **Deployment type**: Standard
    -  Select **Customize**

       ![](../media/msi-image5.png)
       
1. Within the **Deploy model** pop-up interface, enter the following details:
    - **Deployment name**: 35turbo (1)
    - **Deployment type**: Standard (2)
    - **Model Version**: accept default (3)
      
        >**Note** : gpt-35-turbo-16k is supported only for chat completions and it is not supported for completions API.<br>
    - **Tokens per Minute Rate Limit (thousands)**: 10K (4)
    - **Enable dynamic quota**: Enabled (5)
    - Click on **Deploy** (6)

       ![](../media/msi-image6.png)
      
   > **Note**:You can ignore the "Failed to fetch deployments quota information" notification.

   > **Note**: Each Azure OpenAI model is optimized for a different balance of capabilities and performance. We'll use the **3.5 Turbo** model series in the **GPT-3** model family in this exercise, which is highly capable for both language and code understanding.

<validation step="4a0f2d4d-175a-4dc9-8700-484bc47d1f3f" />
   
> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

### Task 2: Generate code in chat playground

Before using in your app, examine how Azure OpenAI can generate and explain code in the chat playground.

1. In [Azure OpenAI Studio](https://oai.azure.com/?azure-portal=true), from top menu ture on the **Toggle** to **Switch to the old look** and click on **skip** and then navigate to the **Chat** playground in the left pane.

      ![](../media/msi-image7.png)

1. In the **Setup** section at the top, select the **Default** (1) system message template and click on **continue**.

      ![](../media/msi-image8.png)

1. Scroll down and in the **Chat session** section, enter the following prompt and press *Enter*.

      ```code
      Write a function in python that takes a character and string as input, and returns how many times that character appears in the string
      ```

      ![](../media/msi-image9.png)
        
1. The model will likely respond with a function, with some explanation of what the function does and how to call it.
   
1. Next, send the prompt `Do the same thing, but this time write it in C#`.
   
1. Observe the output. The model likely responded very similarly as the first time, but this time coding in C#. You can ask it again 
   for a different language of your choice, or a function to complete a different task such as reversing the input string.
   
1. Next, let's explore using AI to understand code. Submit the following prompt as the user message.

      ```code
       What does the following function do?  
       ---  
       def multiply(a, b):  
       result = 0  
       negative = False  
       if a < 0 and b > 0:  
           a = -a  
           negative = True  
       elif a > 0 and b < 0:  
           b = -b  
           negative = True  
       elif a < 0 and b < 0:  
           a = -a  
           b = -b  
       while b > 0:  
           result += a  
           b -= 1      
       if negative:  
           return -result  
       else:  
           return result
      ```   

1. Observe the output, which explains what the function does, which is to multiply two numbers together by using a loop.

1. Submit the prompt `Can you simplify the function?`. The model should write a simpler version of the function.

1. Submit the prompt: `Add some comments to the function.` The model adds comments to the code.
    
### Task 3: Set up an application in Cloud Shell

To show how to integrate with an Azure OpenAI model, we'll use a short command-line application that runs in Cloud Shell on Azure. Open up a new browser tab to work with Cloud Shell.

1. In the [Azure portal](https://portal.azure.com?azure-portal=true), select the **[>_]** (*Cloud Shell*) button at the top of the page 
   to the right of the search box. A Cloud Shell pane will open at the bottom of the portal.

      ![](../media/Openai-08.png)

1. The first time you open the Cloud Shell, you may be prompted to choose the type of shell you want to use (Bash or PowerShell).Select Bash. If you don't see this option, skip the step.

      ![](../media/Openai-09.png)

1. Within the Getting Started pane, select Mount storage account (1), select your Storage account subscription (2) from the dropdown 
   and click Apply (3).

      ![](../media/Openai-10.png)

1. Within the Mount storage account pane, select I want to create a **storage account** **(1)** and click **Next** **(2)**.

      ![](../media/Openai-11.png)

1. Within the Advanced settings pane, enter the following details:

      - Subscription: Default- Choose the only existing subscription assigned for this lab (1).
      - Resource group: Select **openai-<inject key="DeploymentID" enableCopy="false"></inject>** **(2)**
      - Region: Select  **<inject key="Region" enableCopy="false" />** **(3)**
      - Storage account: Select **storage<inject key="DeploymentID" enableCopy="false"></inject>** **(4)**
      - File share: Create a new file share named **blob<inject key="DeploymentID" enableCopy="false"></inject>** **(5)**
      - Click **Create (6)**

        ![](../media/Openai-12.png)

1. Once the terminal starts, enter the following command to download the sample application and save it to a folder called `azure-openai`.

      ```bash
      rm -r azure-openai -f
      git clone https://github.com/MicrosoftLearning/mslearn-openai azure-openai
      ```

      >**NOTE:** If you get a message saying already cloned, please move to the next step.

1. The files are downloaded to a folder named **azure-openai**. Navigate to the lab files for this exercise using the following command.

      ```bash
      cd azure-openai/Labfiles/04-code-generation
      ```

      >**NOTE:** Applications for both C# and Python have been provided, as well as sample code we'll be using in this lab.

1. Open the built-in code editor, and you can observe the code files we'll be using in `sample-code`. Use the following command to open the lab files in the code editor.

      ```bash
      code .
      ```
   
      > **NOTE:** If you're prompted to **Switch to Classic Cloud Shell** after running the **code .** command, click on **Confirm** and make sure you are in the correct project path.

      ![](../media/classic-cloudshell-prompt.png)

1. Repeat the commands you executed in steps 7 and 8 for the language of your preference.


<validation step="d2e1f993-b207-40be-9554-9ece30e830a9" />

> **Congratulations** on completing the task! Now, it's time to validate it.
> - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

### Task 4: Configure your application

For this exercise, you'll complete some key parts of the application to enable using your Azure OpenAI resource.

1. In the code editor, expand the language folder for your preferred language.

1. Open the configuration file for your language.

      - **C#**: `appsettings.json`
      - **Python**: `.env`

1. Update the configuration values to include the **endpoint** and **key** from the Azure OpenAI resource you created, as well as the name of your deployment, `35turbo`. Then save the file by right-clicking on the file from the left pane and hit **Save**.

      - Navigate to the folder for your preferred language and install the necessary packages.

        **C#**
   
        ```bash
        cd CSharp
        dotnet add package Azure.AI.OpenAI --version 1.0.0-beta.14
        ```

        **Python**
   
        ```bash
        cd Python
        pip install python-dotenv
        pip install openai==1.13.3
        ```

1. Open the code file for your preferred language. In the function that calls the Azure OpenAI model, under the comment **Format and send the request to the model**, add the code to format and send the request to the model.

      - Open the code file for your preferred language.

        **C#**
        `Program.cs`
   
           ```csharp
           // Format and send the request to the model
             var chatCompletionsOptions = new ChatCompletionsOptions()
             {
                 Messages =
                 {
                     new ChatRequestSystemMessage(systemPrompt),
                     new ChatRequestUserMessage(userPrompt)
                 },
                 Temperature = 0.7f,
                 MaxTokens = 1000,
                 DeploymentName = oaiDeploymentName
             };
         
             // Get response from Azure OpenAI
             Response<ChatCompletions> response = await client.GetChatCompletionsAsync(chatCompletionsOptions);
         
             ChatCompletions completions = response.Value;
             string completion = completions.Choices[0].Message.Content;
          ```

        **Python**
        `code-generation.py`
   
          ```python
          # Format and send the request to the model
          messages =[
              {"role": "system", "content": system_message},
              {"role": "user", "content": user_message},
          ]
          
          # Call the Azure OpenAI model
          response = client.chat.completions.create(
              model=model,
              messages=messages,
              temperature=0.7,
              max_tokens=1000
          )
          ```
          >**Note**: Please make sure the indentation is correct and matches the code above before moving to the next task.
          
1. To save the changes made to the file, right-click on the file from the left pane, and hit **Save**

### Task 5: Run your application

Now that your app has been configured, run it to try generating code for each use case. The use case is numbered in the app, and can be 
run in any order.

> **Note**: Some users may experience rate limiting if calling the model too frequently. If you hit an error about a token rate limit, 
  wait for a minute then try again.

1. In the code editor, expand the `sample-code` folder and briefly observe the function and the app for your language. These files will 
   be used for the tasks in the app.

1. In the Cloud Shell bash terminal, navigate to the folder for your preferred language.

1. If your using **C#** language kindly open **CSharp.csproj** file and replace with the following code and save the file.

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
1. Run the application.

      - **C#**: `dotnet run`
      - **Python**: `python code-generation.py`

1. Choose option **1** to add comments to your code and enter the following prompt. Note, the response might take a few seconds for 
   each of these tasks.

      ```prompt
      Add comments to the following function. Return only the commented code.\n---\n
      ```

1. Next, choose option **2** to write unit tests for that same function and enter the following prompt.

      ```prompt
      Write four unit tests for the following function.\n---\n
      ```

1. Next, choose option **3** to fix bugs in an app for playing Go Fish. Enter the following prompt.

      ```prompt
      Fix the code below for an app to play Go Fish with the user. Return only the corrected code.\n---\n
      ```

1. Enter **quit** to exit the program.

1. The results will replace what was in `result/app.txt`, and should have very similar code with a few things corrected.

      - **C#**: Fixes are made on line 30 and 59
      - **Python**: Fixes are made on line 18 and 31

1. To check the results paste the following code in the terminal:

      ```
      cd result
      ```

1. Copy the below command in the terminal to see the contents of the app.txt file.

      ```
      cat app.txt
      ```

   - The app for Go Fish in `sample-code` can be run, if you replace the lines with bugs with the response from Azure OpenAI. If you run it without the fixes, it will not work correctly.

   - It's important to note that even though the code for this Go Fish app was corrected for some syntax, it's not a strictly accurate representation of the game. If you look closely, there are issues with not checking if the deck is empty when drawing cards, not removing pairs from the players hand when they get a pair, and a few other bugs that require understanding of card games to realize. This is a great example of how useful generative AI models can be to assist with code generation, but can't be trusted as correct and need to be verified by the developer.

   - If you would like to see the full response from Azure OpenAI, you can set the `printFullResponse` variable to `True`, and rerun the app.

## Summary

By completing this lab, you’ve gained hands-on experience with Azure OpenAI Service models, demonstrating how AI can be a powerful tool in code generation, bug fixing, and code comprehension. You’ve learned to deploy models, utilize the Chat Playground for code-related tasks, and integrate AI into a real-world application through Azure Cloud Shell. Additionally, you've explored the capabilities of the DALL-E model for image generation. These skills will help you leverage AI to enhance your coding workflow, making development more efficient and insightful.

## Review

In this lab, you have accomplished the following:
-   Provision an Azure OpenAI resource
-   Deploy an OpenAI model within the Azure OpenAI studio
-   Use the functionalites of the Azure OpenAI to generate and improvise code for your production applications.

## You have successfully completed the lab. Click on Next >> to procced with next exercise.
