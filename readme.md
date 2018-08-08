# Quick Start Guide - Salesforce Emulator
This project emulates request and response flows of some of the Salesforce partner SOAP API v.41. Used for Developer onboarding so they don't need to sign up for a trial account and lose their path. This is used in the [Connecting your first SaaS applications](https://developer.mulesoft.com/guides/quick-start/connecting-your-first-saas-applications) quick start guide.

**NOTE:** Currently all responses are emulated with predefined payloads. Future iterations can potentially use a real Salesforce instance and use this service to as a proxy while adding/hiding true authentication, but currently that's not possible. At the time of writing this service, SOAPKit overrides the response and the consumer Salesforce connector does not handle the modified responses. You also cannot use the Salesforce WSDL to generate the SOAP service since the payload deviates from pure SOAP standard and SOAPkit will attach namespaces to all tags.

## Requirements
 - Anypoint Studio 6.4
 - Mule runtime 3.9.1

## Usage
Use the MuleSoft Salesforce connector with the details below to POST SOAP requests for operations listed below. 

## Deployed service
[http://salesforce-emulator.cloudhub.io/](http://salesforce-emulator.cloudhub.io/)

## User credentials
Username: `mulesoft`\
Password: `mulesoft`\
Security Token: ` `

## Troubleshooting
To see detailed logs of all transactions, modify your log4j output to include the following:

**NOTE:** For the CloudHub deployed app, it's best to add to Runtime Manager settings instead of having this in the deployed package. The SFDC logger is not needed if the Salesforce connector isn't used.

```
<!-- SFDC --> 
<AsyncLogger name="org.mule.modules.salesforce" level="TRACE"/> 
<AsyncLogger name="com.sforce" level="TRACE"/> 
<!--HTTP--> 
<Logger level="DEBUG" name="httpclient.wire.header"/> 
<Logger level="DEBUG" name="httpclient.wire.content"/> 
<Logger level="DEBUG" name="org.apache.http"/>
```

## Available SOAP Operations
 - Login
 - DescribeSOBject (only 'Lead' and 'Contact'  object type supported)
 - GetUserInfo
 - Query (Only supports a SoQL query of `SELECT Id,FirstName,LastName,Company,Email,Phone,Product_Purchased__c FROM Lead`)
 - DescribeGlobal
