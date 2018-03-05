![](images/100/100-lab.png)  
Update: March 5, 2018

## Introduction

This is the first of several labs that are part of the **Oracle Public Cloud Security and Management workshop.** This workshop will walk you through the various capabilities of **Oracle Identity Cloud Service**.

Although you will login as a single user, you will take on 2 Personas during the workshop. 

* The **LOB Administrator** persona will 

		Onboard users via CSV upload
		Setup and configure SSO Apps
		Configure external identity provider
		Configure MFA and policies
		
* The **End-User** persona will 

		Activate her account 
		Setup and login using various MFA channels 
		Request groups
		Verify SSO for apps from unified launchpad 

### Optional	

* We will see a **Developer** persona exploring `IDCS REST API's` in interactive notebook-style.


## Objectives

- In-built integration with Oracle cloud services `<--Persona: Administrator`
- Onboard users `<--Persona: Administrator`
- Configure SSO for an app `<--Persona: Administrator`
- Grant app to group `<--Persona: Administrator`
- Configure multi-factor authentication `<--Persona: Administrator`
- Activate account `<--Persona: End-User`
- Enroll in multi-factor authentication `<--Persona: End-User`
- Request group `<--Persona: End-User`
- Verify SSO `<--Persona: End-User`
- Optional: API tour `<--Persona: Developer`


## Pre-requisites

- The following lab requires an **Oracle Public Cloud** account trial subscription.

### **STEP 0.1**: Login to your Oracle Cloud Account

- From any browser, go to the URL:
    [https://cloud.oracle.com](https://cloud.oracle.com)

- click **Sign In** in the upper right hand corner of the browser

![](images/100/100-1.png)

- Ensure **Cloud Account with Identity Cloud Service** is selected. Enter your cloud account name. Click on **My Services**

![](images/100/100-2.png)

- On the login page, enter your user name and password and click **Sign In** 

![](images/100/100-3.png)

- You will be presented with a dashboard displaying the various cloud services available to this account.

![](images/100/100-4.png)

### **STEP 0.2**: Access IDCS Admin Console 

- From the cloud **My Services** dashboard, click on **Users** in the upper right hand corner. 

![](images/100/100-4-1.png)

- Then click on **Identity Console** button located towards upper right hand corner again. 

![](images/100/100-5.png)

- If you have logged in using your administrator Account, the users are shown up in IDCS admin console. 

![](images/100/100-6.png)

### **STEP 0.3**: Access IDCS MyApps Console

- From the drop-down associated with the displayed logged-in user in the upper right hand corner of IDCS admin console, choose **My Apps**

![](images/100/100-7.png)
	
![](images/100/100-8.png)
	
# Scenario: Integration with Oracle cloud services

- From the drop-down associated with the displayed logged-in user in the upper right hand corner of IDCS admin console, choose **My Services** to come back to the cloud dashboard.

![](images/100/100-8-1.png)

- Display the sidebar by clicking on the hamburger menu in the upper left hand corner. then expand **Services** to display available Oracle cloud services.

![](images/100/100-8-2.png)	
	
- Click on the service **Analytics**. 

![](images/100/100-8-3.png)

- On the **Analytics** console, click on **Go to Console**

![](images/100/100-8-4.png)

- Observe that the logged in user has successfully single signed-on to the **Analytics** service console

![](images/100/100-8-5.png)

# Scenario - Standard Employee Workflow

## Onboard Users - (Persona: Administrator)

<blockquote>
	<font color="blue">
		<p>
			IDCS supports user (also groups) on-boarding from on-premise 			<b>Active Directory</b>, using file upload, REST API, on-premise 			<b>Oracle Identity Management</b> solution, or manually from IDCS 			admin console.
		</p>
	</font>
</blockquote>

For the exercise we will be using `file upload` option for users.

### **STEP 1**: Obtain upload CSV file

- Download the CSV file for users from [here](resources/Users.csv). Right-click on the link and save the file in your system. Inspect the content of the file from your favorite editor.
	

### **STEP 2**: Import users in IDCS

- Click on the **Users** icon from top right corner assuming you are still on the **Analytics** console.

![](images/100/100-9.png)

- Click on **Identity Console** from top right corner of the **User Management** page.

![](images/100/100-9-1.png)

- On the **Users** page, click on the **Import** button. 

![](images/100/100-10.png)
	
- Select the **CSV** file that you saved locally. Click on **Import**

![](images/100/100-11.png)

- Go to the **Jobs** tab in admin console. Verify that the import Job finished successfully. Click on **View Details** button.

![](images/100/100-12.png)
    
- This will show the detailed information on the **Import** job. Inspect the details.

![](images/100/100-13.png)

### **STEP 3**: Verify user creation

- Go to the **Users** menu in admin console. Verify that the new users are visible on the console.

![](images/100/100-14.png)

![](images/100/100-14-1.png)

- Click on your target end-user and verify user's detailed attribute information.

	<blockquote>
		<font color="red">
			User assigmnets will be provided before the session.
		</font>
	</blockquote>

![](images/100/100-15.png)

    
## Configure SSO for an app - (Persona: Administrator)

<blockquote>
	<font color="blue">
		<p>
			Oracle Identity Cloud Service(IDCS) provides integration with any 			service that can be integrated via <b>SAML</b> (Security Access 			Markup Language) protocol. Administrations will be able to manage 			users into various applications via single control panel and end 			users will be able to get to applications via single click.
		</p>
		<p>
			IDCS provides support for standard SAML 2.0 browser POST login & 			logout profiles.
		</p>
	</font>
</blockquote>


In this hands-on exercise, we will setup integration with **Salesforce** using SAML. IDCS will act as **IdP** (Identity Provider) and Salesforce org as **SP** (Service Provider also known as a Relying Party)

- Download and save IDCS Metadata to a local XML file for your instance. Metadata is available from the following location - 
<blockquote>
	<font color="red">
		https://idcs-xxxxxx.identity.oraclecloud.com/fed/v1/metadata
	</font>
	<font color="blue">
		<br>where idcs-xxxxxx is your IDCS tenant name that you can grab from the browser URL of your IDCS console. Copy-paste the constructed URL on a new browser tab and save the XML file locally.
	</font>
</blockquote>

![](images/100/100-16.png)
	
- Login to the **Salesforce** developer [account](https://demoidaas-dev-ed.my.salesforce.com)

	<blockquote>
		<font color="red">
			Credentials will be provided during session.
		</font>
	</blockquote>

- From side menu bar, go to **Settings** -> **Identity** -> **Single Sign-On Settings**

![](images/100/100-17.png)

- Click on **Edit** and enable **Federated Single Sign-On Using SAML** option. Click on **Save**.

![](images/100/100-18.png)

- Click on **New from Metadata File** button to import IDCS metadata. Select the downloaded metadata XML file using **Choose File** button. Click on **Create**.

![](images/100/100-19.png)
![](images/100/100-20.png)

- Keep all the default information and click on **Save**

![](images/100/100-21.png)
![](images/100/100-22.png)
	
- Go to IDCS admin console -> **Applications** menu

![](images/100/100-25-0.png)

- On the **Applications** page, click on **Add** and select **App Catalog** on the pop-up.

![](images/100/100-25.png)

- Search for **Salesforce** app and click on **Add**

![](images/100/100-26.png)
	
![](images/100/100-27.png)

- On the first page of configuration screen enter the **Organization ID** and **Domain Name** values as provided below. Then click on **Next**.

	<blockquote>
		<font color="red">
			These values are exactly same as those found in the IDCS settings in Salesforce you just configured.
		</font>
	</blockquote>

```	
Domain Name : demoidaas-dev-ed
Organization ID : 00D1N000002M18V
```
![](images/100/100-29.png)

- Click on **Finish** button 

![](images/100/100-30.png)

- **Activate** the application 

![](images/100/100-31.png)

![](images/100/100-31-1.png)

![](images/100/100-31-2.png)


## Grant app to group - (Persona: Administrator)

- Go to IDCS admin console -> **Groups** menu 

![](images/100/100-32.png)

- Add group **Employees**. Check the box `User can request access`. Click on **Finish** 

![](images/100/100-33.png)
	
![](images/100/100-33-1.png)
	
![](images/100/100-33-2.png)

- Go to the **Access** tab. Click on **Assign**. 

![](images/100/100-34.png)

- Select **Salesforce** and confirm 

![](images/100/100-35.png)
	
![](images/100/100-36.png)


## Configure multi-factor authentication - (Persona: Administrator)

<blockquote>
	<font color="blue">
		<p>
			When a user signs in to an application, they are prompted for their 			user name and password, which is the first factor – something that 			they know. With <b>Multi Factor Authentication (MFA)</b> enabled in 			Oracle Identity Cloud Service, the user is then required to provide 			a second type of verification. This is called <b>2-Step 			Verification</b>.
		</p>
		<p>
			The two factors work together to add an additional layer of security 			by using either additional information or a second device to verify 			the user’s identity and complete the login process.
		</p>
	</font>
</blockquote>


- From IDCS admin console, select **Security** -> **MFA** from the sidebar to the left.

![](images/100/100-37-0.png)  

- Select all the options for **Select the factors that you want to enable**. Keep all other parameters to their default values. Click on **Save**.

![](images/100/100-37.png)  

- Confirm new MFA settings.

![](images/100/100-37-1.png)
	
- Select **Security** -> **Sign-On Policies** from the sidebar to the left of admin console.

![](images/100/100-38.png)

- Click on **Default Sign-On Policy**. This will open up the policy. 

![](images/100/100-38-1.png)

- Go to the **Sign-On Rules** tab and then click on **Edit** aganist the **Default Sign-On Rule**.

![](images/100/100-38-2.png)

![](images/100/100-38-3.png)

- Check the box **Prompt for an additional factor**. Set the value of **Enrollment** to `Optional`. Click on **Save**.

![](images/100/100-38-4.png)

![](images/100/100-38-5.png)

	

## Activate account - (Persona: End-User) 

<blockquote>
	<font color="green">
		<p>For end-user flow, use either a separate browser or an incognito/		private browser session. This will ensure that administrator and user 		sessions are not mixed up.</p>
	</font>
</blockquote>

- Login to gmail as [demoidcs@gmail.com](). Go to the gmail label corresponding to your user. Verify that there is an activation email from IDCS.

	<blockquote>
		<font color="red">
			Gmail password will be provided during session.
		</font>
	</blockquote>

![](images/100/100-39.png)

- Open and review the email. Click on the **Activate Your Account** button. 

![](images/100/100-40.png)
	
- IDCS change password page will open up. Provide a suitable password that matches the listed **Password Criteria**. Click on **Submit**.

![](images/100/100-41.png)

- Verify that you are redirected to the MFA enrollment page.
  
## Enroll in multi-factor authentication - (Persona: End-User)

- On the **Enable 2-Step Verification** page, click on `Enable`

![](images/100/100-42.png)

- Select the method `Email`

![](images/100/100-43.png)
	
- Access your email to obtain the one-time passcode .
	
![](images/100/100-45.png)

- Provide the 6-digit code on the enrollment page and click on `Verify`

![](images/100/100-46.png)
	
- Ensure that the success enrollment message is displayed. Click on `Done`
	
![](images/100/100-47.png)
![](images/100/100-48.png)

- Logout from IDCS and re-login with your credentials

- Ensure that you are challenged by 2-Factor authentication and have received a new email containing a new 6-digit one time code.

- Provide the new 6-digit code on the challenge screen for verification

- On successful verification, ensure that user is logged in to the **MyApps** page of IDCS.

![](images/100/100-48.png)

## Request group - (Persona: End-User)

- From MyApps page click on `Add` access request button.

![](images/100/100-48.png)

- From the **Groups** tab, select `Employee` group

![](images/100/100-49.png)
	
- Click on `+` sign to request access to the group. Provide justification on the resulting popup page. Click on `OK`

![](images/100/100-50.png)
		
- Go to `My Profile` section from menu located top-right

![](images/100/100-52.png)
	
- Ensure that `Employee` group is visible under **My Access** sub-tab
	
![](images/100/100-53.png)
	
- Go to `My Apps` section from menu located top-right

![](images/100/100-54.png)
	
- Ensure that Salesforce applications are visible now on the **MyApps** page
	
![](images/100/100-55.png)


## Verify SSO - (Persona: End-User)

- Click on the `Salesforce Chatter` app. 
- Ensure that user is automatically logged-in to Salesforce Chatter (**SSO**)

![](images/100/100-56.png)


# Scenario - Developer Features

## For Information Only: API Tour - (Persona: Developer)

IDCS is built using API-first approach. All the features are accessible through REST API's and are protected by OAuth 2.0 framework. Most of the API's need an **OAuth Access Token** in order to be accepted by IDCS. 

In this demo we will explore some of the API's in the reportaire, especially - 

	1. IDCS Configuration Discovery
	2. Obtaining and inspecting OAuth token
	3. User management
	4. Audit API

The demo uses hosted **Jupyter Notebook**

[Access Notebook Here](http://140.86.32.135:65000/notebooks/IDCS-API.ipynb)


