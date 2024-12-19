# Get Started With OpenAI And Build Natural Language Solution

### Overall Estimated Duration: 4 Hours

## Overview

Azure OpenAI Service brings the generative AI models developed by OpenAI to the Azure platform, enabling the development of powerful AI solutions with the security, scalability, and integration of Azure's cloud services. In this lab, you'll learn to provision Azure OpenAI as a resource and use Azure OpenAI Studio to deploy and explore OpenAI models. With Azure OpenAI, developers can create applications like chatbots and language models that excel in understanding natural human language. The service provides access to pre-trained AI models and a suite of APIs and tools for customizing and fine-tuning these models to meet specific application requirements. In this scenario, you'll assume the role of a software developer tasked with implementing an app to provide hiking recommendations using generative AI, demonstrating techniques applicable to any app utilizing Azure OpenAI APIs.

## Objective

By the end of this lab, you will be able to:

- **Get started with Azure OpenAI Service**: This hands-on exercise aims to provision an Azure OpenAI resource and deploying a model. Explore the model's capabilities in the Completions playground, then interact with it using the Chat playground. Fine-tune responses by adjusting prompts and parameters, and leverage code-generation to automate tasks.
- **Use Azure OpenAI SDKs in your app**: This hands-on exercise aims to provision an Azure OpenAI resource, deploy a model, set up and configure an application in Cloud Shell, and then run the application, demonstrating the full lifecycle from resource creation to application deployment and execution.

## Pre-requisites

- Familiarity with Azure OpenAI Service, Azure CLI, and REST APIs
- Basic understanding of AI and machine learning concepts

## Architecture

The architecture flow for this task begins with provisioning an Azure OpenAI resource within your Azure subscription and deploying a pre-trained model using Azure OpenAI Studio. Next, you'll explore the model's capabilities in the Completions playground and test its conversational abilities in the Chat playground, experimenting with different prompts and parameters to customize responses. You'll also investigate the model's code-generation capabilities. In the application development phase, you'll set up your application environment in Azure Cloud Shell, configure the application to integrate with the deployed OpenAI model, and finally, run the application to provide hiking recommendations using generative AI.

## Architecture Diagram

 ![Access Your VM and Lab Guide](../media/arch20.png)

## Explanation of Components

1. **Azure OpenAI**: Azure OpenAI Service provides REST API access to OpenAI's powerful language models and these models integrates with your data, enabling customized and secure interactions.
1. **Azure OpenAI Models**: Offers pre-trained and customizable large language models for various AI applications. These models allow for powerful AI-driven solutions by generating tailored and contextually relevant content based on well-crafted prompts.
1. **Azure CloudShell**: Azure CloudShell offers an integrated, browser-based shell experience for managing Azure resources. It provides a ready-to-use environment with pre-installed tools and access to both Bash and PowerShell.

## Getting Started with the Lab
 
## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and lab guide will be right at your fingertips within your web browser.
 
![Access Your VM and Lab Guide](../media/labguide-1.png)

### Virtual Machine & Lab Guide
 
Your virtual machine is your workhorse throughout the workshop. The lab guide is your roadmap to success.
 
## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.
 
![Explore Lab Resources](../media/env-1.png)
 
## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the Top right corner.
 
![Use the Split Window Feature](../media/spl.png)
 
## Managing Your Virtual Machine
 
Feel free to start, stop, or restart your virtual machine as needed from the **Resources** tab. Your experience is in your hands!
 
![Manage Your Virtual Machine](../media/res.png)

## **Lab Duration Extension**

1. To extend the duration of the lab, kindly click the **Hourglass** icon in the top right corner of the lab environment. 

    ![Manage Your Virtual Machine](../media/gext.png)

    >**Note:** You will get the **Hourglass** icon when 10 minutes are remaining in the lab.

2. Click **OK** to extend your lab duration.
 
   ![Manage Your Virtual Machine](../media/gext2.png)

3. If you have not extended the duration prior to when the lab is about to end, a pop-up will appear, giving you the option to extend. Click **OK** to proceed.

## Lab Guide Zoom In/Zoom Out

1. To adjust the zoom level for the environment page, click the **A↕ : 100%** icon located next to the timer in the lab environment.

   ![Manage Your Virtual Machine](../media/labzoom-1.png)

## Let's Get Started with Azure Portal
 
1. On your virtual machine, click on the Azure Portal icon as shown below:
 
   ![Launch Azure Portal](../media/sc900-image(1).png)
 
2. You'll see the **Sign into Microsoft Azure** tab. Here, enter your credentials:
 
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>
 
       ![Enter Your Username](../media/sc900-image-1.png)
 
3. Next, provide your password:
 
   - **Password:** <inject key="AzureAdUserPassword"></inject>
 
       ![Enter Your Password](../media/sc900-image-2.png)
 
4. If prompted to stay signed in, you can click "No."
 
5. If a **Welcome to Microsoft Azure** pop-up window appears, simply click **Cancel** to skip the tour.
 
6. Click "Next" from the bottom right corner to embark on your Lab journey!
 
     ![Start Your Azure Journey](../media/sc900-image(3).png)
 
This lab will equip you with the skills to deploy and customize Azure OpenAI models, enabling you to create advanced AI applications like chatbots and recommendation systems.

## Support Contact

The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:

- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Now, click on Next from the lower right corner to move on to the next page.

## Happy Learning!!
