# ChatGPT_Conversational_AI
ChatGPT-Powered NPC Application 

1. Introduction
This is the documentation for the ChatGPT-powered NPC that effectively utilizes ChatGPT at runtime in Unity! This document will guide you through the process of creating and integrating a Non-Playable Character (NPC) powered by ChatGPT. With ChatGPT, our NPC will be capable of engaging in dynamic and interactive conversations with players, enhancing the overall user experience in your Unity game.
2. Prerequisites
Before you proceed, make sure you have the following prerequisites set up:
1.	Unity: Ensure you have the latest version of Unity installed on your system.
2.	Basic Unity knowledge: Familiarity with Unity's interface and scripting is beneficial.
3.	OpenAI GPT-3 API: Obtain access to the OpenAI GPT-3 API, which powers ChatGPT. You'll need an API key and organization ID to interact with the language model.

3. Setting Up the Project
1.	Creating a new Unity project.
2.	Setting up the necessary scenes, characters, and environment for your game. This project focuses on implementing the ChatGPT-powered NPC, assuming having the base setup in place.

4. Integrating ChatGPT into Unity
To integrate ChatGPT into our Unity project, we'll need a way to communicate with the GPT-3.5 API. For this purpose, we can use a C# wrapper that handles API requests. In this example, we'll use the popular " OpenAI Unity Package" package.

4.1 OpenAI Unity Package
An Unity package that allows you to use the OpenAI API at runtime in the Unity game engine.

4.2 How To Use the Package 
Importing the Package
To import the package, follow these steps:

1.	Open Unity 2019 or later
2.	Go to Window > Package Manager
3.	Click the + button and select Add package from git URL
4.	Paste the repository URL https://github.com/srcnalt/OpenAI-Unity.git and click Add

4.3 Setting Up Your OpenAI Account
To use the OpenAI API, you need to have an OpenAI account. Follow these steps to create an account and generate an API key:
1.	Go to https://openai.com/api and sign up for an account
2.	Once you have created an account, go to https://beta.openai.com/account/api-keys
3.	Create a new secret key and save it
4.	Saving Your Credentials
To make requests to the OpenAI API, we need to use our API key and organization name (if applicable). To avoid exposing our API key in your Unity project, we can save it in your device's local storage.
1.	To do this, follow these steps:
2.	Create a folder called .openai in your home directory (e.g. C:User\UserName\ for Windows or ~\ for Linux or Mac)
3.	Create a file called auth.json in the .openai folder
4.	Add an api_key field and a organization field (if applicable) to the auth.json file and save it
Here is an example of what our auth.json file should look like:

 
We can also pass our API key into OpenAIApi  when creating an instance of it but again, this is not recommended as anyone with the code can see our API key.

 

Our API key is a secret. Do not share it with others or expose it in any client-side code (e.g. browsers, apps). If you are using OpenAI for production, make sure to run it on the server side, where your API key can be securely loaded from an environment variable or key management service.


5. Create a ChatGPT Script to Make Requests to OpenAPI
1.	Create a new C# script named "ChatGPTController.cs."
2.	Implemented the necessary logic to handle API requests and responses. Ensure to handle API authentication using our credentials.

We can use the OpenAIApi class to make async requests to the OpenAI API.
All methods are asynchronous and can be accessed directly from an instance of the OpenAIApi class.
Here is an example of how to make a request:
 
    
To make a stream request, we can use the CreateCompletionAsync and CreateChatCompletionAsync methods. These methods are going to set Stream property of the request to true and return responses through an onResponse callback. In this case text responses are stored in Delta property of the Choices field in the Chat Completion.
 

6. NPC Dialogue UI
 Designed a user interface (UI) for the NPC's dialogue. It should display the NPC's responses and offer a text box for the player to enter their input.
 

7. Run the game and Ask about anything to our game character:
-Character will make the API calls to chat GPT to generate the response and will show it in the text display box on the screen.
 

8. Best Practices
- *Limit API Requests*: Use rate limiting and efficient API handling to prevent excessive API calls and manage costs.

- *Keep Conversations Engaging*: Write natural and interactive NPC responses to enhance the player's experience.

9. Challenges encountered 
Challenge 1 - The repository shared for the reference in the problem statement contained the code in older version of Unity .

Solution = Researched and used the api-endpoints from the package which was compatible with the latest version of Unity

Challenge 2 - The repository shared for the reference in the problem statement contained the older chatGPT engine and was using it in the URL which gave this error:
 
Solution = To solve this I used the latest model : “gpt-3.5-turbo” and latest Chat Api Endpoint of ChatGPT
POST https://api.openai.com/v1/chat/completions

Challenge 3 - While asking ChatGPT answers to my questions from chatGPT Chat API Endpoint I was getting this error 

openai.error.RateLimitError: You exceeded your current quota, please check your plan and billing details
Solution = For this chatGPT gives free 5$ credit in new accout to make calls upto the bill of 5$. So I created a new account and generated API key from that account. Please be careful while using API Calls you might exceed your quota.
