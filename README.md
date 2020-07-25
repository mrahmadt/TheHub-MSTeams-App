# The Hub / Microsoft Teams App

This is Microsoft Teams App for [the Hub](https://github.com/mrahmadt/The-Hub)


# How to Integrate The Hub with Microsoft Teams

## Prerequisites

- You must have The Hub hosted with your own domain, below steps will not work if you are using *.azurewebsites.net
- Your domain must be accessible via https (http is NOT supported)
 

## The Hub

- Make sure you have [The Hub](https://github.com/mrahmadt/The-Hub) already installed and working.


## Azure Active Directory SSO

*From: https://docs.microsoft.com/en-us/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso#develop-an-sso-microsoft-teams-tab*

- Go to The Hub application in the (Azure Active Directory – App Registrations portal)[https://go.microsoft.com/fwlink/?linkid=2083908].
- On the overview page, copy and save the Application (client) ID. You’ll need it later.
- Under Manage, select Authentication.
- Add new "Web" Redirect URIs (https://my.example.com/login/graph/callback) and click save (change my.example.com with The Hub domain name).
- Under Manage, select Expose an API.
- Select the Set link to generate the Application ID URI in the form of api://{AppID}. Insert your domain name (with a forward slash "/" appended to the end) between the double forward slashes and the GUID. The entire ID should have the form of: api://my.example.com/{AppID} 

ex: `api://my.example.com/00000000-0000-0000-0000-000000000000.`

- Select the Add a scope button. In the panel that opens, enter `access_as_user` as the Scope name.
- Set **Who can consent?** to `Admins and users`
- Fill in the fields for configuring the admin and user consent prompts with values that are appropriate for the access_as_user scope:

    Admin consent title: Teams can access the user’s profile.
    Admin consent description: Allows Teams to call the app’s web APIs as the current user.
    User consent title: Teams can access the user profile and make requests on the user's behalf.
    User consent description: Enable Teams to call this app’s APIs with the same rights as the user.

- Ensure that **State** is set to **Enabled**
- Select **Add scope**
    The domain part of the Scope name displayed just below the text field should automatically match the Application ID URI set in the previous step, with /access_as_user appended to the end:
    
    `api://my.example.com/00000000-0000-0000-0000-000000000000/access_as_user`

- In the Authorized client applications section, identify the applications that you want to authorize for your app’s web application. Each of the following IDs **needs to be entered**:

    `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams mobile/desktop application)
    `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web application)


## Download The Hub Teams App

- Download https://github.com/mrahmadt/TheHub-MSTeams-App/archive/master.zip

- Unzip master.zip 


## Update your Microsoft Teams application manifest (file mainifest.json)

*From: https://docs.microsoft.com/en-us/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso*


- (Optional) Change the app name 

`
    "name": {
        "short": "The Hub",
        "full": "Your company App Store"
    },
`

- (Optional) Enter your Website URL
`
        "websiteUrl": "https://my.example.com/",
        "privacyUrl": "https://my.example.com/",
        "termsOfUseUrl": "https://my.example.com/"
`
- (Optional) Enter app description
`
    "description": {
        "short": "The Hub",
        "full": "Your company App Store"
    },
`

- Change below lines with your domain
`
    "contentUrl": "https://my.example.com/teams/myapps",
    "websiteUrl": "https://my.example.com/",
`

- Enter your domain name in `validDomains`
`
    "validDomains": [
        "my.example.com"
    ],
`

- Enter your **Application ID** in the **id** element below and change **resource** element to your API ([**Check Azure Active Directory SSO**](https://github.com/mrahmadt/TheHub-MSTeams-App#azure-active-directory-sso))
`
    "webApplicationInfo": {
        "id": "53cda29e-7798-494b-8cf0-b0b4b50ca52d",
        "resource": "api://my.abdc.com.sa/53cda29e-7798-494b-8cf0-b0b4b50ca52d"
    }
`

