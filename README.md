# MEMPowerBI
This is a PowerBI report template for Microsoft Endpoint Manager EPP. It merge data from Configuration Manager and from Microsoft Endpoint Manager allowing you to have a unique report for Cloud Managed devices, Co-Managed devices and CM only managed devices.

![image](https://user-images.githubusercontent.com/48328018/124558003-6fcb5c80-de3a-11eb-977f-73063888a096.png)

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

From here: https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps
click "New registration"
![image](https://user-images.githubusercontent.com/48328018/124559936-883c7680-de3c-11eb-82fe-4dc0b75d380f.png)
Enter you application Name
![image](https://user-images.githubusercontent.com/48328018/124560064-b0c47080-de3c-11eb-9015-8881f2a32a8c.png)

Add a client secret to your application
![image](https://user-images.githubusercontent.com/48328018/124560367-039e2800-de3d-11eb-8a90-418735379610.png)
Don't forget to copy your secret somewhere or to paste it directly in the PowerBI Parameter prompt as it won't be displayed again once you leave that screen

Grant the correct permission
![image](https://user-images.githubusercontent.com/48328018/124561320-0baa9780-de3e-11eb-855e-8a5c44924692.png)
Click "Add a permission", select "Microsoft Graph"
![image](https://user-images.githubusercontent.com/48328018/124561389-20872b00-de3e-11eb-851e-e932bbaa9fcb.png)
Then "Application permissions" and add "Device.ReadAll", "DeviceManagementConfiguration.Read.All" and "DeviceManagementManagedDevices.Read.All"
![image](https://user-images.githubusercontent.com/48328018/124564866-c6886480-de41-11eb-977c-835757e1a970.png)
Click "Add permissions" 

Remove the "User.Read" permission that is not required and then click on "Grant permission for XXXXX"
![image](https://user-images.githubusercontent.com/48328018/124561785-8ffd1a80-de3e-11eb-8104-1815947001cd.png)



## Get data from MEM CM
To connect you MEM CM, you just need to enter the name of the server hosting the Configuration Manager SQL Database and the Database name (usually CM_[name of your primary site])

## Publish it to the PowerBI Service
You can use that report in the PowerBI Service and have a scheduled refresh. To do so, you'll need to deploy the PowerBI Gateway to allow the service to access your onPrem SQL
