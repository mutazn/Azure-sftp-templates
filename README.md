# Azure-sftp-templates

**Installation**
  
  With DNS Label
   ```
az group create --name <resource-group-name> --location <resource-group-location>
az deployment group create --resource-group <my-resource-group> --template-uri https://raw.githubusercontent.com/mutazn/Azure-sftp-templates/main/sftp-existing-stg-multi-users-with-dnslabel.json
   ```
  Without DNS Label
  ```
az group create --name <resource-group-name> --location <resource-group-location>
az deployment group create --resource-group <my-resource-group> --template-uri https://raw.githubusercontent.com/mutazn/Azure-sftp-templates/main/sftp-existing-stg-multi-users.json
   ```
***Tips***

1. **secureVaule** is used to hide the username and password from Azure container group template once deployed.
   ```
   "environmentVariables": [
     {
       "name": "SFTP_USERS",
       "secureValue": "[variables('sftpEnvVariable')]"
      }
    ]
   ```
 
2. Users can be defined with a space between them, example: foo:pass:::upload1 bar:pass:::upload2

   User "foo" with password "pass" can login with sftp and upload files to a folder called "upload1".   
   User "bar" with password "pass" can login with sftp and upload files to a folder called "upload2".

  ```
   "sftpEnvVariable": "[concat(parameters('sftpUser1'), ':', parameters('sftpPassword1'), ':::upload1', ' ', parameters('sftpUser2'), ':', parameters('sftpPassword2'), ':::upload2')]"
  ```
 
 3. If you want to use the same file shares for both users then use the same files shares name for (File Share Name1 & File Share Name2).
 
   ![image](https://user-images.githubusercontent.com/32297719/120243355-09b64d00-c270-11eb-9ab1-d47a0557aec0.png)

Otherwise you can use different file shares:

   ![image](https://user-images.githubusercontent.com/32297719/120243334-fc995e00-c26f-11eb-9001-344b2b291ef5.png)
 
*Note:* Make sure to create the file shares before creating your sftp deployment.
