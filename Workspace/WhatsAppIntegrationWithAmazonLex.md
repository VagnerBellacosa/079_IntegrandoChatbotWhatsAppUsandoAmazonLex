# WhatsApp Integration with Amazon Lex

[![Sachin Sapkale](https://miro.medium.com/fit/c/56/56/0*a65F4SaPCn1j46h9.jpg)](https://medium.com/@sachin.sapkale?source=post_page-----3b852adb0fd1-----------------------------------)

[Sachin Sapkale](https://medium.com/@sachin.sapkale?source=post_page-----3b852adb0fd1-----------------------------------)

[Aug 16, 2020·4 min read](https://medium.com/@sachin.sapkale/whatsapp-integration-with-amazon-lex-3b852adb0fd1?source=post_page-----3b852adb0fd1-----------------------------------)







Recently I came across an article that demonstrates using Amazon Lex bot with Messaging Service, but it lacked integration with WhatsApp(Ref: https://aws.amazon.com/blogs/machine-learning/integrate-your-amazon-lex-bot-with-any-messaging-service/). So, I thought it would be a good idea to create a small article that can be built using this article and still demonstrate WhatsApp + Amazon Lex based ChatBot.

Well, How do we Start? So, I thought to start with…..

# Setting-up Twilio account for SMS and WhatsApp messages

Twilio provides a trial account, So, I signed up for an account (REF: https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account). I got myself registered by following these instructions.

All I ensured was to save Account SID, and Auth Token for ready reference later. They will be required later for setup.

Twilio allows you to leverage WhatsApp Sandbox, I thought of using the same for this demo.

# Setup Amazon Lex Sample (BookTrip) Bot

I thought of setting up environment on my laptop first. (Ref: [Installing Node.js](https://nodejs.org/)), Then I realized, my home laptop already had it.

So, I quickly grabbed my laptop and got existing Sample(BookTrip) setup using Amazon Lex console.

![Screenshot from Amazon Lex console to setup BookTrip bot](https://miro.medium.com/max/60/1*8WDB6yBQDi2tkThu_pBRMA.png?q=20)

![Screenshot from Amazon Lex console to setup BookTrip bot](https://miro.medium.com/max/630/1*8WDB6yBQDi2tkThu_pBRMA.png)

Amazon Lex console to setup BookTrip bot

I followed the steps mentioned in article to setup Sample Amazon Lex bot and to publish it as well.

## QuickReference to setup Amazon Lex Chatbot

1. Login to [Amazon Lex Console](https://console.aws.amazon.com/lex/home), and Choose **Create** in the bots
2. Choose the **BookTrip** sample, note the name of the AWS Identity and Access Management (IAM) role, and choose **Create**.
3. After Amazon Lex builds the bot, test it in the console.
4. Publish the bot. For the Alias, use **devtest**.

Yes, We have a functional Bot now.

# Setup Amazon Lex Channel for WhatsApp

We will establish a channel between Twilio and Amazon Lex, using the Twilio SMS channel. How do you go about it? here is how.

1. Login to [Amazon Lex console](https://ap-southeast-1.console.aws.amazon.com/lex/home)
2. This will list the bots created. Click on hyperlink of recently created “**BookTrip**” bot.

![img](https://miro.medium.com/max/60/1*qGIm6520OzAktEkTka657g.png?q=20)

![img](https://miro.medium.com/max/630/1*qGIm6520OzAktEkTka657g.png)

Amazon Lex console showing “BookTrip” bot

\3. This leads to a screen that allows you to create and configure bot. It shows multiple tabs like “Editor”, “Settings” , “Channels” and “Monitoring”. We will be selecting **“Channels”** tab.

\4. Left hand side will show a pane with list of available channels. We will select **“Twilio SMS” channel** in context of this article. This will show a Twilio channel configuration page, like one below.

![img](https://miro.medium.com/max/60/1*mOVezWrykDk0E1YgUoONxA.png?q=20)

![img](https://miro.medium.com/max/630/1*mOVezWrykDk0E1YgUoONxA.png)

Amazon Lex console showing Twilio SMS Channel configuration page

\5. I proceeded quickly with adding channel name, a brief description, IAM Role (default value), KMS Key (Default value), Alias (used latest published version of bot). I added Twilio Account SID & Auth Token that was saved earlier. Click on **“Activate”** button.

![img](https://miro.medium.com/max/60/1*drXgg20t-j01hzRiAhLtVw.png?q=20)

![img](https://miro.medium.com/max/630/1*drXgg20t-j01hzRiAhLtVw.png)

Activate button at the bottom of the page

This generates an Endpoint URL, that we will require to configure Twilio WhatsApp Sandbox. after all we want to leverage WhatsApp as interface for this Bot :).

# Finally, Integrate Amazon Lex Bot’s Twilio SMS Channel with Twilio WhatsApp Sandbox

1. Login to [Twilio console](https://www.twilio.com/console)
2. Navigate to [WhatsApp sandbox](https://www.twilio.com/console/sms/whatsapp/learn) console

![img](https://miro.medium.com/max/60/1*mTmGfVL77dGCRHktrx7hgw.png?q=20)

![img](https://miro.medium.com/max/630/1*mTmGfVL77dGCRHktrx7hgw.png)

Twilio WhatsApp Sandbox

\3. Join the WhatsApp sandbox, by sending a WhatsApp message “join fully-tomorrow” to mentioned phone. Twilio Sandbox will respond with a message confirming enabling sandbox.

Awesome, you can now send WhatsApp messages on this chat and get response. Just s few steps away from completion…..

\4. Navigate to Twilio [sandbox](https://www.twilio.com/console/sms/whatsapp/sandbox) configuration, by clicking “**Settings**” and then “**WhatsApp Sandbox settings**”.

![img](https://miro.medium.com/max/60/1*clhO7LXiK3vTx62lVpreYA.png?q=20)

![img](https://miro.medium.com/max/630/1*clhO7LXiK3vTx62lVpreYA.png)

Twilio Sandbox Integration with Amazon Lex Bot

\5. Paste the Endpoint URL from previous section in “WHEN A MESSAGE COMES IN” textbox and save the settings.

Voila!!!! We are done with the configuration. We need to now test.

# Testing the Setup via WhatsApp

I had tested it with my phone and below is the screenshot of results.

![img](https://miro.medium.com/max/28/1*oQkKs2gH2pSC1GdSsyEbHQ.jpeg?q=20)

![img](https://miro.medium.com/max/531/1*oQkKs2gH2pSC1GdSsyEbHQ.jpeg)

Bot execution results from my mobile using WhatsApp

This actually opens up a lot of other options for several applications knowing the usage of WhatsApp.

Thatz, all guys. Hope you find something interesting and useful. Until next blog, Namaskar. Till we meet again. :)