[home](README.md)

<h1>REAL-TIME PROFILE EXAMPLE</h1>

This section aims at understanding the concepts of real-time profile, identities and datasets merging with a concrete example.<br>

A first CRM dataset is feeding Adobe Experience Platform. Let's see one profile called Bobby: <br>

<img width="1299" alt="Screenshot 2026-02-02 at 09 34 46" src="https://github.com/user-attachments/assets/f4bb40f8-0330-451f-971f-fad1fa3d059e" />

- The different identities of this dataset enable the identity graph to be initiated.
- The merged profile only contains for now information from this dataset.

A second Loyalty dataset is now feeding AEP:

<img width="1300" alt="Screenshot 2026-02-02 at 09 36 11" src="https://github.com/user-attachments/assets/9a304d42-25ac-42cf-9082-0f2f48aed56a" />

- The identity graph is enriched as the customer's life progresses, in this case through interaction with the loyalty system and Loyalty ID. A new identity is linked to Bobby's profile.
- The datasets are merged according to merge policies: in this case, the CRM dataset takes priority over the Loyalty dataset, so the “Name” field is not updated in the merged profile.

An Experience event dataset contributes to building the profile.

<img width="1297" alt="Screenshot 2026-02-02 at 09 36 49" src="https://github.com/user-attachments/assets/5fd989bb-fe50-4759-ac94-37fa3a66570a" />

- A new web ID has been added to the profile: a first-party cookie.

Calling a call center automatically enriches the profile record in real time with an event:

<img width="1295" alt="Screenshot 2026-02-02 at 09 37 19" src="https://github.com/user-attachments/assets/07b72fef-89e9-44a0-8c7e-df69560b76c7" />

<h1>REAL-TIME PROFILE IN AEP UI</h1>

Go to Customer/Profiles/Browse, and click on "View" on a random profile widget

<img width="1722" height="906" alt="Screenshot 2026-02-02 at 09 42 45" src="https://github.com/user-attachments/assets/4d393887-bdf0-48aa-9b9d-ffa8a07fa016" />

Explore this section, and see for example the identity graph:

<img width="1722" height="905" alt="Screenshot 2026-02-02 at 09 45 42" src="https://github.com/user-attachments/assets/ddd4dd84-8f07-4c5e-bb27-86d03b2b955a" />

And the experience events timeline showing all useful interactions a contact has had with your company:

<img width="1718" height="901" alt="Screenshot 2026-02-02 at 09 46 02" src="https://github.com/user-attachments/assets/9b439bf2-a61e-4bd7-a632-3d23fa915f2b" />

