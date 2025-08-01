
Steps to Deploy and Use the Application

1. Clone the application repository from the Git source.

2. Build the mta.yaml file using one of the following methods:

         mbt build or

         Right-click the project in your IDE and select: "Build MTA Project" This process generates a .mtar file.

3. Deploy the generated .mtar file to your Cloud Foundry space.

4. Post-Deployment Configuration

      a. Update xs-security.json  After deployment:

            Copy the deployed application's URL.

            Add the following section after roles-template in xs-security.json:
   
                      "oauth2-configuration": {
                           "redirect-uris": [
                                 "<Deployed-Application-URL>/**"
                               ]
                           }

                 Example URL:  https://4a13cd20trial-dev-userassignmentapp.cfapps.us10-001.hana.ondemand.com

       b. Configure Destination in BTP Trial Account

             Open xs-app.json and locate the destination field. Create a destination in your BTP Trial account that matches the name exactly.

             Destination Details:

                   Name: ASSEMBLY_POD_DEST (can be customized, but must match xs-app.json)

                   Type: HTTP

                   Authentication: OAuth2ClientCredentials

                   Client ID: [Provided in service key]

                   Client Secret: [Provided in service key]

                   Proxy Type: Internet

                   URL: Public API Endpoint

                  Token Service URL: <Service-URL>/oauth/token

                  Additional Property:

                        Key: HTML5.DynamicDestination

                        Value: true

                  Note: You can find the client credentials in your RITS DMC subaccount under Instances and Subscriptions > [Your Instance] > Service Key of SAP DMC Execution.

5. Prepare Application Launch URL

       Create the final URL in this format:  <Deployed Application URL>/<welcomeFile from xs-app.json>

       Example:   https://4a13cd20trial-dev-userassignmentapp.cfapps.us10-001.hana.ondemand.com/ui/index.html

       Open this URL in a new browser tab to launch the application.
	   
6. Download the CSV File

       Download the users.csv file located in the resource folder at the root directory of the project.

7. Launch and Use the Application

     Open the deployed application URL in a new browser tab. You should now see the user interface of the project.

         Step 1: Upload the CSV File

              Upload the downloaded CSV file using the Upload option in the application.

              After uploading, the user data will be displayed. You may modify the data as needed—ensure values remain comma-separated if editing manually.

        Step 2: Retrieve User Details

                Enter the Plant and User ID in the respective input fields. Click Retrieve.

               The application will display all user details associated with the entered user ID.

       Step 3: Create Users

              Click the Create button to initiate user creation.

              If the user already exists, it will not be created again.

              If the user does not exist, a new user entry will be created.		

    

## UserAssignmentApp
A side-by-side extension using SAP UI5 and public User APIs provided by SAP DM to automate the user assignments to work centers.
Details  please check out SAP Community Blog "Link to be added as soon as published"

## Prerequiste
### 1. Set Up a Destination in Your Subaccount
To call a public API in your coding you first need to setup a destination in your subaccount pointing to the Public API. 
Details you can find on SAP HELP https://help.sap.com/docs/sap-digital-manufacturing/operations-guide/prepare-for-api-integration
### 2. Configure the SAP Cloud Application Router (xs-app.json)
In the xs-app.json file the configuration for your SAP Cloud Application Router, which helps route incoming requests within your app, is defined. 
Make sure it points to the destination you have defined.
### 3. Adjust environment configuration settings in SAP BTP
Issue: Many modern browsers, including Google Chrome, have tightened restrictions on third-party cookies to improve privacy and security.
This can impact authentication flows or application behavior that relies on cookies for session management
Solution: Navigate to the SAP BTP Space where your application is deployed. Locate your environment configuration settings.
Add or modify the variable: COOKIE_BACKWARD_COMPATIBILITY=true
This instructs SAP BTP to maintain compatibility with older cookie behavior, helping resolve login and session issues.

