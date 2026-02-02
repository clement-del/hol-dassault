[home](README.md)

# Data Distiller Overview

<img width="1559" alt="image" src="https://github.com/user-attachments/assets/be21e146-efd9-4add-897a-8d832d4d76e3" />

credentials


## Run Queries on your datasets
Datasets are easy to investigate, you can run any queries on your datasets using AEP UI
- Go to Data Management > Queries > Create Query
- Browse the different tables, you can filter b2b tables to view only the ones that are relevant for this exercise
- Unfold the _demo_system_b2b_opportunity_dataset_ to inspect the different attributes.
- You can click on the dataset name as well as the attribute name to paste them directly in the query editor
- Type (or copy/paste) the following request to look at the different values an opportunity can have:
```sql
SELECT DISTINCT opportunityStage FROM demo_system_b2b_opportunity_dataset;
```
- Click on the _Run Query_ button to execute the query
- After a couple of seconds, you should see the output
  
<img width="746"  alt="image" src="https://github.com/user-attachments/assets/ce6633e9-c77f-470f-847d-c0622ce78917" />

Now let's run more complex queries

### Account Concentration Analysis
This query identifies which accounts have the most opportunities. For Dassault, an account with many small opportunities might require a different marketing play (like a Consolidation campaign) than an account with one massive deal.

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
For this exercise, we will create an audience of "High-Value R&D Decision Makers": People in R&D departments at accounts with over $100k in the pipeline.
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

- After a few minutes, the audience appears in the audience portal (filter them by checking Data Distiller in the UI)

<img width="709"  alt="image" src="https://github.com/user-attachments/assets/a3179a7d-9b4b-469d-ac7e-e4c20c96472f" />

- You can now give a name to your query to save it as template, prefix it with your lab username, eg: `u01 High-Value R&D Decision Makers`
- Click _Save and Close_

## Schedule your queries
- The query template you created can now be scheduled to be refreshed periodically
- Click on Queries > Templates, select the line that correspond to your query.
- On the right hand side, click on _Add schedule_

<img width="317" height="211" alt="image" src="https://github.com/user-attachments/assets/0521646f-b509-4cde-bb78-509fec032fd4" />

- Configure your query to run every Sunday at 5 PM, until Feb 28th.

<img width="949" alt="image" src="https://github.com/user-attachments/assets/2033424f-bc50-4a52-98fb-c2185e179b3b" />

- Click _Save_


## Build dashboard



<br /><br />
Congratulations! You have completed the dataingestion chapter of the lab 👍 ✨, go to the [next step](segmentation.md) or return to the [home](README.md)
