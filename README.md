# ai
REST API to manage resource: Person

Base URI: https://ai.com/resources

GET /data/{data_id}
DELETE /data/{id}
PUT /data

Authentication method:
API Key / Token which can be sent in header

Content-type: application/json
HTTPS (SSL) implementation

GET	/data/{data_id}	
--------------------
Index {data_id}	is the key and the function getPerson to be Used for retrieving requested person data.
     200 Ok        --> Person found in the system and response will be sent
     404 Not Found --> Provided Index not found in the system. (Could be such never never exists or could be deleted)


PUT	/data
--------
UpSertPerson function (Replace if exists else Insert) to be Used for replacing the entire person data. 
    201 Created --> New record created
    200 Ok --> Based on the requirements, As there is no way to identify if a Person exists because the Identifier is not part of user input. If we can make Name as unique then we can apply logic to Replace the record)

DELETE /data/{data_id}
----------------------
deletePerson function can be used for deleting the resource / Record.	
   204 No content --> Person deleted Successfully
   404 Not Found  --> Provided Index identifier not found (Either already deleted or never created)


Technology stack:
-----------------
Language --> Java
Framework --> Springboot
Persistent storage --> Mysql / Postgres  or equvalant. 
Application server --> Tomcat / weblogic / jboss / etc
Can be container based deployment using AWS fargate 

Input parameters from User/requestor
------------------------------------
Id     String  (Auto generated) --> Auto generated number (Based on spec the request is to be String however, usually a non modifiable filed is recomended to be a number)
Name   String  (User Input)     --> Name of the person. (Recomended to be unique to maintain integrity of data. This can help in identifying existing name and replace during PUT operation)
Age    Integer (USer Input)     --> Store the age of the person
Locale String  (Auto capture)   --> If the intention is to store the client Locale, Then better take it from the HTTP Header to have accuracy in data capture.


Table structure
===============
FIELD       DATATYPE and CCONSTRAINT
==========  =======================
ID          STRING  NOT NULL 
NAME        STRING  NOT NULL UNIQUE
AGE         INTEGER 
LOCALE      STRING  
CREATED_DT  DATE
MODIFIED_DT DATE

URI: PUT/resources/data
=======================
    Request payload:
    {
        "Name":"Scott",
        "age":29
    }

    Response payload:
    {
        "data_id":"<System generated value>"
    }

URI: GET/resources/data/{data_id}
=================================
    Request payload: N/a
    Response payload:
    {
        "data_id":"<Retrieved System generated value>",
        "Name":"Scott",
        "Age":"29,
        "Locale":"en_US"
    }

URI: DELETE/resources/data/{data_id}
====================================
    Request payload: N/a
    Response payload: N/a
       
    
