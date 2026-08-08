# App Connect MCP Servers Bob

[Return to MQ lab page](../index.md)


## Pre-reqs

Free trial of Bob

https://bob.ibm.com/trial
<br>

![alt text](image.png)

![alt text](image-1.png)

![alt text](image-2.png)

![alt text](image-3.png)

<br>


## App Connect Dashboard 

### Deploy Customer Database REST API

![alt text](image-13.png)

Click Quick Start , then click \<Next\>. <br>

![alt text](image-14.png)


![alt text](image-15.png)

![alt text](image-16.png)

![alt text](image-17.png)

![alt text](image-18.png)

![alt text](image-19.png)

![alt text](image-20.png)

<br><br>

### Create MCP Servers

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)

![alt text](image-7.png)

![alt text](image-8.png)

![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)

Capture MCP Server Basic Auth Credentials. <br>
![alt text](image-12.png)





## Bob
	
### Add Customer Database MCP Server 

Open the IBM Bob IDE, and navigate to Settings <br>

![alt text](image-21.png)

Navigate to MCP. <br>

![alt text](image-22.png)

Click + sign. <br>

![alt text](image-23.png)

![alt text](image-24.png)

![alt text](image-25.png)
Append the below between the curly braces. <br>
```
    "customer-database-v3": {
        "url": "",
        "headers": {
            "Authorization": ""
        }
    }
```

![alt text](image-26.png)

Now, populate the url, and Authorization values from the MCP Server created in the App Connect Dashboard. <br>

![alt text](image-27.png)

![alt text](image-28.png)

Now, save and close mcp.json. <br>

Notice that customer-databasev-v3 is connected to the MCP server. <br>

![alt text](image-29.png)


### Run prompts


![alt text](image-30.png)

Click on Approve. <br>

![alt text](image-31.png)

Notice that Bob called the backend MCP server and the REST API and retrived list of customers. <br>

![alt text](image-32.png)

Let's add few Customers using below prompt. <br>
```
add customer, firstname Joe, lastname Jodl, address 144 marina drive, edison, nj, zip code 11111-1111
```
Notice that Bob automatically formed the JSON payload for addCustomer operation. <br>
![alt text](image-33.png)

Click "Approve Once". <br>

Notice that Customer 11 was created Successfully.
![alt text](image-34.png)

## Summary

[Return to ACE lab page](../index.md)