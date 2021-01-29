# http-post-sender
This is a C# .Net console application to send data from a delimited text file to an http REST endpoint via POST requests. Publish this console app to your Azure portal to create a continuously running source of messages to your REST endpoint to support demos of Velocity and GeoEvent Server.


## Features
* Use http-post-sender to send records from your delimited data file as event messages to an http REST endpoint via POST requests. 
* Provides a source of messages for your Velocity and GeoEvent Server demos.

## Instructions

1. Clone the repo in Visual Studio Code.
2. Update the app.config file as follows:    


    -	receiverUrl – Paste the complete URL to which data should be sent.    
    -	authenticationArcGIS – True if your Velocity feed requires ArcGIS authentication, false if not.
    -	tokenPortalUrl – Used only if authenticationArcGIS is true. The root url to the ArcGIS portal to be used for obtaining a token.
    -	username – Used only if authenticationArcGIS is true. The username for generating a token.
    -	password – Used only if authenticationArcGIS is true. The password for generating a token.
    -	fileUrl – Enter the URL to the simulation delimited file containing the data to be sent between the empty quotes for the value of fileUrl. If using our sample file, set this value to “https://a4iot-test-data.s3.us-west-2.amazonaws.com/point/Charlotte_Simulations/57Buses_in_CharlotteNC.csv”.
    -	hasHeaders – Enter true or false to indicate whether the simulation csv file has a header row of field names. If using our sample csv file, set this value to “true”.
    -	fieldDelimiter – the delimiter between fields in the simulation file. If using our sample csv file, set this value to “,”.
    -	numLinesPerBatch – Enter the number of lines to send with each batch. The app will read this number of lines from the simulation csv file, bundle them into a batch of events and send them to the REST endpoint all at once. Then it will read the next set of lines into a batch, send them and repeat until the end of the simulation file is reached and all lines have been sent. You might set this value to be equal to the number of unique track ids in your data or use it in conjunction with the sendInterval to simply control the rate of events into your REST endpoint. If using our sample csv file, there are 57 unique track ids.
    -	sendInterval – Enter the number of milliseconds between batches sent to the REST endpoint. This time includes the time required to send a batch. Thus, if this value is set to 1000ms, and it takes 700ms to send a batch, the app will wait 300ms before sending the next batch. If it takes longer than this value to send a batch, it will not wait before sending the next batch.
    -	timeField – The zero-based index of the field in the simulation csv file containing date values. If using our sample csv file, set this value to “0”.
    -	setToCurrentTime – Enter true or false to indicate whether to update the values in the date field to the date and time the event is sent to the REST endpoint. If using our sample csv file, set this value to “true”. 
    -	dateFormat – Optional, only used if setToCurrentTime is true. In that case the date values will be formatted as strings according to this formatter. If this value is empty, date values will be epochs. Formatting string can be standard or custom. See https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings and https://docs.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings
    -	dateCulture - Optional, examples: "en-US", "es-ES", "fr-FR"; only used if setToCurrentTime is true and dateFormat is not empty. In that case date strings will be formatted according to the culture specified in this setting or the default culture if empty

3. Commit the changes in the app.config file
4. Deploy to Azure App Service to your Azure portal.
5. In the resulting App Service, configure the deployment source to be LocalGit.
6. Deploy to Web App.
7. Set up a feed in ArcGIS Velocity or an input in ArcGIS GeoEvent Server to receive the messages sent by this app.

Detailed instructions are in the "Deploy HttpPostSender to Azure App Service using Visual Studio Code.pdf" file in this repo.

## Requirements

* Microsoft Azure account with and active subscription. (Create one for free: https://azure.microsoft.com/free/?utm_source=campaign&utm_campaign=vscode-tutorial-appservice-extension&mktingSource=vscode-tutorial-appservice-extension)
* Visual Studio Code (VS Code) installed on your local machine. (Get it here: https://code.visualstudio.com/)
* The Azure App Service extension for VS Code (install from within VS Code or get it here: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice)
* Git installed on your local machine. (Get it here: https://git-scm.com/)
* A delimited text file of events you wish to simulate. It must be hosted in a place where it is accessible by URL such as an Amazon S3 bucket. To get started you may use the sample file hosted in this repo (https://a4iot-test-data.s3.us-west-2.amazonaws.com/point/Charlotte_Simulations/57Buses_in_CharlotteNC.csv).


## Resources


## Issues

Find a bug or want to request a new feature?  Please let us know by submitting an issue.

## Contributing

Esri welcomes contributions from anyone and everyone. Please see our [guidelines for contributing](https://github.com/esri/contributing).

## Licensing
Copyright 2021 Esri

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

A copy of the license is available in the repository's [license.txt]( https://github.com/kengorton/event-hub-sender/blob/master/license.txt) file.

ArcGIS Velocity, ArcGIS GeoEvent Server, Microsoft Azure, C#, .Net
