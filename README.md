# hol-dassault


Hello World !

You will have opportunity to play with the segment builder and manipulate different concepts.
Each segment has a focus on a dedicated segment builder capability - All capabilities can be combined in more complex segments if needed.

**Segment 1:** OK
This person-level audience is all about profile attributes

In the home page, under Customer, click on audiences, then create audience, build rule
Name your segment with "TRIGRAM-label"
Navigate to XDM Individual Profile / Work email / Address, drag and drop this attribute, select "Address exists"
Navigate to XDM Individual Profile / Work phone / Number, drag and drop this attribute to form a group (IMAGE), select "Number exists"
Type "Job title" in the attribute search bar, click on the information icon (IMAGE) to see the top items repartition (IMAGE), drag and drop the attribute, and select CEO, CFO, CTO
Refresh estimate and view profiles
Choose the evaluation method you need
Save the segment

**Segment 2:** OK
This person-level audience is all about events

In the home page, under Customer, click on audiences, then create audience, build rule
Name your segment with "TRIGRAM-label"
Go to the events tab, search for "page" in the search bar, drag and drop the "page views" event type
Click on "page views" in the "browse variables" section to add context to the "page views" event, select "today" instead of "any time"
Go to Web/Web page details and drag and drop the "page name" attribute in the "event rules" section, select name="product_X"
Check all the evaluation methods available for this segment

Go to the events tab, search for "form", drag and drop the "form filled out" event type on the right to the "page views" event type to define a sequential segmentation (IMAGE)
Clean the search bar
Click on "form filled out" in the "browse variables" section if you wish to add context in the "form filled out" event
Save the segment

**Segment 3:**
This person-level audience is about combining profiles and account attributes

In the home page, under Customer, click on audiences, then create audience, build rule
Type "Job title" in the attribute search bar, drag and drop the attribute, and select CEO, CFO, CTO
Clean the search bar, navigate to XDM Individual Profile/Person Component/Source Account key/Account/Account Organization/, drag and drop "Number of employees", select greater than 500

**Segment 4:**
Account-level audience

In the home page, under Accounts, click on audiences, then create audience
Name your segment with "TRIGRAM-label"
Click on XDM Business Account/Account Organization, drag and drop "Number of employees", select is greater than 500
Click on Opportunities/Opportunity amount/, drag and drop "Amount", select greater than 100000
Refresh estimate and view accounts
Click on Opportunities/, drag and drop "Expected close date", select in next 3 months

**Segment activation**
You will find already 12 ready-to-activate published person-level audiences in the audience folder named "HOL" (HOL = Hands-On-Lab).
Use the audiences named according to your login 01->A, 02->B, 03->C, etc.
Select an audience, click on "activate to destination"
Go to schedule, select "Export full files" and "Daily" at the time of your choice
Click next to see the mapping. This mapping is the default mapping associated to this destination. If you wish to add additional field to this destination, click on "Add new mapping", click on the arrow, type "address" in the search bar and select the work email address for example.
Click on next, review your activation and click on finish to validate it.

The activation process is similar for any destination.

**Dataset export (for technical users)**
You can also export raw data from entire datasets instead of segments with attributes.
You can export system datasets, business datasets, or datasets you created thanks to Query Services.
Go to "Destinations", then "Browse", and click on the 3 dots on the line of the "Demo S3 Destination [Datasets]" destination, then "Export datasets"
Select for example "Demo System - B2B Account Dataset" and "Demo System - B2B Person Dataset", and click on "Next"
Visualize folder path, scheduling options, and click on "Next" to see the final review.
Click Finish


