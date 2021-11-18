# AWS Lex Weather Bot for Beginners from Design to WhatsApp Deployment

[![Shammy Narayanan](https://miro.medium.com/fit/c/96/96/0*bOOCuUC4njjdcB0-.)](https://shammy-n.medium.com/?source=post_page-----65f6e050f07f-----------------------------------)

[Shammy Narayanan](https://shammy-n.medium.com/?source=post_page-----65f6e050f07f-----------------------------------)Follow

[Nov 18, 2020](https://chatbotslife.com/weather-bot-for-beginners-using-lex-from-design-to-whatsapp-deployment-65f6e050f07f?source=post_page-----65f6e050f07f-----------------------------------) · 6 min read













[Chatbots](https://chatbotslife.com/) had been a gateway for most of the beginners into the world of AI, its simplicity and a trove of easily conceivable use-cases had made it tremendously popular in the developer community. Though my personal favorite had been open source RASA chatbots and previously had made few [popular videos](https://youtu.be/7LdN3cA6WOg) and [curated blogs on RASA chatbots](https://chatbotslife.com/common-mistakes-in-rasa-chatbot-environment-setup-design-part-2-of-3-ee3cdee24681), the most challenging part in it is the frequent and dynamic design transformations making the learning curve too steep. Fundamentally a good amount of effort gets expended in Learn-Unlearn and Relearn process. So stepping out of my comfort zone wanted to design and deploy a [chatbot](https://chatbotslife.com/what-is-a-chatbot-an-introduction-to-the-newest-tech-trend-cc668ebe886c) in AWS and compare these two systems in terms of ease of use as well as usability. Had taken a familiar example of a weather [bot](https://chatbotslife.com/what-is-a-chatbot-an-introduction-to-the-newest-tech-trend-cc668ebe886c) and developed it from scratch in Lex.

![img](https://miro.medium.com/max/1400/0*FnAy0druYDwM98zU.png)

As a first step, log in to AWS cloud, and from the management console, select LEX, you will land on a similar screen

![img](https://miro.medium.com/max/60/1*i8OImaBplDuAW14VQMwFUg.png?q=20)

![img](https://miro.medium.com/max/700/1*i8OImaBplDuAW14VQMwFUg.png)

Hit create and provide a name for your bot (in my case it's WeatherBot), once inside the panel we need to create Intents and utterances. For starters, **intent** refers to the goal the customer has in mind when typing in a question. Utterances are various ways they can ask that questions, for example, if “Greet” is an intent, utterances can be “Hi”, “Greetings”, etc

![img](https://miro.medium.com/max/60/1*imzxiDHMYdO9ICL8MVG6FQ.png?q=20)

![img](https://miro.medium.com/max/700/1*imzxiDHMYdO9ICL8MVG6FQ.png)

# Trending Bot Articles:

> [1.Understanding DialogFlow ES and CX](https://chatbotslife.com/dialogflow-es-and-cx-b32b450b2d50)
>
> [2.Deploying Transformer Models](https://chatbotslife.com/deploying-transformer-models-1350876016f)
>
> [3.TensorFlow installation with GPU Support on Python 3.7 in Windows](https://chatbotslife.com/tensorflow-installation-with-gpu-support-on-python-3-7-in-windows-734e6eeefa94)
>
> [4.Conversation Designers: who are they and what do they do?](https://chatbotslife.com/conversation-designers-who-are-they-and-what-do-they-do-8325e527625c)

As a chatbot architect or designer, for a superlative user experience, the efforts should be more focused on generating as many utterances and emulating customer natural way of interaction than the technical considerations.

In my chatbot, I have kept it simple with four intents (Greet, Good Bye, InquireWeather, and Weather inquiry). Out of this “Goodbye intent” is part of a few inbuilt intents which come as part of Lex boutique to simplify the development process. However, Lex allows you to append user-defined responses to such inbuilt intents

![img](https://miro.medium.com/max/2000/1*pzQ-Gg_Xv_XtOjqj9e937Q.png)

![img](https://miro.medium.com/max/1400/1*whAKmcvdFdhjCNk6xcoUMQ.png)

On Slots (variables in your utterances) Lex scores high as it comes with inbuilt enumerations or lists which cuts down your development work. For example, US_State is an in-built list that validates user inputs against 50 US states. Similar validation in RASA would require us to write our own API and perform the validation (hopefully in future versions of open source Bots it may get integrated !!)

![img](https://miro.medium.com/max/1400/1*NNz89Z6dWZ7jjzlb92VC3g.png)

Will leave it to your imagination for designing the number of Intents and its utterances. But there comes a point in your design where we need to interact with an External Datastore, in our Weatherbot we will make use of the Weatherstack website which offers a free API for providing weather information for any given city

![img](https://miro.medium.com/max/60/1*IlKRBlIxmas1AWhcDK_61A.png?q=20)

![img](https://miro.medium.com/max/700/1*IlKRBlIxmas1AWhcDK_61A.png)

Sign in to it and get the API key, we will need it in the fulfillment event.

The next big challenge is to establish the connection from our chatbot to this API to retrieve the weather details for the user-provided city. We accomplish this goal using the AWS lambda function (you can code in Ruby, Java, Python and this list keeps growing…)

![img](https://miro.medium.com/max/60/1*IlX9vbH7BhkHxsRccdurzg.png?q=20)

![img](https://miro.medium.com/max/700/1*IlX9vbH7BhkHxsRccdurzg.png)

Sample Python code to retrieve and communicate response back to Lex

![img](https://miro.medium.com/max/60/1*aQeZwKouEis7doZ5ogXn3w.png?q=20)

![img](https://miro.medium.com/max/700/1*aQeZwKouEis7doZ5ogXn3w.png)

This code is available in https://github.com/shammy45/LexChatbot/blob/main/weatherapi

In the above code snippet Input variable “**City**” comes from the slot of your chatbot utterances

![img](https://miro.medium.com/max/60/1*yhcHgLex2K6R_Rdt5QvFjw.png?q=20)

![img](https://miro.medium.com/max/700/1*yhcHgLex2K6R_Rdt5QvFjw.png)

Once your bot is developed, the remaining phases are Testing and Deployment.

Testing can be done in your local environment on the test pane at the right side of the Lex console

![img](https://miro.medium.com/max/60/1*xVfvWMhTpHsZZO8n7GO05A.png?q=20)

![img](https://miro.medium.com/max/658/1*xVfvWMhTpHsZZO8n7GO05A.png)

If the city name is not provided, Bot follows a different interaction

![img](https://miro.medium.com/max/60/1*qxfMmjVbDEaZeDT1ybIRpA.png?q=20)

![img](https://miro.medium.com/max/680/1*qxfMmjVbDEaZeDT1ybIRpA.png)

With our testing completed, the final stage is deployment. Lex provides an out of box integration with multiple channels as shown below

![img](https://miro.medium.com/max/60/1*lRCBVn1Tsln0zsS54DB8mA.png?q=20)

![img](https://miro.medium.com/max/265/1*lRCBVn1Tsln0zsS54DB8mA.png)

We will use the Twillio option to integrate with the popular messaging platform -Whatsapp

![img](https://miro.medium.com/max/60/1*a49Sou5gbBEdrpgDaAgZNA.png?q=20)

![img](https://miro.medium.com/max/700/1*a49Sou5gbBEdrpgDaAgZNA.png)

once you have signed in and completed your two-factor authentication, select WhatsApp sandbox setting under Programmable messaging (as shown in picture)

![img](https://miro.medium.com/max/60/1*V96eG-vInA9O7YOAawycwQ.png?q=20)

![img](https://miro.medium.com/max/560/1*V96eG-vInA9O7YOAawycwQ.png)

![img](https://miro.medium.com/max/60/1*xxZ5Pvd8LhHlKC0yKIs7eg.png?q=20)

![img](https://miro.medium.com/max/700/1*xxZ5Pvd8LhHlKC0yKIs7eg.png)

In the “When A Message Comes In” and the “Status Callback URL” textboxes, we have to provide a callback webhook URL from our Lex chatbot. So we need to generate it from the Integration panel of the Lex console

![img](https://miro.medium.com/max/60/1*N2AW1oGFLIO_glWhV-t2Pw.png?q=20)

![img](https://miro.medium.com/max/700/1*N2AW1oGFLIO_glWhV-t2Pw.png)

Alias and Account SID information will be available from your Twilio console as shown in below pic

![img](https://miro.medium.com/max/60/1*U0Pt2HT8zcMeXicoUc0FJg.png?q=20)

![img](https://miro.medium.com/max/700/1*U0Pt2HT8zcMeXicoUc0FJg.png)

On clicking activate in the Chatbot channel panel, you will get a call back URL from the LEX panel as shown below

![img](https://miro.medium.com/max/60/1*CTv0wjKgzKTZ-e_h4Piw3Q.png?q=20)

![img](https://miro.medium.com/max/700/1*CTv0wjKgzKTZ-e_h4Piw3Q.png)

Use this URL to populate the WhatsApp sandbox screen

![img](https://miro.medium.com/max/60/1*HO4ACjEi-u9VhYZotirc7Q.png?q=20)

![img](https://miro.medium.com/max/700/1*HO4ACjEi-u9VhYZotirc7Q.png)

You are all set now, follow the instruction on your screen to initiate chatbot in WhatsApp

![img](https://miro.medium.com/max/60/1*rcSQpEvYtg9pwLEqHS6wcQ.png?q=20)

![img](https://miro.medium.com/max/700/1*rcSQpEvYtg9pwLEqHS6wcQ.png)

Now you are all set to interact with your weather bot from your WhatsApp

![img](https://miro.medium.com/max/34/1*nzIGq4C4u0H5KVVPrJfZtQ.jpeg?q=20)

![img](https://miro.medium.com/max/700/1*nzIGq4C4u0H5KVVPrJfZtQ.jpeg)

In conclusion, comparing RASA, Lex significantly cuts down the effort and time in “Designing to deployment cycle” of a chatbot, also the environment comes with multiple benefits and flexibilities (choice of program languages, Inbuilt intents, zero lead time to setup environment, out of box integration on popular platform, Serverless, etc) but we also need to remember all this comes with a vendor lockin. Decision is purely based on Lockin vs Learning curve…and our Chatbot journey continues.

# Don’t forget to give us your 👏