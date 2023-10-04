1. Expand the SQL Server Agent node and right click the Jobs node in SQL Server Agent and select `'New Job'`

2. In the `'New Job'` window enter the name of the job and a description on the `'General'` tab.

3. Select `'Steps'` on the left hand side of the window and click `'New'` at the bottom.

4. In the `'Steps'` window enter a step name and select the database you want the query to run against.

 
5. Paste in the T-SQL command you want to run into the Command window and click `'OK'`.
   
```sql
USE DigitalCreditPaper;  
-- Application.Applications.CustomerName  
UPDATE [Application].[Applications]  
SET CustomerName = LEFT(CustomerName, 4) + 'xxxxxxxx'

-- Customer.CustomerDetail.Name  
UPDATE [Customer].[CustomerDetail]  
SET Name = LEFT(Name, 4) + 'xxxxxxxx'

-- Customer.CustomerDetail.ParentName  
UPDATE [Customer].[CustomerDetail]  
SET ParentName = LEFT(ParentName, 4) + 'xxxxxxxx'

-- Customer.CustomerDetail.UltimateParentName  
UPDATE [Customer].[CustomerDetail]  
SET UltimateParentName = LEFT(UltimateParentName, 4) + 'xxxxxxxx'
```   

6. Click on the `'Schedule'` menu on the left of the New Job window and enter the schedule information (e.g. daily and a time).

7. Click `'OK'` - and that should be it.