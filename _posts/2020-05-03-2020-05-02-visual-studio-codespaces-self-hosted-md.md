---
layout: post
published: true
title: Self-hosted Visual Studio Codespaces
date: '2020-05-09'
subtitle: The future of code editing running in your browser
---
## Visual Studio Codespaces

If you didn't see the [news](https://devblogs.microsoft.com/visualstudio/introducing-visual-studio-codespaces/) - Microsoft have made Visual Studio Code available online using nothing but your web browser. There are 3 great plans for running the remote environments which offer small, medium and large CPU/Memory combinations and these should suit most simple updates to your code on the run. The environments are charged by the minute and I set mine to auto shutdown 30 minutes after i stop using them.

![screenshot of Visual Studio codespaces running in browser]({{site.baseurl}}/img/visual-studio-online-hero.png)

### Great things about Visual Studio codespaces
- Use Visual Studo Code using nothing but a web browser
- Use extenstions for Visual Studio code in your browser
- Use your bash or other shell from your browser
- Easy to edit code or documentation without the need for time consuming local installs
- Want to update your code using Visual Studio Code from your iPad, tablet or phone? You can just open the web browser and you will have access to your development environment
- Because Visual Studio Codespaces is authenticated using Azure Active Directory you get all the benefits of [MFA](https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-mfa-howitworks) and [Azure AD Conditional Access](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/overview) to protect your development environment

What really got me excited is the ability to self-host a codespace environment - you can use your web browser from any device to securely develop software remotely using your own Virtual Machine, server or desktop.

### Benefits of self hosted
- Use hardware you already have so you don't pay by the minute
- Setup networking connectivity to your own database servers etc...
- Install your own custom tools
- Remotely connect to your own development environment securely by enabling nothing but outbound connectivity (no firewall nastiness)

## Setting up a self-hosted Ubuntu 19.01

Sign up for preview then visit to create a codespaces to create a plan e.g. vso-myplan
https://online.visualstudio.com/environments

Go to https:portal.azure.com and use the search box to find the visual studio online plan by name - vso-myplan 

Select Properties and copy the resource id id including the quotes
![screenshot of azure portal - raw detail tab ]({{site.baseurl}}/img/Screenshot 2020-05-03 at 09.34.45.png)

### Example
"/subscriptions/c931ad62-62d8-4f25-a0d3-c88aaaaabbbbb/resourceGroups/vso-rg-e315e92/providers/Microsoft.VSOnline/plans/vso-plan-eastus",

On your Ubuntu 19.01 VM use the following refer to the [instructions](https://docs.microsoft.com/en-us/visualstudio/online/reference/vsonline-cli#installation)

### Issue
For Ububntu 19.01 we don't have instructions - I expected something like this would work but it didn't work for me sudo add-apt-repository https://packages.microsoft.com/ubuntu/19.01/prod/ (NOTE: currently broken URL) - I therefore followed the generic Linux installation

### Install the self-hosted codespaces environment using vso CLI

For other Linux distributions, run the following script by using curl and pipe directly to bash, or download the script to a file and inspect it before running. 
```
curl -L https://aka.ms/install-vso-linux | sudo bash
```

Start the agent
```
vso start -i "/subscriptions/c931ad62-62d8-4f25-a0d3-c88aaaaabbbbb/resourceGroups/vso-rg-e315e92/providers/Microsoft.VSOnline/plans/vso-plan-eastus"
```
![screenshot of vso start]({{site.baseurl}}/img/Screenshot 2020-05-09 at 08.44.05.png)

You are prompted to sign into your web browser using a technique called Device Code Flow
![screenshot of device login]({{site.baseurl}}/img/Screenshot 2020-05-09 at 08.50.02.png)

Then you accept the fact that the app has access to your profile
![screenshot of accepting]({{site.baseurl}}/img/Screenshot 2020-05-09 at 08.54.31.png)

Then you can just keep pressing enter to accept the defaults and finish setup
![screenshot of finishing installation]({{site.baseurl}}/img/Screenshot 2020-05-09 at 08.58.17.png)

You should now see your environment listed
![screenshot showing new self-hosted environment in Codespaces]({{site.baseurl}}/img/Screenshot 2020-05-09 at 09.01.26.png)

### Success
Using the Ubuntu bash terminal running in Visual Studio Code in my web browser I cloned the repo for this post and was up and running
![screenshot of visual studio codespaces running on self-hosted ubuntu]({{site.baseurl}}/img/Screenshot 2020-05-09 at 09.12.32.png)
