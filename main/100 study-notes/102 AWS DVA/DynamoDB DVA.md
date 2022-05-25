---
created: 2022-05-25 10:53
updated: 2022-05-25 12:27
---
---
**Links**: [[102 AWS DVA Index]]

---
## Partition keys
- Option I: Partition Key (*HASH*)
	- Partition key must be **unique** for each item
	- Partition key must be **diverse** so that the data is distributed
	- Example: *User_ID for a users table*
		- ![[attachments/Pasted image 20220525105323.png]]

- Option 2: Partition Key + Sort Key (HASH + RANGE)
	- The **combination must be unique** for each item
	- Data is *grouped by partition key*
	- Example: *users-games table*, User_ID for Partition Key and Game_ID for Sort Key
		- ![[attachments/Pasted image 20220525105504.png]]

> [!question]- What is the best Partition Key to **maximise data distribution**? movie_id ,producer_name, leader_actor_name, movie_language?
> - *movie_id* has the **highest cardinality** so it's a good candidate 
> movie_language doesn't take many values and may be skewed towards English so it's not a great choice for the Partition Key

