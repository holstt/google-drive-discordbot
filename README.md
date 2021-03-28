# GoogleDriveService
RESTful webservice providing convenient methods to search, list and create documents in Google Drive. Has built-in attendance registration using Google Sheets as well. 

## About

The internal architecture is based on the MVC-pattern following the principles from Domain-Driven Design (DDD). 

The GoogleDriveService can be used independently but is also part of the [DiscordBot](https://github.com/roedebaron/DiscordBot) microservice architecture which enables the user to conveniently call the webservice using Discord commands.

A brief overview of the layers: 

**Core**: Business logic. Represents domain objects and services. 

**View**: I/A

**Controller**: Recieves incoming requests which are then delegated to **Core**. The result from Core is returned to the client.

**Infrastructure**: Handles communication with external web services (Google API). No data persistence. 

## Getting Started

Obtain Google credentials (json-file) for the Google Drive API and Google Sheets API and place the file in /Secrets

Either run the project natively or use the provided Dockerfile.

> TODO: 
> - Using own Google API credentials + how to get these.
> - Native + Docker command


## Usage 

### Google Drive requests




### Attendance registration

Registrering attendance requires that: 
- The Google account subscribes to the Google Sheets API
- An url to a Sheet where the Google account has editor access
- The Sheet complies with certain rules in order for the GoogleDriveService to insert/register the attendance correctly in the Sheet. Please see [INSERT REF]

To register attendance call the endpoint `sheet/attendance-updates` with a json object containing the sheet id and attendees with their presence status and an optional message: 

```JSONC
{
  "attendees": [
    {
      "name": "Person1",
      "presence": "Present" //  Or use integer 0
    },
        {
      "name": "Person2",
      "presence": "Late" // Or use integer 1
    },
        {
      "name": "Person3",
      "presence": "Absent", // Or use integer 2
      "attendancemessage" : "On vacation" // Optional attendance message
    }
  ],
  "id": {
    "spreadSheetId": "DwaypOAqJclqPmSlWgPAfgxMjaYhLxJDDtyabvaDTIUHqhoc65",
    "sheetId": 123456789
  }
}
```

> TODO:
> - Insert screenshot, demo gif, code examples... 
> 





