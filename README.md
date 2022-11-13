# Patient_Treatment_Management_Neo4J_and_Mongodb
This scenario involves diagnosing the patient with possible side effects from wrong drug ingestion. I have used MongoDB to store patient’s data and Neo4J for side 	effects, medicines and to define the relationship between them.

Database:	                    Neo4j Desktop,
                              Neo4j Driver,
                              MongoDB Atlas,
                              MongoDB Compass

Programming Languages:	        JavaScript, Nodejs

IDE:	                          Visual Studio Code

Version Control:	              Git
                              GitHub

The system will take the patient's side effects that he's facing and then suggest the medicine that he might have taken. The system also adds new side effects, medicines and defines relationships between them. Relationship is defined as which medicine has which side effects. The user inputs the symptoms of the patient along with the patient’s name. The system updates the test history of the patient in the main patient database.


This system can add side effects and medicines into Neo4J from the front-end by using NodeJS. 
It can also define the relationship between existing side effects and medicines.
Once the patient gives his side effects, the system can generate the possible medicines which he might have taken. 
Output on Localhost

![image](https://user-images.githubusercontent.com/97853861/201519730-f821cccd-6bff-4ea3-8ee6-9446d95783fa.png)

 
Here, I have taken four side effects and after clicking on”Identify Medicine” button, it generates the output. 

![image](https://user-images.githubusercontent.com/97853861/201519735-91ff70dd-b39a-40ba-afe1-f1960c05984c.png)
![image](https://user-images.githubusercontent.com/97853861/201519738-115bc487-c7d8-4415-a7eb-7c2a1740b470.png)

Output in Neo4J
I have imported the medicine and side effects dataset in Neo4J by using below query:
LOAD CSV WITH HEADERS from 'file:///medicines.csv' as row with row where row.Side_Effect is not null MERGE(se:Side_Efect {Name: row.Side_Effect}) MERGE(m:Medicine {Name: row.Medicine}) MERGE(se) -[:ofmedicine]->(m)

![image](https://user-images.githubusercontent.com/97853861/201519754-a9ba971c-5f5c-4854-8231-bae7ef4692b6.png)
![image](https://user-images.githubusercontent.com/97853861/201519763-133644bf-d429-44c0-a7b3-78382ddd1b9e.png)

 
 
Relationship between side effects and medicine
MATCH(se:Side_Effect{Name:$NameParam}), (m:Medicine{Name:$NameParam2}) 		MERGE (se)-[o:ofmedicine]-(m) RETURN se.Name,m.Name,o

Query to generate output.
MATCH (se:Side_Effect{Name:"Coombs test"})-[:ofmedicine]-(m:Medicine)-	[	:ofmedicine]-(se1:Side_Effect{Name:"Cramp abdominal"}) RETURN m
 
![image](https://user-images.githubusercontent.com/97853861/201519782-3593dced-98c0-4beb-9b5d-dedf3c5170f7.png)



Output from MongoDB
System is using MongoDB to update the patient’s history. 
Before updating patient’s history

![image](https://user-images.githubusercontent.com/97853861/201519808-d942ef57-e72d-44f5-bfc0-87f82274251d.png)

 
After updating patient’s history

![image](https://user-images.githubusercontent.com/97853861/201519820-d54d9d01-3251-4b67-b167-4c85b49b88f0.png)

 
Output in terminal

![image](https://user-images.githubusercontent.com/97853861/201519827-a232952f-a257-438a-89ba-d6d881ac5bd2.png)

 
