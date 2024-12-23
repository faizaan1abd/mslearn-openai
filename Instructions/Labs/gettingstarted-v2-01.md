# Get started with Azure OpenAI Service

### Overall Estimated Duration: 1 hour

## Overview

This lab introduces the Azure OpenAI Service, which brings OpenAI's advanced generative AI models to the Azure platform. You'll leverage Azure's security, scalability, and integration capabilities to develop robust AI solutions. In this exercise, you'll learn how to provision the Azure OpenAI Service as a resource and explore OpenAI models using the Azure AI Foundry portal.

## Objective

This lab is aimed to give learners hands-on experience with Azure OpenAI resources, deploy and explore models using the Completions and Chat playgrounds, and experiment with prompts, parameters, and code generation. By the end of this lab, you will be able to:

- **Get started with the Azure OpenAI Service:** This hands-on exercise aims to teach you the fundamentals of using Azure OpenAI Service to integrate advanced AI models into your apps. Participants will set up and begin utilizing the Azure OpenAI Service to integrate AI models into their applications.

## Pre-requisites

- **Development Skills:** Basic programming knowledge and experience with APIs and SDKs.

- **AI Concepts:** Understanding prompt engineering, code development, and image generation using models such as DALL-E.

- **Content Management:** Understanding data integration for RAG and content filtering techniques.

## Architecture

The architecture leverages Azure OpenAI Service to deploy and explore OpenAI models. An Azure resource is provisioned, and the Completions and Chat playgrounds are used for interactive exploration. Prompts, parameters, and code generation are optimized to create efficient AI-driven solutions with Azure's scalability and security.

## Architecture Diagram

 ![](../media/lab1arc.JPG)

## Explanation of Components

The architecture for this lab involves the following key components:

- **Azure OpenAI Resource:** Provision an Azure OpenAI resource to enable access to OpenAI's generative AI capabilities on the Azure platform.

- **Model Deployment:** Deploy a selected OpenAI model to make it accessible for testing and integration.

- **Completions Playground:** Explore the deployed model in the Completions playground to understand how it generates text-based outputs for specific prompts.

- **Chat Playground:** Use the Chat playground to interact with the model in a conversational manner, leveraging its natural language understanding capabilities.

- **Code Generation:** Explore the model's ability to generate code snippets and other structured outputs, showcasing its utility in development scenarios.

## Getting Started with Lab

1. Once the environment is provisioned, a virtual machine (JumpVM) and lab guide will get loaded in your browser. Use this virtual machine throughout the workshop to perform the lab. You can see the number on the bottom of the lab guide to switch to different exercises of the lab guide.

   ![](../media/Intro.png)

## Exploring Your Lab Resources

To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.

![](../media/env-01.png)

## Utilizing the Split Window Feature

For convenience, you can open the lab guide in a separate window by selecting the Split Window button from the top right corner.

![](../media/split-01.png)

## Lab Guide Zoom In/Zoom Out
 
To adjust the zoom level for the environment page, click the **A↕ : 100%** icon located next to the timer in the lab environment.

![](../media/n21.png)  

## Managing Your Virtual Machine

Feel free to start, stop, or restart your virtual machine as needed from the **Resources** tab. Your experience is in your hands!

![](../media/resourses.png)
    
    
## Login to Azure Portal and verify the pre-deployed resources

1. Open Azure Portal from the desktop by double-clicking on it.
    
   ![](../media/azure-portal-edge.png)
   
1. On the **Sign into Microsoft Azure** tab, you will see the login screen, enter the following username, and, then click on **Next**.

   * **Email/Username**: <inject key="AzureAdUserEmail"></inject>

     ![](../media/user-email.png)
   
1. Now enter the following password and click on **Sign in**.
   
   * **Password**: <inject key="AzureAdUserPassword"></inject>
   
     ![](../media/user-pass.png "Enter Password")

1. If you see the pop-up Action Required, click **Ask Later**.

    ![](../media/asklater%20(1).png)

   >**NOTE:** Do not enable MFA, select **Ask Later**.

1. If you see the pop-up **Stay Signed in?**, click on **No**.

1. If you see the pop-up **You have free Azure Advisor recommendations!**, close the window to continue the lab.

1. If a **Welcome to Microsoft Azure** popup window appears, click **Cancel** to skip the tour.

1. Now you can see Azure Portal Dashboard, click on **Resource groups** from the Navigate panel to see the resource groups.

   ![](../media/select-rg.png)
 
1. We have already pre-deployed all the required resources, which you will be using throughout the lab.
 
## Support Contact
 
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:
- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Now, click on **Next** from the lower right corner to move on to the next page.

  ![](../media/n14.png)

### Happy Learning!!