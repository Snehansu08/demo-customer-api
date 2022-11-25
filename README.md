## Description
> The Customer API will facilitate the External reseller e-commerce systems to share details of end-customers with Fuank’s CRM (Salesforce).

The Customer API mainly has three funtionalities.
		1. Create a new customer in CRM.
		2. Update customer details.
		3. Fetch existing customer informations.

## RAML
> Below steps are implemented while building the RAML.
	1. Three resource and correspoding methods were identified for executing the functionalaties.
	2. Data Types were defined for all relevant requests and responses.
	3. Common error handler was defined with common error codes examples.
	4. Basic authentication was implemented for each methods.
	5. Traits types and libraries were created to promote reusability.



## Studio Implementation
> Following steps were performed while implementing the API in Anypoint Studio
	
	1. Flows were generated with the RAML file.
	2. APIKIT router configuration was created.
	3. Listner configuration was created.
	4. TLS was configured by adding keystore file. This will facilitate calls over HTTPS.
	5. Salesforce and Cosmos DB configuration were created.
	6. Error handling was designed in such a way so that any failure in one of the external system will roll back the changes done in other system, keeping    them in sync. In case the rollback operation is unsuccessful the flow will notify the operations team over email to do a manual rollback.
	7. A custom error handlig flow was created to handle any technical errors.
	8. Configuration, secure-configuration and global configuration property files were created.
	9. Loggers were implemented at relevant breakpoints to track transactions and errors end to end.
	10. All static values used for configurations were updated in the .yaml files.
	11. Tokens and credentials were encrypted and updated in secure property files.
	12. The API was deployed locally and sanity tests were performed.


## Testing
> Following Test Cases were created in Munits.

	1. Validate if an customer object is created in both Salesforce and Cosmos DB.
	2. Validate if an exception is thrown in case an object is created in Salesforce and not in Cosmos DB. 
	   Corresponingly the object created in Salesforce is deleted.
	3. Validate if an exception is thrown when an object is created in Salesforce but not in Cosmos DB. In such case try to delete the object from Salesforce and if the rollback operation is unsuccessful notify operations team with email.
	4. Validate if an customer object is updated in both Salesforce and Cosmos DB.
	5. Validate if an exception is thrown in case an object is updated in Salesforce and not in Cosmos DB. Corresponingly the update in Salesforce is rolled back.
	6. Validate if an exception is thrown when an object is updated in Salesforce but not in Cosmos DB. In such case try to roll back the changes from Salesforce and if the rollback operation is unsuccessful notify operations team with email.
	7. Validate if customer information is available when query with customer id.
	8. Validate if an exception is thrown when the request to query Cosmos DB is failed.

## Anypoint Monitering

	1. To enable Anypoint Monitering in Cloudhub the following property needs to be added in the Runtime Manager.
	anypoint.platform.config.analytics.agent.enabled=true
