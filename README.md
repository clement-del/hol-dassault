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

**Segment 3:** KOOOOO
This person-level audience is about combining profiles and account attributes

In the home page, under Customer, click on audiences, then create audience, build rule
Type "Job title" in the attribute search bar, drag and drop the attribute, and select CEO, CFO, CTO
Clean the search bar, navigate to XDM Individual Profile/Person Component/Source Account key/????

**Segment 4:** KOOOOO
Account-level audience

In the home page, under Accounts, click on audiences, then create audience
Name your segment with "TRIGRAM-label"
Click on XDM Business Account/Account Organization, drag and drop "Number of employees", select is greater than 500
Click on Opportunities/Opportunity amount/, drag and drop "Amount", select greater than 100000
Refresh estimate and view accounts
Click on Opportunities/, drag and drop "Expected close date", select in next 3 months




