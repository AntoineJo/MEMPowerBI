# MEMPowerBI
This is a PowerBI report template for Microsoft Endpoint Manager EPP. It merge data from Configuration Manager and from Microsoft Endpoint Manager allowing you to have a unique report for Cloud Managed devices, Co-Managed devices and CM only managed devices.


## How to use it
You can open that PowerBI template directly in PowerBI desktop.

You will be ask to enter connection information. 

![image](https://user-images.githubusercontent.com/48328018/124548338-deee8400-de2d-11eb-9fca-4d95cd33befe.png)

Depending on the data source you want to use, you can enter either or both:
  - ApplicationID, TenantGUID and ApplicationSecret for MEM data (see below where to get them)
  - SQLServerName and DBName for CM data

## Get data from MEM
To gather data from MEM we are using the Microsoft Graph API as the antimalware data is not yet available from the MEM DW.
Thus you need to create an Application in Azure Active Directory and give it access to the Microsoft Graph on the MEM part. Proceed as described here to do so: https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app
Your application will be a Web Application, no need for a return URL

Then create an Application Client Secret.

### Define permission for you app in the Microsoft Graph
You should add the following permissions to your application in the Microsoft Graph
![image](https://user-images.githubusercontent.com/48328018/124557137-72798200-de39-11eb-9d49-4949afb5c906.png)

## Get data from MEM CM
To connect you MEM CM, you just need to enter the name of the server hosting the Configuration Manager SQL Database and the Database name (usually CM_[name of your primary site])

