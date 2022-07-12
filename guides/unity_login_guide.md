---

title: Unity Login Widget Guide
excerpt: Basics of how to setup the Stardust Login Widget for your Unity Game
category: CLIENT_SDK_ID
slug: unity-login-widget
order: 1

---
<!--

The above section is not user read text! It's configuration information when syncing with our customer facing documentation. Find out more here: https://docs.readme.com/docs/rdme

-->
# Stardust Login Plugin

## Table of Contents

- [Pre-requisites](#pre-requisites)
- [Installation](#installation)
- [Installation for package Dev](#installationForPackageDev)
- [Project Setup](#project-setup)
- [API Gateway Setup](#api-gateway-setup)
- [API Call Helper](#api-call-helper)
- [Example Requests](#example-request)

# Pre-requisites

Unity Editor version: 2021.3.2f1

Supported Platforms: iOS, Android

Text Mesh Pro: 3.0.6

# Installation
## Download from Github
1.  Open your unity project 
2.  Go to Window -> Package Manager 

![PackageManager](img/window_dropdown.png)

3.  Click on the + button 
4.  Then select "Add package from git URL" using the git URL: https://github.com/Stardust-Platform/stardust-unity-login.git

![PackageManagerAddURL](img/package_manager.png)
5. Drag and Drop the "Plugins" Folder found in "stardust-unity-login" into the root asset folder of your project.

6. Follow the iOS Deep linking instructions for URL Schemes. This can be found here: https://docs.unity3d.com/2021.2/Documentation/Manual/deep-linking-ios.html Set the size to 1, and for the element 0 field put in 'myapp'

## Configure the Login SDK Data
After you've setup either scene to your liking, we need to create a config file to connect to your Stardust game instance(If you haven't created a game yet, checkout our [getting started guide](https://tbd) on making your first Stardust game).

1. Navigate to any subdirectory of your Projects Assets Folder(it doesn't matter where your config is, as long as it's somewhere within the project's directory)
2. Right click and follow the navigation options to create a StardustConfig file

![CreateStardustData](img/CreateStardustData.png)
3. With a new config file, go ahead and click to open up the config options

![ConfigDetails](img/ConfigDetails.png)
4. At a minimum to get started, make sure to update `Game Id` with the game id found on the dashboard

## Setting up the Login Scene 
There's two default scenes provided with the login sdk:
1. LoginScene which comes with all functional components enabled out of the box
2. BarebonesScene which comes all the essential elements to create your own UI manager

> Whether you're using the LoginScene right out of the box or you're designing your own using the BarebonesScene, one limitation to be aware of is that to date, the unity login sdk only support Google and Discord single-sign-on (SSO). In the future, we hope to add more functionality and options to provide a larger variety of ways your players can login.

### Login Scene Setup

1. First drag and drop the LoginScene from the package project(Packages -> stardust-unity-login-> Assets -> Scenes -> LoginScene) to the Assets (Assets -> Scenes) folder of your project
2. Navigate to the Hierachy and open the LoginScene
3. Find Authenication Manager and select it
4. Locate your StardustConfig file and drop it into the Stardust Config

![DragStardustConfig](img/DragStardustConfig.png)
At this point, your login scene should be correctly configured and you're ready to [start working with the login sdk](#working-with-login-sdk)

### Barebones Scene Setup

In the event that you want to customize the login process with your own UI, you'll need to use the BarebonesScene to accomplish such.

To understand how to work with Barebones Scene, let's go over the Authentication Manager SDK and an example of how to implement it. 

#### Authentication Manager SDK Explained
The Authentication Manager SDK comes with a couple different events that you can listen for to determine how you want the game to react. For example, if the player logs in you can hide the Canvas and render the map. Another example, If the players tokens become invalid and should be refreshed, provide a pop-up that asks the player if they want to reconnect or disconnect. Lastly, If a player's tokens should be refreshed and refreshing fails, then you can disconnect the player from the game; For them to reconnect, they must first log back in. These are some of the use cases around why we've created these listeners and how they can be used. This is why we designed the barebones scene for developers to be able to customize how they want to interact with the players current authentication status in relation to Stardust.

The 4 Events Types to listen for are:
- exchangeCodeForTokenEvent - This event happens when the player initially attempts to log in
- shouldTokenBeRefreshedEvent - This event happens when the access token expires
- refreshTokenEvent - This happens when the client attempts to refresh the tokens
- logoutEvent - This event happens when the player attempts to logout

> Currently the `shouldTokenBeRefreshedEvent` is just triggered in the event that an API call fails, if the API calls fails for other configuration issues that are not related to the token being invalidated, this may trigger your events that are listening for `shouldTokenBeRefreshed` thus causing unintended behavior to occur.


#### Example Implementation

In this example we're going to just make a simple login process where we listen for when the player successfully signs in, and then we hide all the login UI elements.

To start we're going to navigate to to the BarebonesScene hierachy and modify a few things.

![BarebonesHierachy](img/BarebonesHierachy.png)
To explain a bit what you're seeing in the hierachy, we have the follow gameObjects to support the login SDK:
- ProcessDeepLink - Handles flow between browser and application on mobile devices. No configuration required here.
- Authenication Manager - Authenticates the user against Stardust and connects them to your game via it's ID referenced in StardustConfig
- GoogleSignin - This GameObject is the button interface to interact with the Provider, be it Google or Discord.
- EditorUrl - This only needs to be enabled when working in the Editor. Explained more in [During Development](#during-development)

Just like how we started with the login scene, let's do the same by first finding the Authentication Manager and selecting it. With it open in the inspector now, let's drag and drop the StardustConfig file we created earlier in the StardustConfig field.

![DragStardustConfig](img/DragStardustConfig.png)
With that out of the way, next we need to create a new UImanager script or attach one that already exists to any gameObject in the Scene. For this guide, we're going to attach a new Script to the Canvas.

![ConfigBareboneCanvas](img/ConfigBareboneCanvas.png)

Now opening up our new script that we've created we're going to structure it as such:

![UIManagerCode](img/UIManagerCode.png)

A couple of things to explain about this code:
- Make sure you import the required packages at the top, UnityEngine.UI and TMPro
- Within the class we've exposed 3 serialized fields to be able to interact with in the inspector.
- Within the Start function we've added 3 of the 4 Event Listeners 
- Of the 3 Listeners we've associated some basic logic for each. When the player has successfully logged in, we set our gameObjects to be inactive. And then for our refresh and logout events, we just log those to the console.

With this code created, we're going to save and go back to the Unity Editor.

Now back at the Unity Editor, we're going to associate our UI gameObjects with the serialized fields we created in our script.

![DragUIToLogic](img/DragUIToLogic.png)

With the UI gameObjects now assoicate with the proper logic to manage them, this barebones scene is now succesfully configured.

#### Extending the BarebonesScene
Now that you understand how to hook everything up to make it work together, let's see how we can extend based on top of this.

If you go to the package and within the package go to the prefabs you can find all the prefab gameobjects to customize any login scene with

![BarebonePrefabs](img/BarebonePrefabs.png)
For example, with the barebones scene we made above, we could navigate to stardust-unity-login -> Prefabs -> IndividualParts -> DiscordLogin and drag and drop that into our BarebonesScene Canvas to add Discord Login and now support both Discord and Google Single-Sign-On (SSO).

# Working with Stardust Login SDK
Currently the login sdk only supports iOS and Android games. As game developers will not be designing, developing, and iterating on their game all through a mobile device, we made sure that the sdk was functional(although not as pretty) for the Unity Editor on Desktop. When you have a functioning prototype that you're ready to build and test on your targeted mobile device, the login sdk is configured to make for a seamless user experience for players.

## During Development (non iOS/Android platform)
When working with the Unity Editor on your device of choice, we've provided a few additional UI elements to allow you to functionally test your Stardust integration. To start,

1. Make sure your `EditorUrl` is enabled in your Scene
2. Click Play
3. Select a provider to authenicate with (Google or Discord)
4. Step your way through their login process


![Provider](img/Provider.png)

5. When you get to the error page in the process, copy the URL from the error page

![ErrorPage](img/ErrorPage.png)

6. And then paste that into the URL field and then press submit.

![PasteSubmit](img/PasteSubmit.png)

Once Complete, you've now successfully authenticated your code and received an access token, id token, and refresh token. These tokens can be decoded to get Player specific information to pass through when using the Stardust Core API, or allow your players to interact directly with the Stardust Market API when creating things such as buy or sell orders. Feel free to Jump ahead to the next section: [Making API Calls to Stardust](#making-api-calls-to-stardust)

## iOS and Android Builds
When wanting to do production testing of your game or application directly on the mobile device of your choice, the login sdk natively supports deeplinks. This allows you to remove the `EditorURL` gameObject from the LoginScene/BarebonesScene and do end user testing. Assuming Installation was properly followed, both iOS and Android should be properly configured to work with your Unity Build regardless of target platform.

<!--
TODO
Insert GIF of Deeplink Flow
-->
# Making API Calls to Stardust
The two things you'll need to make an API call to stardust are `AuthenticationManager.GetIdToken()` and `AuthenticationManager.GetUserId()`. The User Id is something you can pass to your game's backend server to let it know which player it's interacting with. Knowing which player it's now interacting with, you can make state changes to the players wallet via the Stardust Core API. Check out more on the Stardust Core API at https://docs.stardust.gg/. For the ID token, this is used for the player to make direct client-to-Stardust calls for peer-to-peer trading via the Stardust Market. To learn more about how configure peer-to-peer trading via the Stardust Market API, checkout: https://stardust-marketplace.readme.io/reference.

<!--
TODO ReFactor
# API Call Helper

Class to make easier the request to the Stardust API

Class Name: ApiCallHelper.cs

## Functions
The two helpers methods through which we encourage people to make API calls to Stardust with are:

Get Request Query

    GetRequestQuery(string url, KeyValuePair<string, string>[] query);

Get Request Header

    GetRequestHeader(string url, KeyValuePair<string, string>[] headers);

# Example Requests
<!-- 
TODO:
Update Core Requests to explain getting and using ID Token for Market API and getting and using User ID for Core API

## Stardust Core Requests


### Get Game 

    string url = ApiUrl + "/game/get";

    KeyValuePair<String, String>[] query = new KeyValuePair<string, string>[1];
    query[0] = new KeyValuePair<string, string>("gameId", StardustData.GameId);

    await ApiCallHelper.GetRequestQuery(url, query);

### Get Balance

    string url = ApiUrl + "/balance/get";
    KeyValuePair<String, String>[] reqHeaders = new KeyValuePair<string, string>[1];
    reqHeaders[0] = new KeyValuePair<string, string>("Authorization", authenticationManager.GetIdToken());

    await ApiCallHelper.GetRequestHeader(url, reqHeaders);

## Get Inventory

     string url = ApiUrl + "/player/inventory-get";

    KeyValuePair<string, string>[] reqHeaders = new KeyValuePair<string, string>[1];
    reqHeaders[0] = new KeyValuePair<string, string>("Authorization", authenticationManager.GetUserId());

    await ApiCallHelper.GetRequestHeader(url, reqHeaders);

## Marketplace Requests

### Get Game 

    string url = ApiUrl + "/game/get";

    KeyValuePair<String, String>[] query = new KeyValuePair<string, string>[1];
    query[0] = new KeyValuePair<string, string>("gameId", StardustData.GameId);

    await ApiCallHelper.GetRequestQuery(url, query);

### Get Balance

    string url = ApiUrl + "/balance/get";
    KeyValuePair<String, String>[] reqHeaders = new KeyValuePair<string, string>[1];
    reqHeaders[0] = new KeyValuePair<string, string>("Authorization", authenticationManager.GetIdToken());

    await ApiCallHelper.GetRequestHeader(url, reqHeaders);

## Get Inventory

     string url = ApiUrl + "/player/inventory-get";

    KeyValuePair<string, string>[] reqHeaders = new KeyValuePair<string, string>[1];
    reqHeaders[0] = new KeyValuePair<string, string>("Authorization", authenticationManager.GetIdToken());

    await ApiCallHelper.GetRequestHeader(url, reqHeaders);

## Post Request

NOTE: To get more information about marketplace request visit: 
    
https://stardust-marketplace.readme.io/docs
-->
