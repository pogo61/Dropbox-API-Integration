# Akana API HOOK
![Image of Akana] 
(https://www.akana.com/img/formerlyLOGO8.png) 
[Akana.com](http://akana.com)

## Dropbox-API-Integration
API Integration is an API that combines the SalesForce and Dropbox API Hooks so that it takes a lead, inserts it into SalesForce, then Appends it to a file stored in Google Drive

### Pre-Reqs
- Ensure the [Dropbox API Hook](https://github.com/pogo61/Dropbox-API-Hook) is installed

### Getting Started Instructions
#### Download and Import
- Download migration.properties
- Download the migrations.properties file, and edit it to replace the <replace this with your key> text with the "Container Key" of the ND or ND cluster in your target PM.
    - the container key is found by going to the "Deatils Tab" of the ND cluster, or ND defined in the Policy Manager Console, then looking at the " Container Overview" tab on that page, and copying the "Container Key:" value. ![container key screenshot](https://github.com/pogo61/Google-Sheets-API-Integration/blob/master/Screen%20Shot%202015-03-18%20at%2011.24.45%20am.png "ND Container Key")
- Login to PolicyManager  example: http://localhost:9900
- Select the root "Registry" organisation and click on the "Import Package" from the Actions navigation window on the right side of the screen
  - click on button to browse for the DropboxAPIIntegration.zip archive file 
  - make sure select the migrations.properties file 
  - click Okay to start the importation of the hook.
- this will create a "Dropbox API Integration" Organisation with the requisite artefacts needed to run the API.

#### Verify Import
- Expand the services folder in the Google Sheets API Hook you imported and find Dropbox API Integration VS

#### Activate Anonymous Contract
- Expand the contracts folder in the Google Drive API Integration you imported and find the "Anonymous" contract under the "Provided Contracts" folder
- click on the "Activate Contract" workflow activity in the righ-hand Activities portlet
- ensure that the status changes to "Workflow Is Completed"

#### Configure Security
- select the Dropbox API Integration -> Processes -> SaleForceOAuth process
    - select the "ConfigForAuthentication" script Activity, and change the value of the newQueryString variable to unclude your clientIS, username, and password
    - save the script activity
    - select the save process icon
- Ge the Dropbox authKey value, as per the DropBox API hook readme document

#### Verify Connectivity
- Using 
    curl -H "authKey:authkey value" -H "Content-Type: application/json" -d '{"FirstName":"Paul","LastName":"Pogo40","Company":"SOA","Street":"2962 Rosemary LN NE","City":"Rochester","State":"MN","PostalCode":"55906","Email":"paul40@soa.com"}' http://"ND HOST":"ND PORT"/leads (Make sure you use a unique value for both the Email and LastName values)
- The correct response should be:
    {"salesForceStatus":"Success","Dropbox":"Success"}
- Log in to your Dropbox account
- ensure that there is a "Leads" folder.
- open the "Leads" folder and ensure there is a "leads.txt" file
- Open that file, wait for the preview to generate the contents, and ensure that your lead posted in the curl request has been appended to the bottom of the file.

### License
Put a link to an open source license
