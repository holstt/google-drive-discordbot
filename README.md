# Google Drive Service
![dotnet](https://img.shields.io/badge/asp--net--core-v3.1-blue)
![dotnet](https://img.shields.io/badge/google--api--drive-v3-blue)
![dotnet](https://img.shields.io/badge/google--api--sheets-v4-blue)

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

Using Google's APIs requires a Google Cloud Platform (GCP) account. You might want to familiarize yourself with the resepective API quotas before getting started.

Obtain Google credentials (json-file) for the Google Drive API and Google Sheets API and place the file in /Secrets

Either run the project natively or use the provided Dockerfile.

#### Native
1. `git clone https://github.com/roedebaron/google-drive-service.git`
2. `cd google-drive-service/GoogleDriveService.Api`
3. Run `dotnet run` to download dependencies, build and run the service. 
4. If no other port has been specified in the configuration, the service is now running on port 5000. 

#### Docker
1. `git clone https://github.com/roedebaron/google-drive-service.git`
2. `cd google-drive-service`
3. Run `docker build -t drive-service .` to build the image with name `drive-service`
4. Run `docker run -dp 5000:5000 drive-service ` to start a container from the image. This will map your local port (e.g. 5000) to the port that the service is listening on (default is 5000). 

> TODO: 
> - Using own Google API credentials + how to get these.

## Usage 

### Drive - Queries





### Sheets - Attendance registration

Registrering attendance requires that: 
- THe Google Sheets API is enabled for your GCP service account.
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
