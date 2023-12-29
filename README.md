# **MSO_E5_Dev_AR**

Python application based on Git Actions that use Microsoft Graph API. This guide will provide you with easy-to-understand steps for setting up and running the application.

### Special Notes/Thanks ###
* Normal version address: github.com/HarryVed/Microsoft-Developer-Subscription-Renew-Free

## **Prerequisites**
- A GitHub account
- An existing or new Microsoft Developer E5 account

## **Setup Steps (Encrypted Secure Version)**

1. Register a new application in Azure Active Directory.
    - Go to https://entra.microsoft.com/
    - Applications > App reginstrations > New registration
    - Select "Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant)"
    - Select "Web" for the redirect URL, and enter "**[http://localhost:53682/](http://localhost:53682/)**" for the redirect URL.
    - Save Application ID
    - Go to Certificates & Secrets > New 
    - Save the Secret value.
3. Set API permissions.
    - Go to API Permissions > NEW
    - Select Microsoft graph > Application permissions
    - Select the following permissions: **`files.read.all`**, **`files.readwrite.all`**, **`sites.read.all`**, **`sites.readwrite.all`**, **`user.read.all`**, **`user.readwrite.all`**, **`directory.read.all`**, **`directory.readwrite.all`**, **`mail.read`**, **`mail.readwrite`**, **`mailboxsetting.read`**, and **`mailboxsetting.readwrite`**.
    - "Grant admin consect for MSFT" for all 13 selected permissions.
4. install rclone in your system. It is required to get refresh token (one time only)
5. Execute the command **`rclone authorize "onedrive" "id" "secret"`**.
    - **id** is the Application ID you get it from previous steps
    - **secret** is the Application secret you get it from previous steps
    - Execute, Select admin account the prompt and save the refresh token.
6. Install JsonHandle chrome extention and open it. Paste the access_token acquired from previous step in the dialog box and copy the `refresh_token` from it
7. Keep Application ID, Secret, Refresh_token handly you will need it in the next step
8. Go to the project settings and from the left hand side menu select Secrets and Variables > Actions
9. Click **New repository secrets.** and create three variables and set the value as given below
    - Name: **`CONFIG_ID`** value is App ID
    - Name: **`CONFIG_KEY`** value is App secret
    - Name: **`REFRESH_TOKEN`** value is Refresh token
10. Goto the project setting again and choose Actions menu and scroll down until you see **Workflow permissions click Read and write permission option**
11. Go to your personal settings page on GitHub, select Developer settings > Personal access tokens > Generate new token.
    - Set the name to **`GITHUB_TOKEN`**.
    - Check the options **`repo`**, **`admin:repo_hook`**, and **`workflow`**.
    - Generate the token.
12. Run the action Workflow
13. Click on the Actions tab above to see the log of each run and check if the API is called correctly and if there are any errors.

## **Additional Information**

- The default setting is to run three rounds every six hours from Monday to Friday. You can modify your own crontab to change the frequency and time.
- If you need to modify the API calls, you can check the Graph Explorer at https://developer.microsoft.com/graph/graph-explorer/.
