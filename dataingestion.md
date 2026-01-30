[home](README.md)

---
# File Ingestion 

In this first exercise, we are going to ingest a call center data file into RTCDP. 
- Download the file and save it locally.
- Go to Connections > Sources > Catalog, then select _local file upload_.

label your datasetname uXX-EventDatasetforCallCenter , replace XX with your user number

label your dataflow uXX-EventDatasetforCallCenter,

No need to enable the dataset for profile for now

<img width="833" height="971" alt="image" src="https://github.com/user-attachments/assets/bba94bea-0107-4ff3-bca8-3882ce721121" />



Select Events_Call_Center.csv 

<img width="1735"  alt="image" src="https://github.com/user-attachments/assets/5fe12b8c-a060-4a5e-9dd5-b657699015d4" />

<img width="1841" alt="image" src="https://github.com/user-attachments/assets/7120b8ba-b26d-48eb-a9cf-a8336824a6d0" />



add calculated field  to map the callId field with the _id attribute

<img width="1593"  alt="image" src="https://github.com/user-attachments/assets/12170c1a-70bf-4cda-aa98-7c08184d3e48" />


validate

<img width="111"  alt="image" src="https://github.com/user-attachments/assets/3ca12cbf-e9d9-4355-a68f-47c22f5a2710" />


<img width="1040"  alt="image" src="https://github.com/user-attachments/assets/caeea408-2296-45f7-9840-aab2e37ec88d" />


Check data ingestion process. 

Click on Target Dataset > Preview Dataset


# API Streaming Exercise

Filter the Source Connector from the catalog (look for http)

Click Add Data

<img width="357" alt="image" src="https://github.com/user-attachments/assets/43ef2628-5074-4462-b49d-0fd4bc17df61" />


Select Existing Account

Select Dassault Streaming Endpoint

<img width="1029"  alt="image" src="https://github.com/user-attachments/assets/edf8f4f3-60e4-4f28-a4c4-4b16351dd3fc" />


Copy in your notepad the Streaming Endpoint url, you’ll need it after to test the end to end ingestion process

Click Next 

Upload the dassault-event-payload-search.json file

<img width="1051"  alt="image" src="https://github.com/user-attachments/assets/b69ff2ae-dd5b-4b22-9466-022282541c2c" />


Click Next

Select Existing Dataset: look for Demo System - Event Dataset for User ID (Global v1.1) 

<img width="1027"  alt="image" src="https://github.com/user-attachments/assets/f8a66ed5-5a28-4bec-addc-79a0fbc287b7" />


add following calculated fields: 

targetfield ‘producedBy’, map it to your user name so that we know who ingested the data

_id

timestamp

search.keywords

<img width="1175" alt="image" src="https://github.com/user-attachments/assets/a92fba5c-e23a-40ad-93ea-c9558c5b05fb" />

<img width="2048" alt="image" src="https://github.com/user-attachments/assets/218313da-083d-40a2-bc00-831ab0dcbe12" />


Retrieve the dataflow ID from the dataflow UI

<img width="303"  alt="image" src="https://github.com/user-attachments/assets/8fb42d94-1b19-4d2d-8422-2d6c216b71ec" />


Connect to the Streaming Segmentation Simulation, this is a htttp client we use to send data to RTCDP 

Add your streaming endpoint and dataflowid, type your email address

click invoke HTTP Client

<img width="843"  alt="image" src="https://github.com/user-attachments/assets/bcccc4dd-93b2-484b-93e5-2d2c67c67f51" />


Look for your user under Customer > Profiles, use the identity namespace Demo System - User ID

<img width="1003" alt="image" src="https://github.com/user-attachments/assets/7084882f-b218-4cab-821c-b50325710e41" />


Look for the audience membership tab to see your newly qualified profile

 

<img width="1261"  alt="image" src="https://github.com/user-attachments/assets/94849f23-d443-4809-8f6e-3906cebbca9d" />


Click the audience name to look at the details of the created audience

<img width="1010" alt="image" src="https://github.com/user-attachments/assets/e4394039-e761-4c4f-9b5f-df0e641515f3" />


<img width="2306"  alt="image" src="https://github.com/user-attachments/assets/be67aa7a-4185-4dad-b359-e50090b8f768" />


<br /><br />
Congratulations! You have completed the dataingestion chapter of the lab 👍 ✨, go to the [next step](datamodel.md) or return to the [home](README.md)
