### Batch API

- It supports uploading **large volume of guests, order, tracking offline data** that is imported using CDP's standard JSON schema.
- Benefits:
    - Greater flexibility in guest segmentation.
    - A more comprehensive single customer view.
    - Higher sophistication of decision logic.   
- Typically used for **initial upload of all historical data** to store against the customer profile.
- It supports **asynchronous requests**, meaning that multiple batch imports can be initiated in parallel, if required. After a **batch file** is submitted for processing, users can check the progress-status of the batch import. 

#### Implementation

Sitecore CDP supports Basic Authentication for the Sitecore CDP Batch API. You must send each request to the Sitecore CDP Batch API over HTTPS. **HTTP is not supported**.

When using Basic Authentication, apply a base 64 encoding to a string made up of your API_KEY_ID and API_KEY_SECRET, separated by a colon (:). Example of a PUT request authorization:

- YOUR_API_KEY_ID: Client KEY
- YOUR_API_KEY_SECRET: API Token

```shell
    Authorization: Basic aHR0cHdhdGNoOmY=
    Content-Type: application/json
    Accept: application/json
    PUT https://api.boxever.com/v2/batches/3ee694e5-0b77-2d1e-af19-1aa78f500785

    {
    “checksum”: “40d9a12f0a3c93c8ed66a3b6f3735790”,
    “size”: 3456
    }
```

#### File Formatting Requirements

Before a file is imported, it is important to match that it feels formatting requirements.

1. Compress the file. GZIP Compression. There is a **50MB size limit** for uploading batch files.

2. Generate a **hex-encoded MD5 checksum** for the compressed file. You must provide this during the upload process to provide assurance that the integrity of the import file sent is intact.

3. If you are importing the file using a PUT request, generate a **unique identifier** for the batch. This is used when interacting with the Batch API endpoint and must be unique across all batches.

4. Use a **JSON HTTP PUT** request to the Sitecore CDP Batch API to allocate a location to which you subsequently upload the batch file.

5. Each file must contain a separate JSON record for each entity to import. Each JSON record must contain a single line, be terminated with a carriage return, and encoded according to RFC 4627.

Required fields of the JSON:
- ref: UUID.
- schema: type of record, guest, order, tracking or migration.
- mode: how to import the record into the system:
    - insert: overwrites everthing.
    - upsert: updates the existing entity only with the fields set in the request.
    - guest: applies specific migration rules to how the fields are updated. Only use "guest" as the value for "mode", when migrating guests.
- value: JSON object

```shell
    {"ref":"CE8B4A20-9C56-49A9-8B94-D1474939612F","schema":"guest","mode":"upsert","value":{ <valid guest record> }} 
    {"ref":"A721CE88-7E0D-45FC-9380-93EA1A5CA559","schema":"guest","mode":"upsert","value":{ <valid guest record> }}
```

6. After you send a request to upload a batch file, you can verify the status of the batch upload by sending a GET request to the unique batch URL.


#### JSON Data Model

Fields:

- identifiers: A list of identifiers for the guest.
    - provider.
    - id.
    - expirtyDate.
    
- extentions: A list of extensions associated with the guest.
    Guest data extensions are optional and enable your organization to capture more robust information about your guests.

    A guest data extension is an **array** that enables you to specify whatever **name/value pairs (attributes)** you want. 

    The guest data extension collection is linked to a **guest object** that enables you to extend your own requirements and custom attributes into the guest object. You can insert one data extension within the array.
    - name*: set to *ext*
    - key*: set to *default*.
    - attribute: name/value pair attributes.

- subscriptions:
    - name: subscription's name.
    - pointOfSale: The store front the subscription is associated with.
    - channel: delivery of communications (EMAIL).
    - status: PENDING, SUBSCRIBED, UNSUBSCRIBED, UNKNOWN.
    - effectiveDate: The date and time the subscription list is valid from subscribed.

#### Tracking event Data Model

```json
{  
   "ref":"37906b7c-6867-4e81-ada7-78ecfe329eb8",
   "schema":"tracking",
   "mode":"insert",
   "value":
   {  
        // The name of the external Service which is providing the reporting data.
        "serviceIdentifier":"TEST_PROVIDER",
        "occurredAt":"2015-03-07T14:15:00.000Z",
        "channel":"EMAIL",
        // Type of tracking event which occurred.
        "type":"SENT",
        "uotr":"c56a4180-65aa-42ec-a945-5fd21dec0538|0",
        "utms":{  
            "utm_medium":"EMAIL",
            "utm_source":"BOXEVER",
            "utm_term":"abc"
        },
        "feedback": { 
            "reasonCode": "PRICE_TOO_HIGH",
            "notes": "The customer said the price was out of their budget"
        }
   }
}
```