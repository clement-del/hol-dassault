[home](README.md)

# Data Ingestion
Adobe RTCDP facilitates data ingestion from assorted sources  where it can be accessed, used, and analyzed by an organization. Data ingestion can be grouped into two main categories: batch ingestion and streaming ingestion

<div align="center">
<img width="50%" alt="image" src="https://github.com/user-attachments/assets/e5fe8870-64e6-4bf8-8605-7391b1cd4a98" /><br />
<i>an overview of source and activation dataflows in RTCDP</i>
</div>

---
## Batch Ingestion 

In this first exercise, we are going to ingest data from a call center data into RTCDP. It will be used to complete the 360° profile of your customers, and can later be used for segmentation, activation and analysis purposes. 
The file contains phone numbers from customers, a timestamp and call details (call reason, comments from the call agent, call resolution status etc). Those interaction data will be stored in a specific dataset that you're going to create.
Ingesting offline data is made easy through the use of dedicated source connectors. They can be pulled from sftp or cloud storage location with dedicated connector. For this lab, we're going to upload the file manually in RTCDP UI, so that you have full control over the end to end process.

- [Download the file](Events_Call_Center.csv  "download") and save it locally.
- Go to Connections > Sources > Catalog.
- Browse the different category, under _Local system_, you should find _local file upload_
- Click _Add data_ to start the 3 step wizard.


<br /><br /><b>Dataflow details step</b>
- In dataset details, select _New Dataset_.
- Label your dataset name _uXX-EventDatasetforCallCenter_, where XX with your user number from the user that has been assigned to you.
- Optionally, you can add a description, such as _Customer Service Events for 2025_.
- Select the schema that represents the kind of data you'd want to store. The schema that store interaction data from call center has already been created for you. Select the schema named `Demo System - Event Schema for Call Center (Global v1.1)`.
- No need to enable the dataset for profile for this exercise.
- Enable partial ingestion, and define a treshold from which the entirety of the file will be rejected.
- Label your dataflow _uXX-EventDatasetforCallCenter_.
- Once you have configured the following setup, click _Next_.

<img width="833" alt="image" src="https://github.com/user-attachments/assets/bba94bea-0107-4ff3-bca8-3882ce721121" />


<br /><br /><b>Select data step</b>
- Drag and drop the Events_Call_Center.csv file.
- RTCDP guesses the file format automatically.
- Look at the sample data shown as preview.
- click _Next_.

<img width="1735"  alt="image" src="https://github.com/user-attachments/assets/5fe12b8c-a060-4a5e-9dd5-b657699015d4" />



<br /><br /><b>Mapping step</b>
- RTCDP tries to find the best mapping between the csv columns of the file and your selected data schema
- You can alter the mapping to update it, add new columns or remove unnecessary ones
<img width="1841" alt="image" src="https://github.com/user-attachments/assets/7120b8ba-b26d-48eb-a9cf-a8336824a6d0" />

- add calculated field  to map the callId field with the _id attribute

<img width="1593"  alt="image" src="https://github.com/user-attachments/assets/12170c1a-70bf-4cda-aa98-7c08184d3e48" />

- Click Validate <img width="111"  alt="image" src="https://github.com/user-attachments/assets/3ca12cbf-e9d9-4355-a68f-47c22f5a2710" /> to check if there are any pending issues.
- Your data ingestion flow is now complete, - click _Finish_.
- You can now seethe dataflow activity details and check how many records get ingested.
 
<img width="1040"  alt="image" src="https://github.com/user-attachments/assets/caeea408-2296-45f7-9840-aab2e37ec88d" />

- Click on Target Dataset > Preview Dataset to inspect the records within RTCDP datasets.

Through 3 simple steps, you were able to bring data in RTCDP, there's plenty of additional options available to manage errors, retries, schedules ingestion etc. Let's now look at streaming ingestion process. 

## Streaming Ingestion

In this second exercise, we are going to setup a HTTP streaming ingestion endpoint that will receive  json data from your back end system. This is particularly useful when you have to segment and activate customer data in real-time. Common use case are: apply personalized content on your website based on customer interactions, or trigger a request for call back to your sales team. 
In our case, we're going to use an incoming event (a web search containing specific keyworks such as Catia) to segment our customer in real-time.

- Go to Connections > Sources > Catalog.
- Browse the different category, under _Streaming_, you should find _HTTP API_
- Click _Add data_ to start the 5 steps wizard.

<img width="357" alt="image" src="https://github.com/user-attachments/assets/43ef2628-5074-4462-b49d-0fd4bc17df61" />


<br /><br /><b>Authentication step</b>
- You have the option to either use a new account or use an existing one. An account carries the authentication mechanism (oAuth2 credentials). Let's use a predefined account for this exercise.
- Click _Existing Account_.
- Select _Dassault Streaming Endpoint_.

<img width="1029"  alt="image" src="https://github.com/user-attachments/assets/edf8f4f3-60e4-4f28-a4c4-4b16351dd3fc" />

- Click Next 

<br /><br /><b>Select data step</b>
- [Download the dassault-event-payload-search.json](dassault-event-payload-search.json  "download"). It contains a sample payload describing the structure of the interaction that is created when a user makes a search on a webiste. It usually comes from your datalayer or your backend system. 
- Now, let's upload the dassault-event-payload-search.json to describe the  input that will be expected.
- You can preview the sample data on the right hand side. 

<img width="1051"  alt="image" src="https://github.com/user-attachments/assets/b69ff2ae-dd5b-4b22-9466-022282541c2c" />


- Click Next

<br /><br /><b>Dataflow detail step</b>
- In dataset details, select _Existing dataset_.
- Select the dataset that will store those interactions: `Demo System - Event Dataset for User ID (Global v1.1)`.
- Make sure the dataset is Profile enabled.
- Label your dataflow _uXX-EventDatasetforAPISource dataflow_.
- Once you have configured the following setup, click _Next_.

<img width="1027"  alt="image" src="https://github.com/user-attachments/assets/f8a66ed5-5a28-4bec-addc-79a0fbc287b7" />

<br /><br /><b>Mapping step</b>
- RTCDP tries to find the best mapping between the json payload of the request and your selected dataset. You can alter the mapping to update it, add new columns or remove unnecessary ones.
- Let's add following calculated fields to enrich our record with additional details.
  - First we want to store who ingested the data, to do so we are going to map our user name to the _producedBy_ attribute of the schema.
    - Click _New field type_ button, then select _Add calculated field_.
    - The data prep window appears, let's add the name of our user (like `'user01'`), dont forget the surrounding quotes !. Click _Save_.
    - Click _Map target field_, select _producedBy_.
 - Then, let's call a function that will generate a unique id for each of our interactions and map it to the __id_ attribute of the schema.
    - Click _New field type_ button, then select _Add calculated field_.
    - The data prep window appears, under function tab, let's look for the _uuid()_ function. Click the + sign to add it. Click _Save_.
    - Click _Map target field_, select __id_.
  - Now, let's call a function that will add a timestamp for each of our interactions and map it to the _timestamp_ attribute of the schema.
    - Click _New field type_ button, then select _Add calculated field_.
    - The data prep window appears, under function tab, let's look for the _now()_ function. Click the + sign to add it. Click _Save_.
    - Click _Map target field_, select _timestamp_.
   - Map _email_ source field to _userAccountID_.
    - Click _New field type_ button, then select _Add new field_.
    - select _email_, then click _select_
    - under target fields, search for _userAccount_, expand the node and select _ID_
   - Map _websearch_ source field to _search.keywords_.
    - Click _New field type_ button, then select _Add new field_.
    - select _websearch_, then click _select_
    - under target fields, search for _keyword_, expand the node and select _keywords_
     
- Click Validate to ensure your mapping is correct. You should end up with the following mapping: 

<img width="1175" alt="image" src="https://github.com/user-attachments/assets/a92fba5c-e23a-40ad-93ea-c9558c5b05fb" />

- Click _Next_.

<br /><br /><b>Review step</b>
- This is the final step of the wizard. Click Finish if you're happy with the setup.
  
<img width="2048" alt="image" src="https://github.com/user-attachments/assets/218313da-083d-40a2-bc00-831ab0dcbe12" />

<br /><br /><b>Dataflow detail page</b>
- Click on your newly created dataflow, on the right hand rail, under API Usage you should see the streaming endpoint url and the dataflowID. Those information are required to test the streaming ingestion. 

<img width="303"  alt="image" src="https://github.com/user-attachments/assets/8fb42d94-1b19-4d2d-8422-2d6c216b71ec" />

<br /><br /><b>Testing the streaming segmentation</b>
- Open the <a href="https://1246593-apiauto-stage.adobeio-static.net/index.html#/http-client" target="_blank">Streaming Segmentation Tester</a>. This is a htttp client we use to send data to RTCDP 
- Paste the streaming endpoint URL and the dataflowID from the previous step into their respective fields.
- Enter your user email address.
- Click invoke HTTP Client.
- You should see in the response a confirmation your request has been sent to the streaming endpoint. Behind the scene the request will and in Adobe Kafka pipeline that will segment in real time our user (as defined by the email identity). 


<br /><br /><b>Lookup Profile Details</b>


<img width="843"  alt="image" src="https://github.com/user-attachments/assets/bcccc4dd-93b2-484b-93e5-2d2c67c67f51" />


Look for your user under Customer > Profiles, use the identity namespace Demo System - User ID
- Go back to RTCDP browser window, under Customer > Profile menu, select the browse tab and look for the email address you used in the simulator. 
- Make sure you use _Default Timebased_ Merge Policy and _Demo System - User ID_ Identity namespace.
- Click _View_.
  
<img width="1003" alt="image" src="https://github.com/user-attachments/assets/7084882f-b218-4cab-821c-b50325710e41" />


- Under Audience membership tab, you should see your profile qualified for the _3DS - Interested in CATIA_ audience.
  
<img width="1261"  alt="image" src="https://github.com/user-attachments/assets/94849f23-d443-4809-8f6e-3906cebbca9d" />

- Click the audience name to look at the details of the created audience

<img width="1010" alt="image" src="https://github.com/user-attachments/assets/e4394039-e761-4c4f-9b5f-df0e641515f3" />


<br /><br />
Congratulations! You have completed the dataingestion chapter of the lab 👍 ✨, go to the [next step](datamodel.md) or return to the [home](README.md)
