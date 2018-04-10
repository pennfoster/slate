# Errors

## HTTP Errors

All errors will send back an additional JSON message.

Error Code | Meaning
---------- | -------
400 | Bad Request
401 | Unauthorized
404 | Not Found
500 | Internal Server Error
503 | Service Unavailable

## Penn Foster System Codes

Error Code | Meaning
---------- | -------
E601400001 | Country is invalid
E601400002 | Country is required
E602500001 | Employee Id is required
E602500002 | Student already has an active enrollment
E602600001 | Invalid student email address.
E604000001 | Zip code must be entered  
E604100001 | Email address must be entered  
E604100002 | Invalid email address
E604200001 | Invalid phone type  
E604300001 | Phone number must be entered when there is a phone type   
E607100001 | Invalid parent id
E607200001 | Invalid location id  
E607300001 | Invalid client id
E607400001 | Student name must be entered  
E607700001 | Address line 1 must be entered   
E607700002 | Action code is invalid
E607800001 | City must be entered  
E607900001 | Invalid state code    
E608600001 | Alternate id alrady exists
E608600002 | Alternate id is required
E614400001 | Invalid product code   
E614400002 | Invalid module or lesson
E614400003 | Module or lesson is obsolete
E614400005 | Product code already exists for student
E614400006 | Product code is not active or current - field IMSRP3 on F4101LB
E999999001 | Order is currently being processed by:  
