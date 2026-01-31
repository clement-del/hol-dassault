[home](README.md)

# Data Modelling

A schema is a set of rules that represent and validate the structure and format of data. 
In addition to describing the structure of data, schemas apply constraints and expectations to data so it can be validated as it moves between systems. 

## B2B Data Model

Real-Time CDP B2B Edition provides several  XDM schema, classes,  field groups, and relationships types to capture and structure your data specifically for B2B purposes.
The following diagram provides an example of how the different B2B schemas can relate to each other in a standard implementation:

<img width="1280" alt="image" src="https://github.com/user-attachments/assets/9221b80c-0d4a-4473-b485-56d03279e170" />

## Review existing B2B Schemas

- Navigate to Schemas under Data Management.
- While on the Browse tab, type in B2B in the search box: It will display only B2B related schemas.

<img width="1280"  alt="image" src="https://github.com/user-attachments/assets/64b1be13-9296-4bd5-b7c4-cabc2aa23165" />

- Click on the B2B Person Schema to review the schema composition

<img width="895" alt="image" src="https://github.com/user-attachments/assets/18804ac8-1f47-49b8-b03b-b8a0e0418246" />


  - `Class` It represents the nature of the data that are instantiated with a schema.
    - Click on the Class  XDM Individual Profile to highlight fields contributed by that class. You can add more fields in a schema to specialize the base class. 


  - `Field Groups` They are reusable components that define data attributes which are allowed to be ingested through this schema.
    - Click on the XDM Business Person Details field group to highlight the B2B specific fields contributed by this out-of-the-box field group to the schema. You can remove fields from a field group if that are necessary for your business. 

    
  - `Identitites`: Identities are keys which are ingested into the ID graph to build a unified  representation of your B2B person and account profiles.
    - Click on workEmail.address identity to reveal to what identity namespace it relates.
      
<img width="343" height="95" alt="image" src="https://github.com/user-attachments/assets/ad9401d8-63ee-4640-8ad2-28c0ccba4b12" /><br />


  - `Relationships`: It describes how these business schemas relate to each other
    - Click on the different relationships listed and review the field used to connect the person schema to other schemas
    - Click on the View Relationship on the right panel to expose the cardinality of the relationships. Compare this to the B2B data model that was surfaced earlier

<img width="1280" alt="image" src="https://github.com/user-attachments/assets/8a45eefc-e6bb-4c73-a78b-6fd12a97f6c2" />

<img width="1280" alt="image" src="https://github.com/user-attachments/assets/9541ced7-35e6-452c-9ab8-4124e95da17f" /><br />


  - `Required fields`: It shows all the fields which are mandatory when ingesting a record into RTCDP. You can restrict the expected values through the use of enums. 

<img width="314"  alt="image" src="https://github.com/user-attachments/assets/1ff20b72-fc09-49b1-9464-3ab653528c59" /><br />





<br /><br />
Congratulations! You have completed the dataingestion chapter of the lab 👍 ✨, go to the [next step](datadistiller.md) or return to the [home](README.md)
