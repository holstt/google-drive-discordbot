# GoogleDriveService
RESTful webservice providing convenient methods to search, list and create documents in Google Drive. 

## About

The internal architecture is based on the MVC-pattern following the principles from Domain-Driven Design (DDD). 

The GoogleDriveService can be used independently but is also part of the [DiscordBot](https://github.com/roedebaron/DiscordBot) microservice architecture which enables the user to implicitly call the webservice using Discord commands.

A brief overview of the layers: 

**Core**: Business logic. Represents domain objects and services. 

**View**: I/A

**Controller**: Recieves incoming requests which are then delegated to **Core**. The result from Core is returned to the client.

**Infrastructure**: Handles communication with external web services (Google API). No data persistence. 
