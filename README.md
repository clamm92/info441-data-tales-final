# info441-data-tales-final

# PROJECT DESCRIPTION

## Who is your target audience?  
Who do you envision using your application? Depending on the domain of your application, there may be a variety of audiences interested in using your application. You should hone in on one of these audiences.

Our target audience is owners or restaurant managers who want stability and clarity within their restaurant. Having a site that easily shows tables, servers, and clients will help organize service. We just want one “management dashboard” that can be edited by staff to update information about the restaurant service. In summary our audience we are honing in on is restaurant staff.

## Why does your audience want to use your application?  
Please provide some sort of reasoning.  

Running a restaurant can be chaotic, especially during peak hours when keeping track of which tables are occupied, which servers are assigned where, and which clients are waiting can become confusing. Our application simplifies this process by offering a centralized dashboard that provides an instant overview of the dining floor. This helps managers make quick decisions, reduce confusion among servers, and improve the overall dining experience for customers. Ultimately, our product will improve efficiency and build customer satisfaction. 

## Why do you as developers want to build this application?

We want to build a real-world application that utilizes the skills we’ve learned - namely Node.js, MongoDB, Express, and front-end development to build a full-stack application. We will gain experience designing, implementing, and managing a system with multiple interacting data models (tables, servers, clients). Additionally, real-time updates, usability, and data management are skills that are relevant to real-world software engineering challenges. 

## Endpoints:

**POST** `/user/login` - allows owner/manager login to account  
**POST** `/user/register` - registers an owner/manager account (1 per restaurant)  
**GET** `/user` - returns name of restaurant  

**GET** `/tables` - gets all table and their status (occupied, available, assigned server)  
**GET** `/tables/{id}` - gets information about a specific table (seats, occupied, server)  
**POST** `/tables` - adds a new table with attributes  
**PUT** `/tables/{id}` - updates a table (reassign server, etc)  
**DELETE** `/tables/{id}` - deletes a table  

**GET** `/servers` - return all servers and attributes (assigned tables, etc.)  
**GET** `/servers/{id}` - returns details for a specific server  
**POST** `/servers` - creates a new server with attributes  
**PUT** `/servers/{id}` - updates a server with attributes (inactive, etc)  
**DELETE** `/servers/{id}` - deletes a server  

**GET** `/clients` - returns all clients (groups) in restaurant  
**GET** `/clients/{id}` - returns details about a specific client (group)  
**POST** `/clients` - creates a new client with details (allergies, group size)  
**PUT** `/clients/{id}` - updates client information (allergies, table change)  
**DELETE** `/clients/{id}` - deletes a group  

**GET** `/tables/{tableId}/server` - returns server for specific table  

We may come up with more as we develop.  

## Users
```
userID (Number)
name (String) (probably name of restaurant, since 1 per restaurant)
```

## Tables
```
tableId (Number)
tableNumber (Number)
seats (Number)
occupied (Boolean)
assignedServerId (Number) (references a server)
location (String)
```

## Servers
```
serverId (Number)
name (String)
assignedTables ([Number]) // references tables
active (Boolean)
```

## Clients
```
clientId (Number)
names ([String]) // not sure if this is necessary
notes (String) //allergies, etc.
assignedTableId (Number)
partySize (Number)
```