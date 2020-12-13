# SaaS-Sample
A simple app that introduces you to how to develop a multitenant application on SAP Cloud.

ref:  
 - https://developers.sap.com/tutorials/cp-cf-security-xsuaa-create.html
 - https://developers.sap.com/tutorials/cp-cf-security-xsuaa-multi-tenant.html


## Key Points
1. XSUAA Service (SAP User Authentication and Authorization)
2. SaaS Provisioning Service (SaaS Register)

### XSUAA Service
XSUAA is a UAA service used within SAP.  
Like a typical UAA service, it is used integrated with IDP and does not store direct user information, but instead takes e-mail and id values that can be keys and maps them with the Role.  
Configuration of the XSUAA service can be found in the `security/xs-security.json` file and is used as defined.  

### SaaS Provisioning Service (SaaS Register)
SaaS Provisioning is a service that registers SaaS App/Service and manages Lifecycle for use by other Tenants.  
It is a function that supports onboarding/offboarding and subscribing to App/Service through UI/API.  
Settings can be found in `config.json`.  

### How does it work?
Before deploying the SaaS app, you should pre-deploy the services that bind together.
``` bash
## Create the XSUAA service instance with the xs-security.json security descriptor file.
cf create-service xsuaa application xsuaa-service-tutorial -c security/xs-security.json

## Create the SaaS Provisioning service instance with the config.json file.
cf create-service saas-registry application saas-registry-tutorial -c config.json

## deploy the application with the updated manifest.yml file.
cf push
```