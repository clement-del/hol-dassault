# Activation

[home](README.md)

<h1>Audience activation</h1>
You will find 12 ready-to-activate published person-level audiences in the audience folder named "HOL" (HOL = Hands-On-Lab).<br>
Use the audiences named according to your login 01->A, 02->B, 03->C, etc.<br><br>

<img width="1720" alt="Screenshot 2026-01-28 at 15 27 57" src="https://github.com/user-attachments/assets/30d8f188-50fc-4346-a4aa-3d641945f26b" />

- When you wish to activate segments, you can activate one segment to a destination, or select a destination first, and pick all segments required for this destination.
- We will do the first method: first selecting the segment, and pick a destination.
- The destination for this exercice will be an S3 account.
- Depending on destinations, activation is streaming or batch.
- The process of the streaming/edge segment activated to a streaming destination is the following :
1. As soon a new dataflow arrives in AEP, the segment is evaluated in seconds/milliseconds and persons enter (or exit) the segment
2. An enter or exit in this segment automatically triggers the activation and the persons are propagated to (or removed from) the destination in seconds/milliseconds<br><br>

So let's activate an audience to our S3 account, a batch activation.<br>
- Select the right audience, click on "activate to destination"
- Select the "Demo S3 Destination (audiences)" destination
  
<img width="1719" alt="Screenshot 2026-01-28 at 15 55 14" src="https://github.com/user-attachments/assets/9ee04174-a2b8-479a-bffc-de9426a90920" />

- Click on Next
- Click on the schedule pencil, select "Export full files" and "Daily" at the time of your choice.
- Click next to see the mapping. This mapping is the mapping from the last execution to this destination. If you wish to add additional field to this destination, click on "Add new mapping", click on the arrow, type "address" in - the search bar and select the work email address for example.

<img width="1721" alt="Screenshot 2026-01-28 at 15 57 51" src="https://github.com/user-attachments/assets/e637d48c-8d81-4026-92d0-df11ca09987f" />

- Click on next, review your activation and click on finish to validate it.<br>

The activation process is similar for any destination.<br>

<h1>Dataset export (for technical users)</h1>
You can also export raw data from entire datasets instead of exporting segments with attributes.<br>
You can export system datasets, business datasets, or datasets you created thanks to Query Services for dedicated use cases.<br><br>

You will first create your own dataset export destination on a s3 account.
- Go to "Destinations", then "Catalog", filter on "S3".
- Click on the 3 dots, and click on "Configure new destination"

<img width="1720" alt="Screenshot 2026-01-28 at 15 59 38" src="https://github.com/user-attachments/assets/11aad57f-f600-4bff-bc3b-d024b9f5fa88" />

- Select an existing s3 account already configured on the environment
- Pick the "Dataset" data type instead of "Audiences"
- Put the following values
- Name : Demo S3 Destination [Datasets] + YOUR_TRIGRAM
- Bucket name : aepdemodestination
- Folder path : /aep-audiences/
- File type = JSON
- Compression format GZIP<br><br>

<img width="1717" alt="Screenshot 2026-01-28 at 16 00 57" src="https://github.com/user-attachments/assets/e5c72001-a9fb-4441-98bb-363c9ca101fc" />

Now that your destination for datasets export on S3 has been created, it is time to export your first datasets:
- Go to "Destinations", then "Browse", and click on the 3 dots on the line of the "Demo S3 Destination [Datasets] + TRIGRAM" destination.
- Click on "Export datasets"

<img width="1712" alt="Screenshot 2026-01-28 at 16 01 45" src="https://github.com/user-attachments/assets/c88f6c6d-8586-447b-abcb-79ddb57406e2" />

- Select for example "Demo System - B2B Account Dataset" and "Demo System - B2B Person Dataset", and click on "Next"
- Visualize folder path, scheduling options, and click on "Next" to see the final review.
- Click on "Finish" to validate the export on the cloud storage destination.
