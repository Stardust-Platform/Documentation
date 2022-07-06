---

title: Unreal Login Widget Guide
excerpt: Basics of how to setup the Stardust Login Widget for your Unreal Game
category: CLIENT_SDK_ID
slug: unreal-login-widget
order: 2

---
<!--

The above section is not user read text! It's configuration information when syncing with our customer facing documentation. Find out more here: https://docs.readme.com/docs/rdme

-->

# Stardust Login Plugin

## Table of Contents

- [Pre-requisites](#pre-requisites)
- [Installation](#installation)
    - [Adding the plugin as a Submodule](#adding-the-plugin-as-a-submodule)
    - [Cloning the repository](#cloning-the-repository)
    - [Manual Installation](#manual-installation)
- [Project Setup](#project-setup)
- [Api Gateway Setup](#api-gateway-setup)

# Pre-requisites

1.  Check Your Unreal version and make sure is the UE 4.27 
2.  Enable the Web Browser plugin from Unreal engine
3.  Get VARest from the Unreal Engine Marketplace
4.  Check if you have a C++ compiler (Such as cmake or Visual studio compiler)  
5.  Stardust login requires C++ to function properly, make sure your project is configured as a C++ project


# Installation
    
## Adding the plugin as a Submodule

Go to the root of the project and create a Plugins folder if one does not already exist.

Open a terminal and type the following command:

    git submodule add https://github.com/Stardust-Platform/stardust-unreal-login.git

    or

    git clone https://github.com/Stardust-Platform/stardust-unreal-login.git

Then right click the unreal project file and click Generate visual studio project file

![6](img/files-generateVSproject.png)

And Open the project

![10](img/ProjectMapModes.png)

## Cloning the repository with example

**With version 2.13 of Git and later, --recurse-submodules can be used instead of --recursive**

    git clone --recurse-submodules https://github.com/Stardust-Platform/stardust-unreal-login.git
    cd stardust-unreal-login

**With version 1.9 of Git up until version 2.12 (-j flag only available in version 2.8+):**
    
    git clone --recursive https://github.com/Stardust-Platform/stardust-unreal-login.git

    cd unreal-login 

**If the repo is already clone**

    git clone https://github.com/Stardust-Platform/unreal-login.git
    cd unreal-login 
    git submodule update --init --recursive
## Manual Plugin Installation    

 1. Open the project and enable the Web Browser Plugin from Unreal Engine.

![1](img/pluginbrowser.png)


2. Close the project and Delete the following files and folders projectName.sln, Intermediate, Saved, Binaries.

![2](img/files-deletesource.png)


3. Create a Plugin folder if you don't have one, in the root of the project.

![3](img/files-createplugin.png)

4. Copy the StardustLogin folder and paste it inside the Plugins folder.

![4](img/files-pastewidget.png)

5. Right click the Unreal Engine Project File
6. Click Generate Visual Studio Project Files

![5](img/files-projectfileoptions.png)

7. Open the project 

![6](img/files-generateVSproject.png)
![7](img/files-rebuild.png)
![8](img/files-projectbuild.png)

8. In button right corner of the Content Browser, click View Options, and enable Show Plugin Content

![ShowPluginContent](img/showplugincontent.png)

9. Setup the Project GameMode with BP_Stardust_GameMode and the Game Instance class with GI_Stardust

    Going to:
    Edit -> Project Settings -> Maps & Modes 

![10](img/ProjectMapModes.png)


10. Go to the StardustLogin Content folder and drag and drop the StardustWidget folder in the project content.

![11](img/copywidgetfolder.png)


11. Compile and restart the project.

Compile your UE4 Project after the project is compile successfully close the Editor and Open the project again.
![UEUi](img/compileproject.png)

# Project Setup

The Stardust Login  properties can be found in the StardustGameInstance.h file

**StardustLogin C++ Classes -> StardustLogin -> Public**

**Note:** Remember to enable in the view options *Show Plugin Content* step 8

![image](img/widgetconfigcode.png)


LogoUrl: Set an url with the logo of your brand to show.

![Logo](img/widgetimage.png)

TermsOfServiceUrl: Url with the terms of services of the company.

PrivacyPolicy: Url with the Privacy Policies of the company.

GameId: 

![image](img/gameIDcode.png)


# How to start using the Widget

Select StardustGameMode as you game GameMode

**By going to Edit -> Project Settings -> Maps & Modes**

![SelectingGameMode](img/ChangeGamemode.png)

Select StardustWidget as your Editor Map and Default Map

![MapsAndModesSelection](img/ChangeMap.png)

Set GI_Stardust as your GameInstance Class

![GameInstanceSelection](img/ChangeGameInstance.png)

Compile the project and close the Editor and opened again

Click on the Play button to test
# Api Gateway End Points

## API END POINT

    https://bddtm60cbd.execute-api.us-east-1.amazonaws.com/v1

Sub (UUID): Is the unique identity for a user obtain by decoding the idToken when an user logs in and store to be used later to make request to the Stardust Marketplace

## /exchange-code-for-tokens

Send a post request with a json object containing a code to exchange for login tokens and sends the gameId to Register a new player in the game pool

Example of the body request to request tokens:

    {
        "body":"{
                "code": "8bb3db31-edea-47ea-aae2-4e14926ede3d"
                "gameId": "1"
            }"
    }

## /retrieve-new-tokens

Post request with an Authorization Header and an Access Token as the value. With a json object containing the player Refresh Token to refresh the player session with new tokens

Example of the body request to new tokens exchanging the refresh token:

    {
        "body":"{
                "refreshToken":"<insert-valid-refresh-token-here>"
            }"
    }

##  /invalidate-tokens

Get request with an Authorization Header with the player Access Token as the value to invalidate the current tokens and logout.

Example of the Header request to invalidate tokens:

    "headers": {
            "Authorization": "<insert-valid-access-token-here>"
        }
    }

# StardustWidgetFunctionLibrary

Class to make easier the request to the Stardust API

Class Name: ApiCallHelper.cs

## Functions


GetSubFromIdToken: Returns an FString with the IdToken Decoded and ready to used as a sub or uuid.

    UStardustWidgetFunctionLibrary::GetUserSubFromIdToken(FString IdToken)

SaveToJson: Save the new token an the  idToken decode in a json file 

    UStardustWidgetFunctionLibrary::SaveToJson(FString NewAccessToken, FString NewIdToken, FString NewRefreshToken, FString NewSub)

LoadFromJson: Load tokens saved before and to then try to login if the token are valid

    UStardustWidgetFunctionLibrary::LoadFromJson(FString& NewAccessToken, FString& NewIdToken, FString& NewRefreshToken, FString& NewSub)
# Example Requests

## Get Requests

### Get Game 



### Get Balance



## Get Inventory
    TSharedRef<IHttpRequest, ESPMode::ThreadSafe> Request = Http->CreateRequest();

	// get game instance, which will allow us to grab singleton-like class GI_Inventory to call the refresh
	UGameInstance* gameInstance = GetWorld()->GetGameInstance();
	if (gameInstance != nullptr) {
		UStardustGameInstance* StardustGameInstance = Cast<UStardustGameInstance>(gameInstance);
		Request->OnProcessRequestComplete().BindUObject(this, &UUHttpManager::OnGetInventoryResponse);
		Request->SetURL("https://xpfssmd0a5.execute-api.us-east-1.amazonaws.com/Demo_Test/player-inventory?sub=" + StardustGameInstance->Sub);

		Request->SetVerb("GET");
		Request->SetHeader("User-Agent", "X-UnrealEngine-Agent");
		Request->SetHeader("Accept", "application/json");
		
		Request->ProcessRequest();
	}
    

## Post Request

NOTE: To get more information about marketplace request visit: 
    
https://stardust-marketplace.readme.io/docs
