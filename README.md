# info441-data-tales-final

# PROJECT DESCRIPTION

## Who is your target audience? 

Our target audience is owners or restaurant managers who want stability and clarity within their restaurant. Having a site that easily shows tables, servers, and clients will help organize service. We just want one “management dashboard” that can be edited by staff to update information about the restaurant service. In summary our audience we are honing in on is restaurant staff.

## Why does your audience want to use your application?  

Running a restaurant can be chaotic, especially during peak hours when keeping track of which tables are occupied, which servers are assigned where, and which clients are waiting can become confusing. Our application simplifies this process by offering a centralized dashboard that provides an instant overview of the dining floor. This helps managers make quick decisions, reduce confusion among servers, and improve the overall dining experience for customers. Ultimately, our product will improve efficiency and build customer satisfaction. 

## Why do you as developers want to build this application?

We want to build a real-world application that utilizes the skills we’ve learned - namely Node.js, MongoDB, Express, and front-end development to build a full-stack application. We will gain experience designing, implementing, and managing a system with multiple interacting data models (tables, servers, clients). Additionally, real-time updates, usability, and data management are skills that are relevant to real-world software engineering challenges. 

| Priority | User | Description | Technical Implementation |
|-----------|------|--------------|---------------------------|
| P0 | As a restaurant manager | I want to be able to create an account and log in/out. | Use **Azure Authentication** to authenticate users. On first login, store user information (Azure userId, name, email) in MongoDB. |
| P0 | As a restaurant manager/server | I want to be able to view all tables and their current status. | Implement `GET /tables` to retrieve all tables and their status (occupied, available, assigned server) from MongoDB. |
| P0 | As a restaurant manager/server | I want to be able to add new tables to the restaurant floor plan. | Implement `POST /tables` to create new tables with attributes (tableNumber, seats, location, assignedServerId) in MongoDB. |
| P0 | As a restaurant manager/server | I want to be able to assign client groups to tables. | Implement `PUT /clients/{id}` to update a client’s `assignedTableId` and mark that table as occupied in MongoDB. |
| P0 | As a restaurant manager/server | I want to be able to assign servers to specific tables. | Implement `PUT /tables/{id}` to update `assignedServerId` for a given table. Update the server’s `assignedTables` list accordingly. |
| P1 | As a restaurant manager/server | I want to be able to view details for a specific table. | Implement `GET /tables/{id}` to return information about one table, including assigned server and occupancy status. |
| P1 | As a restaurant manager/server | I want to be able to view all servers and their assigned tables. | Implement `GET /servers` to return all servers and their attributes from MongoDB. |
| P1 | As a restaurant manager | I want to be able to add or remove servers. | Implement `POST /servers` to add new servers and `DELETE /servers/{id}` to remove servers from MongoDB. |
| P1 | As a restaurant manager/server | I want to be able to add new client groups when customers arrive. | Implement `POST /clients` to create a new client record with details (partySize, notes, allergies). |
| P1 | As a restaurant manager/server | I want to be able to delete tables or clients when they leave. | Implement `DELETE /tables/{id}` and `DELETE /clients/{id}` to remove entries from MongoDB. |
| P2 | As a restaurant manager | I want to be able to reassign tables between servers during a shift. | Implement `PUT /tables/{id}` to update assigned server and modify both server and table data in MongoDB. |
| P2 | As a restaurant manager | I want to be able to view which server is assigned to a specific table quickly. | Implement `GET /tables/{tableId}/server` to fetch the server assigned to that table. |
| P2 | As a restaurant manager/server | I want to be able to update client details such as allergies or table changes. | Implement `PUT /clients/{id}` to modify client information in MongoDB. |
| P3 | As a restaurant manager | I want to be able to view all current clients and their assigned tables. | Implement `GET /clients` to return all current clients with their table assignments. |


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
userId: (Number)
name: (String) // name of restaurant
email: (String) // email from Azure account
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