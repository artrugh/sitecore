### REST api

- Characteristics of the REST APIs:
    - Support synchronous calls.
    - Report processing errors.
    - Support server-side requests.
    - Session authentication.
    - Read/write data.
    - Online Data Capture (ODC).

Sitecore CDP supports **Basic Authentication** for the Sitecore CDP REST API. You must send each request to the Sitecore CDP REST API over HTTPS.

**HTTP is not supported**.

- YOUR_API_KEY_ID: Client KEY
- YOUR_API_KEY_SECRET: API Token

```shell
    curl -u ${apiKey.id}:${apiKey.secret} \ -H "Accept: application/json" \ -L https://{apiEndpoint}/v2/someCollection
```

- Collection resource
    - Resource that contains other resources.
    - Submit an HTTP GET request to the Collection Resource Uniform Resource Identifier (URI).
    - They support additional behavior specific to collections, such as pagination, filtering, and sorting.
    - Attributes:
        - **href**: The fully qualified location URI of the collection resource.
        - **limit**: The maximum number of collection items to return for a single request. Minimum value is 1. The maximum value is 100. The default value is 10. This is a pagination-specific attribute.
        - **items**: array

#### Guest REST API

##### Guest Object

The **Guest Object** is the core entity of CDP. The personal data of a customer or prospect is recorded and stored, and all **relevant transactional and behavioral data** is linked in a guest profile.

Fields:
- firstSeen
- lastSeen
- guestType
- title
- firstName
- lastName
- gender
- dateOfBirth
- emails
- phoneNumbers
- language
- nationality
- passworNumber
- passportExpiry
- street
- city
- country
- postcode
- state
- subscriptions
    - name
    - channel
    - pointOfSale
    - status
    - effectiveDate
- indentifiers
    - provider
    - id
    - expiryDate

##### Guest Response Object

Response Object fields:
- href: The resource fully qualified location Uniform Resource Identifier (URI).
- ref: The reference of the resource.
- createdAt: Date and time when the resource was created in Sitecore CDP.
- modifiedAt: Date and time when the resource was updated in Sitecore CDP.

##### Locate guests functions

###### GET Guest

**Locate guests function** to return guests using the following search parameters:
- FIRST_NAME
- LAST_NAME
- PHONE_NUMBER
- EMAIL
- EMAIL.UNTOUCHED
- IDENTIFIERS.PROVIDER
- IDENTIFIERS.ID

```shell
    $ curl -H "Accept: application/json" \  "https://{apiEndpoint}/v2/guests?email=jack.smith@boxever.com"

    $ curl -H "Accept: application/json" \ "https://api.boxever.com/v2/guests/?identifiers.provider=MY_ACCOUNT_ID&identifiers.id=jack123"
```
JSON Response

```json
{
    "href": "https://{apiEndpoint}/v2/guests?email=jack.smith@gmail.com",
    "offset": 0,
    "limit": 10,
    "items": [{
        "href": "https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46"
    }]
}
```

After you perform the **locate guests function**, you can use the **guestRef** included in the response href to retrieve the full guest record.

The Guest Function with **guestRef** retrieves Guest Data + Personally Identifiable Information (PII).

```shell
$ curl -H "Accept: application/json" \ "https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46"
```

You can expand the collection resource when using the locate guests function.

However, the following pagination parameters are **not supported** using the locate guests function:
- offset
- limit
- support

###### POST Guest

Create or Update a guest Record using PII

create: POST: https://apiEndpoint/v2/guests
update: POST: https://apiEndpoint/v2/guests/guestRef

Create example.

```shell
    $curl  --request POST 'https://{apiEndpoint}/v2/guests' \
    --header 'Content-Type: application/json' 
    --data-raw '
    {
        "guestType": "customer",
        "title": "Mr",
        "firstName": "Jack",
        "lastName": "Smith",
        "gender": "male",
        "dateOfBirth": "1976-10-28T00:00:00.000Z",
        "emails": [
            "jack.smith@boxever.com"
        ],
        "phoneNumbers": [
            "0851234567"
        ],
        "nationality": "Irish",
        "passportNumber": "PZ4A9565",
        "passportExpiry": "2019-01-01T00:00Z",
        "street": [
            "Apartment 15",
            "West Drive Avenue"
        ],
        "city": "Dublin",
        "country": "IE",
        "postCode": "D2",
        "state": "Dublin",
        "subscriptions": [
            {
                "name": "default",
                "channel": "EMAIL",
                "pointOfSale": "default",
                "status": "SUBSCRIBED",
                "effectiveDate": "2012-08-23T16:17:16.000Z"
            }
        ]
    }'
```

##### Guest Extentions data model - Additional guest Data

- extentions:
    - A guest data extension is an **array** of custom name-value pairs (attributes).
    - The guest data extension collection is linked to a **guest object** that enables you to extend your own requirements and custom attributes into the guest object. You can insert one data extension within the array.
        - name*: set to *ext*
        - key*: set to *default*.
        - attribute: name/value pair attributes.

###### GET

```shell
$ curl -H "Accept: application/json" \
    "https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46/extExt
```

Response
```JSON
{
    "href": "https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46/extExt",
    "offset": 0,
    "limit": 10,
    "items": [{
        "href": "https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46/extPreferences/0349654D-5DB7-4103-8C9E-88953648EE1"
    }]
}
```

```shell
$ curl -H "Accept: application/json" \
    "https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46/extExt/0349654D-5DB7-4103-8C9E-88953648EE1
```

Response
```json
{
    "href": "https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46/extExt/0349654D-5DB7-4103-8C9E-88953648EE18",
    "ref": "0349654D-5DB7-4103-8C9E-88953648EE18",
    "createdAt": "2010-03-07T16:15:11.000Z",
    "modifiedAt": "2012-08-23T16:17:16.000Z",
    "key": "default",
    "format": "HTML",
    "acceptedTermsAndConditions": true,
    "shortDescription": "The email preferences for this guest",
    "longDescription": "The email preferences for this guest"
}
```

###### POST

Create guest data Extention
POST: https://apiEndpoint/v2/guests/guestRef/extdataExtensionName

```shell
$curl  --request POST 'https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46/extExt' \
 --header 'Content-Type: application/json'  \
 --data-raw '{
    "key": "default",
    "format": "HTML",
    "acceptedTermsAndConditions": true,
    "shortDescription": "The email preferences for this guest",
    "longDescription": "The email preferences for this guest"
}'
```
Update guest data Extention 
POST: https://apiEndpoint/v2/guests/guestRef/extdataExtensionName/dataExtensionRef

```shell
$curl  --request POST 'https://{apiEndpoint}/v2/guests/9d94ee11-7043-4b71-980c-a777d00a7b46/extExt/0349654D-5DB7-4103-8C9E-88953648EE18' \
 --header 'Content-Type: application/json' \
 --data-raw '{
    "key": "default",
    "format": "HTML",
    "acceptedTermsAndConditions": true,
    "shortDescription": "The email preferences for this guest",
    "longDescription": "The email preferences for this guest"
}' 
```

###### DELETE

- delete guest data Extention
DELETE: https://apiEndpoint/v2/guests/guestRef/extdataExtensionName/dataExtensionRef
