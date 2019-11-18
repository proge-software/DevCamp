# Bots (.NET)

## Overview


## Objectives

In this hands-on lab, you will learn how to:

* Set up the developing environment to support the creation of bot applications.
* Create your own bot from scratch.
* Create your own bot using Azure Bot Service.
<!-- * Call Azure Cognitive Services to leverage computer vision API -->
* Hosting your bot in Azure.

## Prerequisites

<!-- * The source for the starter app is located in the [start](start) folder.
* The finished project is located in the [end](end) folder. -->
* Deployed the starter ARM Template [HOL 1](../01-developer-environment).
* Completion of the [HOL 5](../05-arm-cd).
* Visual Studio 2019

## Exercises

This hands-on-lab has the following exercises:

* [Exercise 1: Set up your environment](#ex1)
* [Exercise 2: Create an interactive dialog](#ex2)
* [Exercise 3: Integrate the API](#ex3)
* [Exercise 4: Send attachments to the bot](#ex4)
* [Exercise 5: Analyze submitted pictures automatically](#ex5)
* [Exercise 6: Host your bot in Azure](#ex6)
* [Exercise 7: Azure Bot Service](#ex7)
* [Exercise 8: Azure Functions Bot](#ex8)


## References

- [https://docs.microsoft.com/en-us/azure/bot-service/dotnet/bot-builder-dotnet-sdk-quickstart?view=azure-bot-service-4.0](https://docs.microsoft.com/en-us/azure/bot-service/dotnet/bot-builder-dotnet-sdk-quickstart?view=azure-bot-service-4.0)

---

## Exercise 1: Set up your environment<a name="ex1"></a>

1. Install Visual Studio 2019 if you did not

1. Open Visual Studio 2019 and click on `Continue without code`

    ![image](./media/07-01-01_VS2019_Startup.png)

1. In the top bar click open `Extensions` and then `Manage Extensions`

    ![image](./media/07-01-02_VS2019_Extensions.png)

1. In the form use the top-right box to search for `Bot Framework`, select `Bot Framework v4 SDK Templates for Visual Studio 2019` and then hit `Download`

    ![image](./media/07-01-03_VS2019_Extensions_BotFrameworkV4Templates.png)

1. When it finished, hit `Close` and close Visual Studio 2019

    ![image](./media/07-01-04_VS2019_Extensions_BotFrameworkV4Templates_CloseToInstall.png)

1. In the prompted dialog click on `Modify`

    ![image](./media/07-01-05_VS2019_Extensions_BotFrameworkV4Templates_Install.png)

1. When it finish hit `Close`

    ![image](./media/07-01-06_VS2019_Extensions_BotFrameworkV4Templates_Installed.png)

1. Click on this [link](https://github.com/microsoft/BotFramework-Emulator/releases/) to the `BotFramework-Emulator` releases page and download the latest.
   At the time of writing it is the `4.6.0`.

   ![image](./media/07-01-01_BotFramework-Emulator_Github_Releases.png)

1. Download the installer for the Operative System you are working with.
   In the image the release for Windows is highlighted.

   ![image](./media/07-01-08_BotFramework-Emulator_Github_Releases_Download.png)

1. Install the BotFramework-Emulator.


## Exercise 2: Create your first echo bot<a name="ex2"></a>

1. In the Visual Studio 2019 Startup hit `Create a new project`

    ![image](./media/07-02-01_VS2019_Startup_CreateProject.png)

1. Use the search box in the top of the dialog to search for `echo bot`, select the entry `Echo Bot (Bot Framework v4)`, and hit `Next`

    ![image](./media/07-02-02_VS2019_Startup_CreateProject_EchoBot)

1. Configure your project using as `Project Name` and `Solution Name` `MyFirstBot`, and as `Location` `C:\Projects\HOL7\`.
   Finally hit `Create` and wait for Visual Studio 2019 to create the project.

    ![image](./media/07-02-03_VS2019_Startup_CreateProject_ConfigureProject.png)

1. Run the Bot
    
    ![image](./media/07-02-04_VS2019_EchoBot_Run.png)

    > During the build and run processes it will ask you to configure SSL. Hit `Yes`
    >
    > ![image](./media/07-02-05_VS2019_EchoBot_Run_SSL.png)
    > 
    > A security warning will display: hit `Yes` again
    >
    > ![image](./media/07-02-05_VS2019_EchoBot_Run_SSL_SecurityWarning.png)


1. A new Chrome tab will be opened. Take note of the opened URL.

    ![image](./media/07-02-06_Chrome_EchoBot.png)

1. Open the BotFramework-Emulator and hit `Open Bot`

    ![image](./media/07-02-07_BFE.png)
    
1. Fill the form using the URL from the opened Chrome suffixed with `/api/messages` and finally hit connect

    ![image](./media/07-02-08_BFE_Connect.png)

1. The BotFramework-Emulator should connect to the Bot, which will welcome you!

    ![image](./media/07-02-09_BFE_Connected.png)

1. You can write anything to the bot and it will simply repeat your words. Try it!

    ![image](./media/07-02-10_BFE_Chatted.png)

## Exercise 3: Web App Echo Bot <a name="ex3"></a>

1. In Azure Portal open the resource group `Corso-MS-Cloud` and click on the `+ Add` button

    ![image](./media/07-03-01_Portal_Corso-MS-CLoud_Add.png)

1. Use the search box to search for and select `Web App Bot`

    ![image](./media/07-03-02_Portal_NewResource_WebAppBot.png)

1. Hit the button `Create`

    ![image](./media/07-03-03_Portal_NewResource_WebAppBot_Create.png)

1. Fill the form as in picture. For the name of the bot use your proge's mail prefix followed by the word `bot`.
   Finally hit `Create`

    ![image](./media/07-03-04_Portal_WebAppBot_Create.png)

1. In the overview of the created Web App Bot hit on the button `Browse`

    ![image](./media/07-03-05_Portal_WebAppBot_Browse.png)

1. A new tab of the browser will be opened and it will display a page similar to the one in the following picture

    ![image](./media/07-03-06_Portal_WebAppBot_Created.png)

1. Open the blade `Configuration` of the Web App Bot. Take note of the `MicrosoftAppId` and `MicrosoftAppPassword`

    ![image](./media/07-03-07_Portal_WebAppBot_Configuration.png)

1. In the BotFramework-Emulator click on the button `Open Bot`

    ![image](./media/07-03-08_BFE.png)

1. Fill the form with the url to the deployed bot, the `MicrosoftAppId` and the `MicrosoftAppPassword`

    ![image](./media/07-03-09_BFE_WebBot.png)

1. The BotFramework-Emulator will display an error related to the configuration of `ngrok`

    ![image](./media/07-03-10_BFE_WebBot_ngrok_error.png)

1. Download ngrok from [https://ngrok.com/download](https://ngrok.com/download).

    ![image](./media/07-03-11_BFE_WebBot_ngrok_download.png)

1. Unzip the downloaded zip file in the desktop and configure BotFramework-Emulator to use the `ngrok.exe` file in the Desktop and finally hit `Save`

    ![image](./media/07-03-12_BFE_WebBot_ngrok_configure.png)

1. Finally Restart the conversation 

    ![image](./media/07-03-13_BFE_WebBot_Chat.png)


## Exercise 4: Publish the Bot on Teams for testing <a name="ex4"></a>

1. In the `Corso-MS-Cloud` resource group open your bot and click on the `Channels` blade.
   Finally, hit the `Teams` button.

   ![image](./media/07-04-01_WebBot_Channels.png)

1. Click the `Save` Button

    ![image](./media/07-04-02_WebBot_Channels_Teams.png)

1. Tick the checkbox and click on the `Agree` button

    ![image](./media/07-04-03_WebBot_Channels_Teams_Agreements.png)

1. Click on the `Settings` blade and copy the `MicrosoftAppID`

    ![image](./media/07-04-04_WebBot_Settings_AppID.png)

1. Open `Teams` and paste the copied GUID in the searchbox on top of the window.
   Click on the `People` tab and you find the bot you published.

    ![image](./media/07-04-05_WebBot_Teams_Chat.png)


## Exercise 5: Analyze submitted pictures automatically<a name="ex5"></a>

## Exercise 6: Host your bot in Azure<a name="ex6"></a>

## Exercise 7: Azure Bot Service<a name="ex7"></a>

## Exercise 8: Azure Functions Bot<a name="ex8"></a>

## Summary

In this hands-on lab, you learned how to:

* Set up the developing environment to support the creation of bot applications.
* Create your own bot from scratch.
* Create your own bot using Azure Bot Service.
* Call Azure Cognitive Services to leverage Computer Vision API and Translator Text API.
* Hosting your bot in Azure and Azure Functions.

After completing this module, you can continue on to Module 9: IoT.

### View Module 9 instructions for [.NET](../11-IoT/)

---
Copyright 2018 Microsoft Corporation. All rights reserved. Except where otherwise noted, these materials are licensed under the terms of the MIT License. You may use them according to the license as is most appropriate for your project. The terms of this license can be found at <https://opensource.org/licenses/MIT>.