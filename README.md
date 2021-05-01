# Google Drive Discord Bot <img src="https://logos-world.net/wp-content/uploads/2020/11/Google-Drive-Logo.png" alt="Alt text" width="50">


![dotnet](https://img.shields.io/badge/asp--net--core-v3.1-blue)
![dotnet](https://img.shields.io/badge/google--api--drive-v3-green)
![dotnet](https://img.shields.io/badge/google--api--sheets-v4-green)
![csharp](https://img.shields.io/badge/C%23-8-purple)
![ide](https://img.shields.io/badge/IDE-vs2019-purple)

Discord bot providing convenient methods to search, list and create documents in Google Drive. Has built-in attendance registration using Google Sheets as well.

## About

The Discord bot is developed using a microservice architecture, but the google-drive-service can also be used independently. 

#### Microservice: google-drive-service

The internal architecture is based on the MVC-pattern following the principles from Domain-Driven Design (DDD). 

A brief overview of the layers:

**Core**: Business logic. Represents domain objects and services. 

**View**: I/A

**Controller**: Recieves incoming requests which are then delegated to **Core**. The result from Core is returned to the client.

**Infrastructure**: Handles communication with external web services (Google API). No data persistence. 

#### Microservice: discordbot

....


## Getting Started

Using Google's APIs requires a Google Cloud Platform (GCP) account. You might want to familiarize yourself with the resepective API quotas before getting started.


### Configuration

Obtain Google credentials (json-file) for the Google Drive API and Google Sheets API and place the file in the folder `google-drive-service/GoogleDriveService.Infrastructure/Secrets`.

### Running the bot

Either run the services from source or use the provided `docker-compose.yml` file to run it via Docker Compose (recomended).  

Clone the project: 
1. `git clone https://github.com/roedebaron/google-drive-service.git`

#### Running from source
2. Run `dotnet run --project GoogleDriveService.Api`. This will automatically download all dependencies, build the project and then run the service. 
3. If no other port has been specified in the configuration, the service is now running on port 5000. 


#### Running with Docker Compose 🐳
2. Examine the configuration in the `docker-compose.yml` file. Change the host port in the port mapping to your preference or leave as is. 
3. Run `docker-compose up` in the root folder to build and run the service.

> TODO: 
> - Using your own Google API credentials + how to get these.

## Usage

Go to `localhost:[PORT]/swagger/v1/swagger.json` to get an overview and try out all the endpoints.

> TODO: 
> - Document swagger endpoint

### Drive - Queries


### Sheets - Attendance registration

Registrering attendance requires that: 
- The Google Sheets API is enabled for your GCP service account.
- An url to a spreadsheet where the GCP account has _editor_ access. As such, you have to ensure that the spreadsheet is shared with the email of the account.   
- The sheet complies with certain rules in order for the GoogleDriveService to insert/register the attendance correctly in the sheet. It is possible to have a compliant sheet created for you from a template, by simply providing an id on a completely empty sheet at the first attendance request. Then the service will create an attendance sheet and register the attendance. attendance ready-made 

To register attendance call the endpoint `sheet/attendance-updates` with a json object containing the spreadsheet id and attendees with their presence status and an optional message. If the spreadsheet contains multiple tabs (sheets), and the attendance is **not** on the first tab, then the sheetId should always be specified.

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
    "sheetId": 123456789 // Optional. Defaults to the first sheet/tab of the specified spreadsheet.
  }
}
```

> TODO:
> - Insert screenshot, demo gif, code examples... 
>

## Project TODO
- [ ] Push code to repo
- [ ] Migrate to .NET 5/C#9
- [ ] Discord bot integration

## Disclaimer



