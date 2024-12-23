# Add your data for RAG with Azure OpenAI Service

### Overall Estimated Duration: 1 hour

## Overview

This lab explores the Azure OpenAI Service, where you'll provision the service, deploy a model, generate natural language output, and interact with the model using your own data. You'll also set up, configure, and run an application. By the end of this lab, you'll enhance your ability to create AI-driven applications with Azure.

## Objective

This lab provides hands-on experience with Azure OpenAI resources, including provisioning a resource, deploying a model, generating natural language output, and setting up, configuring, and running an application. By the end of this lab, you will be able to:

- **Explore content filters in Azure OpenAI:** This hands-on exercise demonstrates how to construct and maintain content filters in Azure OpenAI to control and refine generated outputs. Participants will learn about and implement content filters in Azure OpenAI to control and refine created material.

## Pre-requisites

- **Development Skills:** Basic programming knowledge and experience with APIs and SDKs.

- **AI Concepts:** Understanding prompt engineering, code development, and image generation using models such as DALL-E.

- **Content Management:** Understanding data integration for RAG and content filtering techniques.

## Architecture

The architecture leverages Azure OpenAI Service to provision resources, deploy models, and generate natural language output. It includes setting up, configuring, testing, and running an application, enabling AI-driven solutions with Azure’s scalability and security.

## Architecture Diagram

 ![](../media/lab7arc.JPG)

## Explanation of Components

The architecture for this lab involves the following key components:

- **Azure OpenAI Resource:** Provision an Azure OpenAI resource to access OpenAI’s advanced AI models, enabling integration with custom applications.

- **Model Deployment:** Deploy an OpenAI model to access and utilize its functionality for testing and application use cases.

- **Natural Language Output Generation:** Generate natural language output using the deployed model to process and understand data, enhancing the application’s capabilities.

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