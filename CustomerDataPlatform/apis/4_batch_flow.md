### Batch Flows

Batch processing is a method of running software programs called **jobs** in batches automatically.

No other interaction by the user is required to process the batch.

Batches may **automatically be run at scheduled times** as well as being run contingent on the availability of computer resources.

Use flows for batch flows, that is:
- daily.
- weekly.
- monthly.

#### Steps

1. Configure External Service Connection.
2. Create Flow Template.
    - Library tab
3. Returning Offers.

You can use the A**udience Sync REST API** to perform the retrieve batch flows job record function to retrieve a batch job for a flow.

To do this, you must have the ref attribute included in the response when locating batch flow jobs.

To retrieve a batch flows job record in Sitecore CDP, use the following:

GET: https://apiEndpoint/v2/batchFlowsJob/<ref>

