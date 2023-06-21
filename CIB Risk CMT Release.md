
## Steps

1. Send Email:
   Attach testing outline
```
Good day @CIB Credit Risk System Support

  

Would you please assist us with a Standard Change Production Deployment for DCP?  
  

Deployment is set for the Thursday **22nd June 2023 from 10:00 am - 12:00 pm**  

Changes included:

- Prod Bug - East African Breweries Limited CIF 502674189 - CCAP Breach   
    

- If there are no changes to facilities we should not be sending anything to customer service. This problem might be because we are sending empty facilities to customer svc and then we are getting a null proposed CCAP. If proposed CCAP is null, it needs to default to CCAP.
    

- Limit Switch Credit Paper Type - Feature is hidden behind feature toggle  
    

- _Please see sheet 20230622 in attached excel_

  

  

Pipelines to deploy:

- digital-credit-paper-app-vdc release 1.0.1384  
    
- digital-credit-paper-db-vdc release 1.0.824  
    
- digital-credit-paper-svc-vdc release 1.0.1032  
    

@Cornelius, Beverley (Credit Division), would you please assist us with Business Approval for the above change?
```

2. Deploy All Pipelines(Dagon) to production
3. 