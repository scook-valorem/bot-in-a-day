---
layout: page
title: ARM
permalink: arm.html
---

## Automated ARM Deployment

The deployment of intelligent resources in Azure can be automated in a manner similar to all other Azure resources. You can deploy simple Bot Services or complex solutions using a single JSON-based template.

### Setup the Cloud Shell

1. Navigate to the [Azure Portal](https://portal.azure.com).

1. Launch the **Cloud Shell** from the top navigation page of the Azure portal

	![](./media/shell-icon.png)

1. On the first launch of the **Cloud Shell** you will see various prompts to configure your shell environment. Configure the following options:

	- For shell type, select the **Bash (Linux)** option.

	- For storage, select your preferred subscription.

	- Click the **Configure** button.

1. Select the environment drop down from the left-hand side of the shell window

	![](./media/env-selector.png)

1. Select the **Bash** option.

### View Subscription Information in the Cloud Shell

You are automatically authenticated for the Azure CLI 2.0 in every session. We can use this to learn basic information about our subscription.

1. Run the following command in the **Cloud Shell** to view the list of subscriptions associated with your current identity:

	```
	az account list
	```

1. View the details of your currently selected Azure subscription:

	```
	az account show
	```

	> If you need to change the subscription, you can use the ``az account set --subscription my-subscription-name`` command.

1. View a list of [Resource Groups](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) in your subscription:

	```
	az group list
	```

### Deploy a Bot Service ARM Template using the Cloud Shell

We can now deploy a very simple Bot Service ARM Template (<https://github.com/azure-immersion/bot-in-a-day/blob/master/assets/bot.json>) using the Cloud Shell. We will then configure a Bot.

1. Create a new resource group named ``CapitalOneWITAutomation`` in your subscription:

	```
	az group create --name CapitalOneWITAutomation --location "East US"
	```

1. Deploy an example ARM template that creates a simple [Bot Service](https://azure.microsoft.com/en-us/services/bot-service/) instance using a *consumption plan*:

	```
	az group deployment create --resource-group CapitalOneWITAutomation --template-uri https://raw.githubusercontent.com/azure-immersion/bot-in-a-day/master/assets/bot.json
	```

1. The ARM Template deployment will begin. This deployment can take 3-5 minutes. Wait for the deployment to complete before moving on with the exercise.

1. Click the **Resource groups** link in the Azure Portal navigation bar.

	> If you don't see this link, click the **More services** link and search for the **Resource groups** link. You can click the *star* icon to pin this link to your navigation bar.

1. Select the **CapitalOneWITAutomation** resource group.

1. Select the **Bot Sevice** created using the ARM template.

1. On the **Bot Service** blade, choose the programming language that you want to use to develop your bot. For this tutorial, choose the **C#** language.

1. Select the template to use as the starting point for developing your bot. For this tutorial, choose the **Basic** template.

1. Click **Next** to create the bot based on the programming language and template that you've chosen.

1. Click **Create Microsoft App ID and password**.  

1. On the page that opens in a new browser tab, record the **App name** and **App ID** values.

1. Click **Generate an app password to continue**.

1. Copy and securely store the password that is shown, and then click **Ok**.

1. Click **Finish and go back to Bot Framework**.

1. Back in the Azure Portal, assure the **App ID** field is auto-populated for you, and paste the password that you copied (in step 3 above) into the password field.

1. Agree to terms, and then click **Create bot**.

### Obtain your LUIS App Programmatic Key

Now, we can obtain your LUIS key to use in a future ARM template.

1. In your browser, navigate to <https://www.luis.ai/user/settings>.

	> You can also get to this page by clicking your name in the top-right corner of the LUIS portal.

1. Sign in if you are not already authenticated.

	> If you see the **LUIS Welcome Page**, you can safely skip this page.

1. Record the value of your **Programmatic Key**.

### Deploy a Cortana Intelligence Suite ARM Template using the Cloud Shell

We can finally create a more complex Cortana Intelligence Suite ARM Template (<https://github.com/azure-immersion/bot-in-a-day/blob/master/assets/cortana.json>) using the Cloud Shell. To accomplish this, we will need the **App Id** and **App Password** from the **Bot Service** we have just created and we will also need a **Management Key** from a new **LUIS** app.

1. Deploy the advanced ARM Template to our existing resource group:

	```
	az group deployment create --resource-group CapitalOneWITAutomation --template-uri https://raw.githubusercontent.com/azure-immersion/bot-in-a-day/master/assets/cortana.json
	```

1. You will be prompted to provide various ARM Template parameter values including:

	- **app-id**: Use the **App Id** field from your Bot.

	- **app-password**: Use the **App Password** field from your Bot.

	- **luis-management-key**: Use the **Programmatic Key** field from your LUIS account.

1. The ARM Template deployment will begin. This deployment can take 10-12 minutes. Wait for the deployment to complete before moving on with the exercise.

1. Click the **Resource groups** link in the Azure Portal navigation bar and select the **CapitalOneWITComplex** resource group.

1. View the various resources deployed as part of this ARM template.

> **Up Next**: [Cleanup your Azure Subscription](cleanup.html)
