[home](README.md)

# Data Distiller Overview

<img width="1559" alt="image" src="https://github.com/user-attachments/assets/be21e146-efd9-4add-897a-8d832d4d76e3" />

AEP Data Distiller acts as the analytical engine that transforms raw, multi-dimensional data into actionable business intelligence. It lets you perform high-performance SQL queries across disparate datasets joining profiles, accounts, and opportunities to uncover insights that standard segmentation cannot reach. 
This allows marketing teams to calculate complex metrics, build audiences, enrich your real time customer profile and even build dashboard. You can use Data Distiller from your own data visualization tool such as PowerBI, Tableau or your AI & ML notebooks if you want. However, for this exercise, we're going to use AEP embedded query editor to start our data analysis.

## Run Queries on your datasets
Datasets are easy to investigate, you can run any queries directly within AEP: 
- Go to Data Management > Queries > Create Query
- Browse the different tables, you can filter b2b tables to view only the ones that are relevant for this exercise.
- Unfold the _demo_system_b2b_opportunity_dataset_ to inspect the different attributes.
- You can click on the dataset name as well as the attribute name to paste them directly in the query editor.
- Type (or copy/paste) the following request to look at the different values an opportunity can have:
  
```sql
SELECT DISTINCT opportunityStage FROM demo_system_b2b_opportunity_dataset;
```
- Click on the _Run Query_ button to execute the query
- After a couple of seconds, you should see the output
  
<img width="746"  alt="image" src="https://github.com/user-attachments/assets/ce6633e9-c77f-470f-847d-c0622ce78917" />

Now let's run more complex queries

### Account Concentration Analysis
This query identifies which accounts have the most opportunities. For Dassault, an account with many small opportunities might require a different marketing play (like a consolidation campaign) than an account with one massive deal.

```sql
SELECT 
    acc.accountName,
    COUNT(opp.opportunityID) AS total_opportunities,
    SUM(opp.expectedRevenue.amount) AS total_pipeline_value,
    ROUND(AVG(opp.expectedRevenue.amount), 2) AS avg_deal_size,
    MAX(opp.probabilityPercentage) AS highest_probability
FROM demo_system_b2b_account_dataset acc
JOIN demo_system_b2b_opportunity_dataset opp 
    ON acc.accountKey.sourceKey = opp.accountKey.sourceKey
GROUP BY acc.accountName
HAVING COUNT(opp.opportunityID) > 1
ORDER BY total_pipeline_value DESC
```

### Buying Center Completeness
One of the most advanced B2B marketing needs is knowing if you have a full house of contacts. This query aggregates the number of contacts per account and identifies "at-risk" accounts where there is a high-value opportunity but fewer than 6 contacts identified in the system.

```sql
SELECT 
    acc.accountName,
    SUM(opp.expectedRevenue.amount) AS pipeline_at_risk,
    COUNT(DISTINCT p._id) AS contact_count,
    COLLECT_LIST(DISTINCT p.extendedWorkDetails.jobTitle) AS identified_titles
FROM demo_system_b2b_account_dataset acc
JOIN demo_system_b2b_opportunity_dataset opp 
    ON acc.accountKey.sourceKey = opp.accountKey.sourceKey
LEFT JOIN demo_system_b2b_person_dataset p 
    ON acc.accountKey.sourceKey = p.b2b.accountKey.sourceKey
  GROUP BY acc.accountName
HAVING contact_count < 10 AND SUM(opp.expectedRevenue.amount) > 100000
ORDER BY pipeline_at_risk DESC
```

## Create audiences with SQL
We are now going to create an audience of "High-Value R&D Decision Makers": People in R&D departments at accounts with over $100k in the pipeline.

```sql
CREATE audience delaland_3ds_hv_rd_pipeline WITH (primary_identity=email, identity_namespace=email) AS (
SELECT
  p.workemail.address AS email
FROM
  demo_system_b2b_person_dataset p
  JOIN demo_system_b2b_account_dataset acc ON p.b2b.accountKey.sourceKey = acc.accountKey.sourceKey
  JOIN demo_system_b2b_opportunity_dataset opp ON acc.accountKey.sourceKey = opp.accountKey.sourceKey
WHERE
  p.extendedWorkDetails.departments[0] = 'Research and Development'
  AND opp.expectedRevenue.amount > 100000
  AND p.consents.marketing.email.val = 'y'
GROUP BY
  p.b2b.personKey.sourceKey, email)
```

- You can now give a name to your query to save it as template, prefix it with your lab username, eg: `u01 High-Value R&D Decision Makers`
- Click _Save and Close_
- After a few minutes, the audience appears in the audience portal (filter them by checking Data Distiller in the UI)
- 
<img width="709"  alt="image" src="https://github.com/user-attachments/assets/a3179a7d-9b4b-469d-ac7e-e4c20c96472f" />

- Your audience is now materialized and can be activated across the destination catalog

<img width="699" height="189" alt="image" src="https://github.com/user-attachments/assets/cd7568bd-c787-4853-968d-d833a9608098" />


## Schedule your queries
- The query template you created can  be scheduled to be refreshed periodically
- Click on Queries > Templates, select the line that correspond to your query.
- On the right hand side, click on _Add schedule_

<img width="317" height="211" alt="image" src="https://github.com/user-attachments/assets/0521646f-b509-4cde-bb78-509fec032fd4" />

- Configure your query to run every Sunday at 5 PM, until Feb 28th.

<img width="949" alt="image" src="https://github.com/user-attachments/assets/2033424f-bc50-4a52-98fb-c2185e179b3b" />

- Click _Save_
- Now, every week your audience will be refreshed with up to data data, so that you can fully automate the nurturing process for your key accounts. 


## Leverage analytics dashboards
Data Distiller Templates provide a set of powerful dashboards designed to help you gain insights into your audience data. To help you make data-driven decisions and improve targeting strategies, each template offers a structured guide for analyzing specific aspects of audience behavior, segmentation, and identity management.

- Go to _Dashboard_ menu, then select the _Templates_ tab

<img width="1114"  alt="image" src="https://github.com/user-attachments/assets/07ee53d8-4d0b-440c-9a92-e8b6d015f353" />

- Click on Audience Comparison to access the dashboard. It compares key audience metrics in a side-by-side view. From this dashboard, you can perform a variety of actions to contrast two audience groups and analyze key metrics between them. You can then make data-driven decisions regarding audience segmentation and targeting strategies.
- Click on the _Filter_ icon to select the audiences you'd like to compare. We are going to select the following audiences:
- `Audience A: HOL - Audience contactability - A` and `Audience B: HOL - Audience job title - A`
- Select _Today_ as date filtering criteria
- Click _Apply_
- you should now see the audience comparison dahsboard updated, reflecting key metrics about your audience, helping you analyze their differences and trend over time.

  <img width="1555" alt="image" src="https://github.com/user-attachments/assets/680a4c31-9764-4180-a0ab-8a3ca777f66d" />

You can also build your own dashboard using Data Distiller to share key insights about your audiences and B2B opportunities within AEP, but that would be for a future hands-on session :) 

<br /><br />
Congratulations! You have completed the data distiller chapter of the lab 👍 ✨, go to the [next step](segmentation.md) or return to the [home](README.md)
