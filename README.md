# MSDYN365FO-EventBasedIntegration
Event Based Integration using Business Events and Data Management Framework

## Trigger
The main trigger is in the handler class. Notice how it is only firing when the category is Integration.
```
class NAVAXDMFExportBusinessEventHandler
{
    [DataEventHandler(tableStr(DMFEntityExportDetails), DataEventType::Inserted)]
    public static void DMFEntityExportDetails_onInserted(Common sender, DataEventArgs e)
    {
        DMFEntityExportDetails dmfEntityExportDetails = sender;                                                                         
        DMFDefinitionGroup dmfDefinitionGroup = DMFDefinitionGroup::find(dmfEntityExportDetails.DefinitionGroup);

        if (dmfDefinitionGroup.OperationType == DMFOperationType::Export &&
            dmfDefinitionGroup.ProjectCategory == DMFProjectCategory::Integration &&
            dmfEntityExportDetails.RecId &&
            dmfEntityExportDetails.SampleFilePath)
        {
            NAVAXDMFExportBusinessEvent businessEvent = NAVAXDMFExportBusinessEvent::newFromDMFEntityExportDetailsRecId(dmfEntityExportDetails.RecId);
            businessEvent.send();
        }
    }
}
```
## Sample payload
Below is a sample payload that the Business Event produces. 
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
