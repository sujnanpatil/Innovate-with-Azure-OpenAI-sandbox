# Exercise 5: Azure OpenAI + NLP using ChatGPT on SQL Engine

This exercise illuminates the path of setting up an Azure Function/Web App, fortifying API keys, and seamlessly integrating ChatGPT to effortlessly transform user queries into powerful SQL commands for advanced data analysis. 

## Lab scenario
Contoso aims to enhance its analytics capabilities by integrating Azure SQL Database with OpenAI's ChatGPT for natural language processing. In this lab, Contoso's team will set up an Azure Function/Web App, securely manage API keys, and utilize ChatGPT to convert user queries into SQL, executing advanced analytics on the Azure SQL Database.

## Lab objectives
In this lab, you will complete the following:

- Open AI Setup and Installation of Application  
- Quick Start With Hosted Demo Application.
   
## Overview of the application
This application demonstrates the of Open AI (ChatGPT/GPT-4) to help answer business questions by performing advanced data analytic tasks on a business database. Examples of questions are:

 * Simple: Show me daily revenue trends in 2016 per region
 * More difficult: Is that true that the top 20% of customers generate 80% of revenue in 2016?
 * Advanced: Forecast monthly revenue for the next 12 months starting from June-2018

The application supports Python's built-in SQLite as well as your own Microsoft SQL Server.

## Task 1: Review Open AI resource

1. Naviagte back to [Azure portal](http://portal.azure.com/), search and select **Azure OpenAI**, from the **Azure AI Services | Azure OpenAI pane**, select the **OpenAI-<inject key="Deployment ID" enableCopy="false"/>**.

1. Now select **Keys and Endpoints** **(1)** under Resource Management and click on **Show Keys** **(2)**. Copy the **KEY 1** **(3)** and **Endpoint** **(4)**, and store them in a text file for later use.

   ![](media/update4.png)
      
## Task 2: Deploy the application to Azure

1. In the LabVM, open **File Explorer** naviagte to the `C:\LabFiles\OpenAIWorkshop-Automation\scenarios\incubations\automating_analytics` **(1)** path, right click on **app.py (2)**, and select **Open with Code (3)**. Take a look at the code to see how it works.

   ![](media/file-select.png "Azure OpenAI")

   - The provided code is a Streamlit application that consists of two main components: a SQL Query Writing Assistant and a Data Analysis Assistant. The application allows you to interact with an SQL database and perform various tasks.

   - The code begins with importing necessary libraries and dependencies such as Streamlit, Pandas, NumPy, Plotly, and others. It also imports custom modules like AnalyzeGPT, SQL_Query, and ChatGPT_Handler.

2. In the code snippet, you can configure Azure OpenAI deployment settings and optional SQL Server settings. It provides input fields for entering deployment names, endpoints, API keys, and SQL Server details. With Streamlit, you can save settings and customize the application's functionality. Settings allow you to customize the application's behavior based on your specific needs, enhancing the overall experience.

   ![](media/code01.png "Azure OpenAI")

3. The code snippet creates a chat interface using two GPT models, "ChatGPT" and "GPT-4". There are various models to choose from, FAQs specific to each model, and a form to ask questions. Moreover, the code includes options for showing the code and prompts, allowing you to interact with the chat interface more easily.

   ![](media/code02.png "Azure OpenAI")

4. There is a "Submit" button in the code snippet that triggers a series of checks and actions. It verifies that the necessary deployment settings and SQL server settings are provided. If all requirements are met, it creates an SQL query tool and an analyzer object. To run queries and display results, it uses different methods based on the index value.

   ![](media/code03.png "Azure OpenAI")   
      
5. In the LabVM, navigate to Desktop and search for `cmd` in the search box then click on **Command Prompt**.

6. Run the below command to change the directory.

   ```bash
   cd C:\LabFiles\OpenAIWorkshop-Automation
   ```

7. Run the below command to **Authenticate with Azure**. It will redirect to Azure authorize website, Select your account.

   ```bash
   azd auth login
   ```

8. Run the below command to setup the resource group deployment and **Create a new environment**. Make sure to replace `{DeploymentId}` with **<inject key="Deployment ID" enableCopy="true"/>** in the below command.

   ```bash
   azd config set alpha.resourceGroupDeployments on
   ```
   
   ```bash
   azd env new sql-chat-gpt-{DeploymentId}
   ```

9. Run the below command to Provision Azure resources, and deploy your project with a single command.

   ```bash
   azd up
   ```

10. Please select your Azure Subscription to use, enter `1` and click on the **Enter** button.

      ![](media/app-sub.png "Azure OpenAI")

11. Please select an Azure location to use, select the location as **<inject key="Region" enableCopy="false"/>** location, and click on the **Enter** button. You can change the location using the up and down arrow.

      ![](media/app-location.png "Azure OpenAI")

12. Please select Resource Group to use, select the Resource Group as OpenAI, and click on the **Enter** button. You can change the Resource Group using the up and down arrow.

       ![](media/img0011.png "Azure OpenAI")
   

13. Once the deployment succeeded, you will see the following message **SUCCESS: Your application was provisioned and deployed to Azure**. The deployment might take 5 - 10 minutes. It is producing a web package file, then creating the resource and publishing the package to the app service.

      ![](media/app-deployment-output.png "Azure OpenAI")

14. Navigate back to the Azure portal, search and select **App service**. Select the available web app that you have deployed in the previous step.

      ![](media/app-service-select.png "Azure OpenAI")

15. Next, click on **Browse** to open your Web application.

      ![](media/webapp.png "Azure OpenAI")
      
      ![](media/webapp1.png "Azure OpenAI")

16. Click the **Next** button located in the bottom right corner of this lab guide to continue with the next exercise.

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
  > - Navigate to the Lab Validation tab, from the upper right corner in the lab guide section.
  > - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at labs-support@spektrasystems.com.

## Task 3: Analyzing Data Analysis Assistant and SQL Query Writing Assistant

1. When you're on the **Natural Language Query** page, click on **Settings (1)** from the left side menu. Enter **ChatGPT deployment name** as **gpt-35-turbo-16k(2)**, enter **GPT-4 deployment name** as **gpt-35-turbo-16k (3)**, enter **Azure OpenAI Endpoint** as **Endpoint (4)** which you have saved in previous task, and **Azure OpenAI Key** as **Key (5)** which you have saved in previous task have all been filled in. Click on **Submit(6)** to save the changes.

    ![](media/img0010.png "Natural Language Query")

2. On the Natural Language Query page, select **SQL Query Writing Assistant (1)** from the left-side menu, from the **GPT model**, select **ChatGPT (2)**,  change the **FAQs** from the drop-down menu to select **Show me revenue by-product in ascending order (3)**, and and click on **Submit (4)**. According to the query, the **Output (5)** will be displayed. 

    ![](media/nl-01.png "Natural Language Query")
    
3. On the **Natural Language Query** page, on the left side menu, change the **FAQs** from the drop-down menu to select **Show me top 10 most expensive products (1)**, and click on **Submit (2)**. According to the query, the **Output (3)** will be displayed.

    ![](media/nl-02.png "Natural Language Query")

4. On the **Natural Language Query** page, on the left side menu, change the **FAQs** from the drop-down menu to select **Show me net revenue by year. Revenue time is based on the shipped date. (1)**, and click on **Submit (2)**. According to the query, the **Output (3)** will be displayed.

    ![](media/nl-03.png "Natural Language Query")

5. The dropdown menu allows you to browse the rest of the **FAQs** by changing the Input value.

## Review

In this exercise, you have accomplished the following:
- Connected Azure SQL Database with ChatGPT for easier language processing.
- Ensured strong security for API keys and data protection.

## Proceed to Exercise 6
  
   
