# hol-dassault

<h1>SEGMENTATION</h1>
You will have opportunity to play with the segment builder and manipulate different concepts.<br>
Each segment has a focus on a dedicated segment builder capability.<br>
All capabilities can be combined in more complex segments if needed.
<br><br>

**Audience 1**<br>
This person-level audience is about profile attributes

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
This person-level audience is about events

- In the home page, under Customer, click on audiences, then create audience, build rule
- Go to the events tab, search for "page" in the search bar, drag and drop the "page views" event type
- Click on "page views" in the "browse variables" section to add context to the "page views" event, select "today" instead of "any time"
- Go to Web/Web page details and drag and drop the "page name" attribute in the "event rules" section, select name="product_X"
- Check all the evaluation methods available for this segment
- Go to the events tab, search for "form", drag and drop the "form filled out" event type on the right to the "page views" event type to define a sequential segmentation (IMAGE)
- Clean the search bar
- Click on "form filled out" in the "browse variables" section if you wish to add context in the "form filled out" event
- Save the segment

When adding events or additional dimensions, it might depend on the number of events, timeframe used for events, additional dimensions, etc. Combining a batch segment in a streaming segment is a way to ensure real-time evaluation of the most important criteria.

**Audience 3**<br>
This person-level audience is about combining profiles and account attributes

- In the home page, under Customer, click on audiences, then create audience, build rule
- Type "Job title" in the attribute search bar, drag and drop the attribute, and select CEO, CFO, CTO
- Clean the search bar, navigate to XDM Individual Profile/Person Component/Source Account key/Account/Account Organization/, drag and drop "Number of employees", select greater than 500

**Audience 4**<br>
Account-level audience

- In the home page, under Accounts, click on audiences, then create audience
- Name your segment with "TRIGRAM-label"
- Click on XDM Business Account/Account Organization, drag and drop "Number of employees", select is greater than 500
- Click on Opportunities/Opportunity amount/, drag and drop "Amount", select greater than 100000
- Refresh estimate and view accounts
- Click on Opportunities/, drag and drop "Expected close date", select in next 3 months

<h1>Audience activation</h1>
You will find 12 ready-to-activate published person-level audiences in the audience folder named "HOL" (HOL = Hands-On-Lab).<br>
Use the audiences named according to your login 01->A, 02->B, 03->C, etc.<br><br>

- Select an audience, click on "activate to destination"
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


