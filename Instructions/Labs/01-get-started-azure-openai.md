# Lab 01: Get started with Azure OpenAI Service

### Estimated time: 60 minutes

Azure OpenAI Service brings the generative AI models developed by OpenAI to the Azure platform, enabling you to develop powerful AI solutions that benefit from the security, scalability, and integration of services provided by the Azure cloud platform. In this exercise, you'll learn how to get started with Azure OpenAI by provisioning the service as an Azure resource and using Azure AI Foundry portal to deploy and explore OpenAI models.

## Lab objectives
In this lab, you will complete the following tasks:

- Task 1: Provision an Azure OpenAI resource
- Task 2: Deploy a model
- Task 3: Explore a model in the Completions playground
- Task 4: Use the Chat playground
- Task 5: Explore prompts and parameters 
- Task 6: Explore code-generation

## Task 1: Provision an Azure OpenAI resource

In this task , you'll create an Azure resource in the Azure portal, selecting the OpenAI service and configuring settings such as region and pricing tier. This setup allows you to integrate OpenAI's advanced language models into your applications.

1. In the **Azure portal**, search for **Azure OpenAI** and select **Azure OpenAI**.

   ![](../media/tel-11.png)

2. On **Azure AI Services | Azure OpenAI** blade, click on **Create**.

   ![](../media/tel-10.png)

3. Create an **Azure OpenAI** resource with the following settings:
   
    - **Subscription**: Default - Pre-assigned subscription.
    - **Resource group**: openai-<inject key="DeploymentID" enableCopy="false"></inject>
    - **Region**: Select **Swedencentral**
    - **Name**: OpenAI-Lab01-<inject key="DeploymentID" enableCopy="false"></inject>
    - **Pricing tier**: Standard S0
  
      ![](../media/openai-lab01_01.png "Create Azure OpenAI resource")

      >**Note** : **Please deploy Openai resource in Swedencentral Region**.

4. Click on **Next** thrice by keeping others default and click on **Create**.

5. Wait for deployment to complete. Then go to the deployed Azure OpenAI resource in the Azure portal.

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="1fa0e87b-eb46-463d-b63b-edf6e2282e16" />

## Task 2: Deploy a model

In this task, you'll deploy a specific AI model instance within your Azure OpenAI resource to integrate advanced language capabilities into your applications.

1. In the **Azure portal**, search for **Azure OpenAI** and select **Azure OpenAI**.

   ![](../media/tel-11.png)

2. On the **Azure AI Services** page, ensure that **Azure OpenAI (1)** is selected from the left blade. Then, select **OpenAI-Lab01-<inject key="Deployment-id" enableCopy="false"></inject> (2)**

   ![](../media/update07.png)

3. In the Azure OpenAI resource pane, click on **Go to Azure AI Foundry portal** it will navaigate to **Azure AI Foundry portal**.

   ![](../media/update08.png)

4. On the **Azure AI Foundry portal** page, select **Deployments (1)** under **Shared Resources** from the left pane. Then, click **+ Deploy Model** and choose **Deploy Base Model (2)**.

      ![](../media/ui1.png)

5. Search for **gpt-4o-mini**, click on **Confirm**

   ![](../media/gpt-4-mini.png)
   
6. Within the **Deploy model** pop-up interface, enter the following details:
      - **Deployment name**: my-gpt-model (1)
      - **Deployment type**: Standard(2)
      - Click on **Customize**
      - **Model version**:2024-07-18(default) (3)
      - **Tokens per Minute Rate Limit (thousands)**: 10K (4)
      - **Enable dynamic quota**: Enabled (5)
      - Click on **Deploy** (6)
  
           ![](../media/gpt-4omini.png)

           >**Note** : gpt-4o-mini is supported only for chat completions and it is not supported for completions API.

7. Click the back arrow on the newly created model, then select **Deployments (1)** under **Shared Resources** in the left pane. After that, click **+ Deploy Model** and choose **Deploy Base Model (2)**.

      ![](../media/ui1.png)

8. Search for **Babbage-002**, click on **Confirm**

   ![](../media/babbage-02.png)
   
9. Within the **Deploy model** pop-up interface, enter the following details:
      - **Deployment name**: babbage-002 (1)
      - **Deployment type**: Standard(2)
      - Click on **Customize**
      - **Model version**:1 (3)
      - **Tokens per Minute Rate Limit (thousands)**: 10K (4)
      - **Enable dynamic quota**: Enabled (5)
      - Click on **Deploy** (6)
  
           ![](../media/babbage-2.1.png)

10. These will deploy models that you can experiment with for both chat and completion tasks as you go along.

      > **Note**: You can ignore any error related to assignment of roles to view the quota limits. 
   
     > **Note**: Azure OpenAI offers a variety of models, each optimized for different balances of capabilities and performance. In this exercise, you'll be using the **gpt-4o-mini** and a completion model, which is well-suited for tasks like summarizing and generating natural language and code. For more details on the available models in Azure OpenAI, refer to the [Models](https://learn.microsoft.com/azure/cognitive-services/openai/concepts/models) page in the Azure OpenAI documentation.

   
   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps
   > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
   > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

   <validation step="3b4a472e-f956-45d8-b828-3e2cc01c2e88" />

## Task 3: Explore a model in the Completions playground

In this task ,You'll Explore a model in the Completions playground involves interacting with the AI model to test and refine its responses using real-time input and output examples.

1. In Azure AI Foundry Portal, in the left pane under **Playground**, select **Completions**.

2. In the **Completions playground** page, ensure your **my-gpt-model** deployment is selected , Copy paste this `Generate a quiz of 5 questions  For each question, provide me the answer options and the correct answer` in the Prompt.

      ![](../media/generate_01.png)

      >**Note:** The summarize text sample consists of a *prompt* that provides some text to tell the model what kind of response is required and include some contextual information.

3. At the bottom of the page, note the number of *tokens* detected in the text. Tokens are the basic units of a prompt - essentially words or word-parts in the text.

      ![](../media/gnrttoken.png)

4. Use the **Generate** button to submit the prompt to the model and retrieve a response (you may need to scroll down). The response consists of a quiz based on the example in the prompt.

      ![](../media/generated.png)

      >**Note**: Sometime it can happen the OpenAI wont provide you the exact output, in that case you can use the **Regenerate** button to resubmit the prompt(new changes have been made), and note that the response may vary from the original one. A generative AI model can produce new language each time it's called.

5. Use the **View Code** button to view the code that a client application would use to submit the prompt. You can select your preferred programming language. The prompt contains the text you submitted to the model. The request is submitted to the *Completions* API for your Azure OpenAI service.

      ![](../media/imag01.png)

      ![](../media/openai-7u.png)
    
6. Close the **Sample Code**.

## Task 4: Use the Chat playground

In this task, you'll use the Chat playground to interact with and test the AI model's conversational abilities through a simulated chat interface.

1. In the **Playground** section, select the **Chat** page, and ensure that the **my-gpt-model** model is selected in the configuration pane.

2. In the **Setup** section, in  **Give the model instructions and context** box, replace the current text with the following statement: `The system is an AI teacher that helps people learn about AI`.

      ![](../media/setup-1.png)

3. Click on **+ Add Section** drop-down menu and select **Examples**. Now enter the following message and response in the designated boxes:

      ![](../media/imag8u.png)

4.  Enter the following message and response in the designated boxes:

      - **User**: `What are different types of artificial intelligence?`
      - **Assistant**: `There are three main types of artificial intelligence: Narrow or Weak AI (such as virtual assistants like Siri or Alexa, image recognition software, and spam filters), General or Strong AI (AI designed to be as intelligent as a human being. This type of AI does not currently exist and is purely theoretical), and Artificial Superintelligence (AI that is more intelligent than any human being and can perform tasks that are beyond human comprehension. This type of AI is also purely theoretical and has not yet been developed).`

         ![](../media/exples-ai.jpg)
   
         > **Note**: Few-shot examples are used to demonstrate the desired tone, style, and type of responses expected from the model. These examples guide the model to generate responses that align with the provided patterns.

5. Save the changes by clicking on **Apply changes** 

   ![](../media/image7u-1.png)

6. On Update system message? pop-up, click on **Continue**.

   ![](../media/image4.png)
   
7. In the query box on the left side at the bottom of the page, enter the text `What is artificial intelligence?` **(1)**. Click the **Send (2)** button to submit the prompt and view the response.

      ![](../media/openai-12.png)
   
      > **Note**: You may receive a response that the API deployment is not yet ready. If so, wait for a few minutes and try again.

8. Review the response and then submit the following message to continue the conversation: `How is it related to machine learning?`

9. Review the response, noting that context from the previous interaction is retained (so the model understands that "it" refers to artificial intelligence).

10. Use the **View Code** button to view the code for the interaction. The prompt consists of the *system* message, the few-shot examples of *user* and *assistant* messages, and the sequence of *user* and *assistant* messages in the chat session so far.
            
      ![](../media/image5.png)

## Task 5: Explore prompts and parameters

In this task, you'll explore prompts and parameters by experimenting with different inputs and settings to fine-tune the AI model's responses and behavior.

1. In the **Setup** pane select **Parameters (1)** , set the following parameter values:
      
      > **Note**: You may need to scrolldown to see the parameters option
      
      - **Max response**: 500 **(2)**
      - **Temperature**: 0 **(3)**
      

         ![](../media/image6.png)
      
2. Submit the following message in chat session

      ```
      Write three multiple choice questions based on the following text.

      Most computer vision solutions are based on machine learning models that can be applied to visual input from cameras, videos, or images.*

      - Image classification involves training a machine learning model to classify images based on their contents. For example, in a traffic monitoring solution you might use an image classification model to classify images based on the type of vehicle they contain, such as taxis, buses, cyclists, and so on.*

      - Object detection machine learning models are trained to classify individual objects within an image, and identify their location with a bounding box. For example, a traffic monitoring solution might use object detection to identify the location of different classes of vehicle.*

      - Semantic segmentation is an advanced machine learning technique in which individual pixels in the image are classified according to the object to which they belong. For example, a traffic monitoring solution might overlay traffic images with "mask" layers to highlight different vehicles using specific colors.
      
      ```

3. Review the results, which should consist of multiple-choice questions that a teacher could use to test students on the computer vision topics in the prompt. The total response should be smaller than the maximum length you specified as a parameter.

      ![](../media/last-3.jpg)
   
4. Observe the following about the prompt and parameters you used:

    - The prompt specifically states that the desired output should be three multiple choice questions.
       
    - The parameters include *Temperature*, which controls the degree to which response generation includes an element of randomness. The value of **0** used in your submission minimizes randomness, resulting in 
         stable, predictable responses.

## Task 6: Explore code-generation

In this task, you'll explore code-generation by testing the AI model’s ability to generate and suggest code snippets based on various programming prompts and requirements.

1. In the **Setup** section, in the **Give the model instructions and context** box, replace the current text with the following statement: `You are a Python developer.` for Give the model instructions and context and save the changes by clicking on **Apply Changes** when prompted click on **Continue**.

      ![](../media/imag8-1.png)
      

3. In the **Chat session** pane, select **Clear chat** to clear the chat history and start a new session.
   
      ![](../media/openai-14u.png)

4. Submit the following user message:

      ```
      Write a Python function named Multiply that multiplies two numeric parameters.
      ```

5. Review the response, which should include sample Python code that meets the requirement in the prompt.
   
      ![](../media/task-6-last.jpg)

## Summary

In this lab, you have accomplished the following:
-   Provision an Azure OpenAI resource
-   Deploy an Azure OpenAI model within the Azure AI Foundry portal
-   Use the chat playground to utilize the functionalities of prompts, parameters and code-generation

##   You have successfully completed the lab.
