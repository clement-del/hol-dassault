# hol-dassault

<h1>SEGMENTATION</h1>
You will have opportunity to play with the segment builder and manipulate different concepts.<br>
Each segment has a focus on a dedicated segment builder capability.<br>
All capabilities can be combined in more complex segments if needed.
<br><br>

**Audience 1**<br>
Attributes, events, and existing audiences can be combined in segment definition. This first person-level audience is about profile attributes only. 

- In the home page, under Customer, click on audiences, then create audience, build rule
  
<img width="1720" height="895" alt="Screenshot 2026-01-28 at 14 37 05" src="https://github.com/user-attachments/assets/0383f736-db86-49c1-a1ef-d5a3eb5c8106" />
 
- Please respect this segment label policy for this session "YOUR_TRIGRAM + label"
- Navigate to XDM Individual Profile / Work email / Address, drag and drop this attribute, select "Address exists"
- Navigate to XDM Individual Profile / Work phone / Number, drag and drop this attribute to form a group, and select "Number exists"
  
<img width="1728" height="1117" alt="Screenshot 2026-01-28 at 14 39 22" src="https://github.com/user-attachments/assets/82b8ee02-5073-4204-a839-348d52da0729" />

- Click on Refresh estimate, and "view profiles". The attributes used in the segmentation are the last columns displayed
  
<img width="1724" height="906" alt="Screenshot 2026-01-28 at 14 40 30" src="https://github.com/user-attachments/assets/0bec9916-d774-4e32-a216-101ff2befae3" />

- Click on "Hide profiles"
- Type "Job title" in the attribute search bar, click on the information icon (IMAGE) to see the top items repartition

<img width="1722" height="909" alt="Screenshot 2026-01-28 at 14 41 36" src="https://github.com/user-attachments/assets/830a18f2-0e61-4503-8007-f9ec60a80989" />

- Drag and drop the job title attribute, and select CEO, CFO, CTO thanks to the drop down list
- Refresh estimate
- Use an "OR" operator in the first container, and refresh estimate

<img width="1725" height="906" alt="Screenshot 2026-01-28 at 14 43 48" src="https://github.com/user-attachments/assets/b09e1f9e-2b69-4895-9547-1173c1e0b306" />

- Click on "view profiles", and visualize the new columns on the right
- Choose the evaluation method you need. When your segment only contains person attributes, all the evaluation methods are available.
  
<img width="1721" height="904" alt="Screenshot 2026-01-28 at 14 46 37" src="https://github.com/user-attachments/assets/348ba83c-c559-408b-b77d-caa280632983" />

- Save the segment
- For your segment to be evaluated by the audience job and available for activation, you may publish it.

**Audience 2**<br>
Attributes, events, and existing audiences can be combined in segment definition. This second person-level audience is about events.

- In the home page, under Customer, click on audiences, then create audience, build rule
- Go to the events tab, search for "page" in the search bar, drag and drop the "page views" event type

<img width="1721" height="905" alt="Screenshot 2026-01-28 at 14 55 05" src="https://github.com/user-attachments/assets/2270789a-4206-47ae-8880-c6ad35fe00c1" />

- Select "today" instead of "any time" for the event you chose

<img width="1715" height="893" alt="Screenshot 2026-01-28 at 14 57 07" src="https://github.com/user-attachments/assets/53e2568c-d358-4900-b539-9f9c1856d50a" />

- Clear the search bar
- To add additional context to the "page views" event, click on "page views" in the "browse variables" section
- Go to Web/Web page details and drag and drop the "name" attribute in the "event rules" section

<img width="1728" height="1117" alt="Screenshot 2026-01-28 at 14 58 04" src="https://github.com/user-attachments/assets/edde57fc-a6ab-430b-b42d-7bb31083c18e" />

- Select name="Product_X"
- Check all the evaluation methods available for this segment. Combining as many profile attributes and one event in a 24 hours timeframe allows all evaluation methods.

<img width="1720" height="909" alt="Screenshot 2026-01-28 at 14 59 20" src="https://github.com/user-attachments/assets/f0efd712-5eaa-46b6-8021-5903c08e3c05" />

- Go to the events tab, search for "form fill", drag and drop the "form filled out" event type on the right to the "page views" event type to define a sequential segmentation

<img width="1723" height="897" alt="Screenshot 2026-01-28 at 15 00 52" src="https://github.com/user-attachments/assets/4b0fb1ca-89e9-4c33-b6c9-8df29de10e15" />

- Clean the search bar
- Click on "form filled out" in the "browse variables" section if you wish to add context in the "form filled out" event
- Save the segment
- Check evaluation methods available. The edge segmentation method is not available anymore. As it must segment in less than 250ms for web personalization use cases, the edge evaluation method is not available when several events are added as segmentation criteria.

<img width="1722" height="901" alt="Screenshot 2026-01-28 at 15 03 15" src="https://github.com/user-attachments/assets/a311ba11-737f-4278-8c6e-0dc92c96651f" />

Combining a batch segment in a streaming/edge segment is a way to ensure on-time evaluation for the most important criteria of your use cases.

**Audience 3**<br>
This person-level audience is about combining profiles and account attributes.

- In the home page, under Customer, click on audiences, then create audience, build rule
- Type "Job title" in the attribute search bar, drag and drop the attribute, and select CEO
- Clean the search bar, navigate to XDM Individual Profile/Person Component/Source Account key/Account/Account Organization/, drag and drop "Number of employees", select greater than 20000

<img width="1720" height="904" alt="Screenshot 2026-01-28 at 15 06 14" src="https://github.com/user-attachments/assets/59d57fbb-aebd-406b-87f7-a0f3662cea97" />

- Refresh estimate and view profiles to check the results are fine
- Check the evaluation method. Only batch evaluation method is available. This is a normal behaviour, when adding account attributes in a person-level audience, it only allows batch evaluation.

<img width="1722" height="902" alt="Screenshot 2026-01-28 at 15 10 16" src="https://github.com/user-attachments/assets/745d785e-2130-48fe-8a9b-ffc521c717c1" />

- To bypass this work by design behaviour that guarantees segment evaluation performance, we will do the same segment differently. Take off the "number of employees" attribute in the segment definition.
- Go to audience tab in the segment definition screen, click on "Experience Platform" to see the list of published audiences. (Audiences might be available from other sources in customers implementation).
- Drag and drop the "Bodea - Companies above 20k employees" person-level batch audience.
- Refresh estimate - Visualize the same volume as before.

<img width="1719" height="906" alt="Screenshot 2026-01-28 at 15 15 29" src="https://github.com/user-attachments/assets/91a08263-7199-4c18-8315-04827fb7a764" />

- Check the evaluation method available, and select streaming segmentation. This time, with a different segmentation logic combining a batch segment within a streaming segment, this segment will be evaluated in seconds as soon as new data arrives within Adobe Experience Platform.
  
<img width="1718" height="903" alt="Screenshot 2026-01-28 at 15 16 12" src="https://github.com/user-attachments/assets/1e350c7a-f51b-4e4c-83d5-ecc07f96d4ba" />

**Audience 4**<br>
This time we will not create person-level audiences that target persons, but an account-level audience that will target accounts. LinkedIn for example allows to send person-level audiences OR account-level audiences depending on use cases. Some destinations in the B2B industry can only receive account-level audiences.

- In the home page, under Accounts on the left rail, click on audiences, then create audience
- Name your segment with "TRIGRAM-label"
- Click on XDM Business Account/Account Organization, drag and drop "Number of employees", select is greater than 500
- Come back on the main segmentation screen by clicking on "attributes", cf below screenshot:

<img width="1716" height="903" alt="Screenshot 2026-01-28 at 15 25 00" src="https://github.com/user-attachments/assets/cf5f0268-b096-49ba-9b8b-3b4e1b3cfa3e" />

- Click on Opportunities/Opportunity amount/, drag and drop "Amount", select greater than 10000
- Click on Opportunities/, drag and drop "Expected close date", select in next 3 months

<img width="1718" height="905" alt="Screenshot 2026-01-28 at 15 26 40" src="https://github.com/user-attachments/assets/3ecc35e9-24ba-4629-95db-c0ae0818260a" />

- Refresh estimate and view accounts, same mechanisms apply as for person-level audiences
- Please note that account audiences are only evaluated in batch mode

<h1>Audience activation</h1>
You will find 12 ready-to-activate published person-level audiences in the audience folder named "HOL" (HOL = Hands-On-Lab).<br>
Use the audiences named according to your login 01->A, 02->B, 03->C, etc.<br><br>

<img width="1720" height="899" alt="Screenshot 2026-01-28 at 15 27 57" src="https://github.com/user-attachments/assets/30d8f188-50fc-4346-a4aa-3d641945f26b" />

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
<img width="1719" height="907" alt="Screenshot 2026-01-28 at 15 55 14" src="https://github.com/user-attachments/assets/9ee04174-a2b8-479a-bffc-de9426a90920" />


- Go to schedule, select "Export full files" and "Daily" at the time of your choice
- Click next to see the mapping. This mapping is the default mapping associated to this destination. If you wish to add additional field to this destination, click on "Add new mapping", click on the arrow, type "address" in - the search bar and select the work email address for example.
- Click on next, review your activation and click on finish to validate it.<br>

The activation process is similar for any destination.<br>

<h1>Dataset export (for technical users)</h1>
You can also export raw data from entire datasets instead of segments with attributes.
You can export system datasets, business datasets, or datasets you created thanks to Query Services.<br><br>

You will create your own dataset export destination on a s3 account.
- Go to "Destinations", then "Catalog", filter on "S3".
- Click on the 3 dots, and click on "Configure new destination"
- Select an existing s3 account already configured on the environment
- Pick the "Dataset" data type instead of "Audiences"
- Put the following values
- Name : "Demo S3 Destination [Datasets] + YOUR_TRIGRAM"
- Bucket name : "aepdemodestination"
- Folder path : "/aep-audiences/"
- File type = JSON
- Compression format GZIP<br><br>

Now that your destination for datasets export on S3 has been created, it is time to export your first datasets:
- Go to "Destinations", then "Browse", and click on the 3 dots on the line of the "Demo S3 Destination [Datasets]" destination.
- Click on "Export datasets"
- Select for example "Demo System - B2B Account Dataset" and "Demo System - B2B Person Dataset", and click on "Next"
- Visualize folder path, scheduling options, and click on "Next" to see the final review.
- Click on "Finish" to validate the export on the cloud storage destination.


