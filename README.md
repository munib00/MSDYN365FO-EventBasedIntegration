# MSDYN365FO-EventBasedIntegration

Event Based Integration using Business Events and Data Management Framework

1. Export Business Event
2. Import Business Event

Create an import or export project with category type of "Integration" for these business events to fire.

## Sample payload

Below is a sample payload that the Business Event produces. 

**Export Business Event**

```json
{
    "DownloadURL": "https://d365fo07dd4ba16f.blob.core.windows.net/dmf/Customer%20g%7BD1A2E1DB24F548AB9A24F8EC65D05DC1%7D.json?sv=2014-02-14&sr=b&sig=KbEE0xpf0Rm2rgfUuhN4R6R%2Fv88fSeImq%2BAFTpqjNO4%3D&st=2019-06-18T06%3A28%3A29Z&se=2019-06-18T07%3A33%3A29Z&sp=r",
    "EntityName": "Customer groups",
    "EventId": "{6070E2A4-A3D8-4074-B105-4F2666CCA04C}",
    "EventTime": "/Date(1560839609000)/",
    "LegalEntity": "usmf",
    "MajorVersion": 0,
    "MinorVersion": 0,
    "NoOfRecords": 7,
    "OperationType": "Export",
    "ProjectCategory": "Integration",
    "RecId": 68719523988
}
```

**Note:** that the download URL is only valid for 1 hour. This is by default because I am using a standard method to generate the blob url

```
DMFDataPopulation::getAzureBlobReadUrl(str2Guid(_dmfEntityExportDetails.SampleFilePath))
```

**Import Business Event**

```json
{
    "BusinessEventId": "NAVAXDMFImportStatusBusinessEvent",
    "ControlNumber": 5637145327,
    "EndDateTime": "2020-05-29T07:55:30Z",
    "EntityName": "Customer groups",
    "EventId": "E6471158-09E3-4BDA-A508-924A8FE7A43B",
    "EventTime": "/Date(1590738930000)/",
    "ExecutionId": "ProductImport-2020-05-29T07:55:23-661B8ED5EA024A6F8F1B8C6E08282D6E",
    "FileName": "O6J09AR6F",
    "LegalEntity": "usmf",
    "MajorVersion": 0,
    "MinorVersion": 0,
    "NoOfCreatedRecords": 1,
    "NoOfRecords": 2,
    "NoOfUpdatedRecords": 0,
    "OperationType": "Import",
    "ProjectCategory": "Project",
    "RecId": 5637188829,
    "StartedDateTime": "2020-05-29T07:55:27Z",
    "Status": "Partially succeeded"
}
```
