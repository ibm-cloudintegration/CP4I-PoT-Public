# IBM API Connect v12

## Create, Secure, Publish, Subscribe, and Test an API

[Return to main APIC lab page](../ReadMe.md#lab-abstracts)

---

# Table of Contents
- [1. Introduction](#introduction)
- [2. IBM App Connect - Deploying the backend REST Service](#deploy)
- [3. Import an API into the Developer Workspace](#import_api)
	* [3a. Create project](#create-project)
	* [3b. Add API ](#add-api)
	* [3c. Configure Gateway Policy](#config-api-gateway-policy)
	* [3d. Configure CORS](#config-api-cors)
	* [3e. Configure Security](#config-api-security)
- [4. Publish API](#publish-api)
- [5. API Connect Developer Portal<](#devportal)
	* [5a. Subscribe API](#devportal-subscribe)
- [6. Test the API](#test-api)
- [7. Summary](#summary)

---

# 1. Introduction <a name="introduction"></a>

In this lab, you will get a chance to use the IBM API Connect (APIC) Studio and its intuitive interface to import and edit an API using the OpenAPI definition (YAML) of an existing Customer Database RESTful web service.

In this tutorial, you will explore the following key capabilities:

-   Creating an API by importing an OpenAPI definition for an existing backend REST service

-   Configuring ClientID/Secret Security, endpoints, CORS, and proxy to invoke an endpoint

-   Publish API to **IBM DataPower API Gateway** and to Developer Portal

-   Testing a REST API in the Developer Portal

<br>

![alt text](./images/apic-lab1-component-diagram.png)


<br>

# 2. IBM App Connect - Deploying the backend REST Service <a name="deploy"></a>

First, you will deploy a Customer Database REST service and then you will download the OpenAPI file for the Customer Database REST service that you deployed.

1. In a browser, enter the URL for the Platform Navigator URL that is provided by your instructor.


1. Filter instances by the student(number). You will see your instances.(br)

1. Navigate to the **App Connect Dashboard**.
![alt text](./images/image-1.png)

1. Click on the **Dashboard** icon in the left navigation.
![alt text](./images/93.png)

1. For this lab, we already have the REST service built and available as a **bar** file. You can download the **CustomerDatabaseV3.bar** file for the service [<u>**here**</u>](./resources/CustomerDatabaseV3.bar).

1. Click on **Deploy integrations**.
![alt text](./images/94.png)


1. Click **Quick start integration** and click **Next**.
![alt text](./images/95.png)


1. Drag and drop the BAR file that you just downloaded or click to upload.  Once you have dragged and dropped or uploaded, you will see the bar file listed under **to be imported**.  Click **Next**.
![alt text](./images/96.png)

1. Click **Next**.
![alt text](./images/97.png)

1. Give the Integration Server a **Name** (e.g., student(n)-customerdb) and click **Create**. Replace (n) with your student number, for example student1-customerdb. <br>
![alt text](./images/98.png)

1. This will take you back to the Runtimes Dashboard where you will see your new server. It will likely be showing Pending while it is starting up the pod.

	**Note:** It may take a several minutes to start up. You can refresh the page. Once it is up and running it will show the following:

	Click on the newly created Runtime.
![alt text](./images/99.png)


1. Confirm that the **Overview** tab is selected and click **Download OpenAPI Document As JSON (or) Download OpenAPI Document As YAML**. Either format can be used to import in API Connect.<br>
![alt text](./images/103.png)


<br><br>

# 3. IBM Api Connect - Import backend REST API <a name="import_api"></a>

You will be importing the backend REST API definition into IBM API Connect Studio, then you will configure the API to enable Security, CORS, and finally publish the API to community. <br>

1. Navigate to the API Connect instance.

From the IBM Cloud Pak for Integration Platform Navigator, navigate to apim-demo an IBM API Connect capability. <br>

Click on apim-demo instance. <br>
\![alt text](images/6.png)

1. If this is your first time logging in, the login page is presented. Click **Cloud Pak User Registry**.
![alt text](images/8.png)

1. Confirm that you are in the provider organization for your username (upper right).
![alt text](images/9.png)

1. We are now able to begin to create APIs and Products.  Click **API Studio**
![alt text](images/10.png)



## 3a. Create project <a name="create-project"></a>

1. Click **Create New Project**.
![alt text](images/12.png)

	Name it customer-database-agw, where agw stands for the API Gateway. <br>
![alt text](images/12a.png)

1.  Open the project customer-database-agw. 
![alt text](images/12b.png)


## 3b. Add API <a name="add-api"></a>

1. Click "Add API"
![alt text](images/12c.png)

1. Click "Import". 
![alt text](images/12d.png)

1. Click on "drag and drop" 
![alt text](./images/12e.png)

1. Select Customer_Database-1.0.0.yaml <br>
![alt text](./images/12f.png)

1. Click \<Create\>. <br>
![alt text](./images/12g.png)

	Your backend REST API has been imported successfully. <br>


## 3c. Configure API - Add Gateway Policy<a name="config-api-gateway-policy"></a>

1. Click (+) sign next to "Policy Sequence". <br>
![alt text](./images/13a.png)

1. Select "DataPower API Gateway", and name the policy as "customer-database-agw-policy", then select the API using the drop-down. <br>
Click \<Add\>.
![alt text](./images/13b.png)

1. Click on "Invoke" policy. <br>
![alt text](./images/13c.png)

	Append "$(api.operation.path)" at the end of the backend URL. <br>
![alt text](./images/13d.png)



## 3d. Configure CORS<a name="config-api-cors"></a>

1. Click on the API Customer_Database under APIs section (left), then scroll down and click on CORS (Cross-Origin Resource Sharing). <br>

1. Click <\Add\>. <br>
![alt text](./images/14a.png)

1. Enter name, namespace (project), then click <\Add\>. <br>
![alt text](./images/14b.png)

1. Edit CORS. <br>
![alt text](./images/14c.png)

	SCROLL down, and uncheck "Expose headers", then Save. <br>
![alt text](./images/14d.png)


## 3e. Configure Security<a name="config-api-security"></a>

1. Click the Components section
Scroll down to "Components" section, then on the right side again scroll down to "Security Schemas" section. <br>

1. Click <\Add Security Schema\>. <br>
![alt text](./images/15a.png)

1. Add "X-IBM-Client-Id". <br>
![alt text](./images/15b.png)

1. Similarly, add "X-IBM-Client-Secret". <br>
![alt text](./images/15c.png)

1. Now, click "Security" section and then click on <\Add Security Schema\>. <br>
![alt text](./images/15d.png)

	First, select both apikeys, then click on <\Create AND group (2 selected)\> button. <br>
![alt text](./images/15e.png)


	Now, click <\Add\>. <br>
	![alt text](./images/15f.png) <br>

	![alt text](./images/15g.png)


<br>


# 4. Publish API<a name="publish-api"></a>

Here, you will publish the API to IBM DataPower API Gateway and Developer Portal community for consuming the API. <br>

1. Click on "Publish" 
![alt text](./images/image-18.png)

	![alt text](./images/image-19.png)

	![alt text](./images/image-20.png)

1. Click on Catalog button. Don't worry if that little window disappears quickly, you should be able to access the Catalog through Manage section in the left. <br>
![alt text](./images/image-21.png)

1. Navigate to the Portal Section under Catalog Settings, then click on the Portal URL. <br>
![alt text](./images/image-22.png)

<br>


# 5. API Connect Developer Portal<a name="devportal"></a>

1. Welcome to developer portal
![alt text](./images/image-23.png)

1. Click on \<Sign up\> button. <br>
![alt text](./images/image-24.png)
![alt text](./images/image-25.png)

1. Login as student(n) now. <br>
![alt text](./images/image-26.png)


1. THis is the Developer Portal Welcome page. <br>
![alt text](./images/image-27.png)

1. Click on "API Products". <br>
![alt text](./images/image-28.png)

1. You should see Customer_Database API that was published earlier, then Click on the API. <br>
![alt text](./images/image-29.png)


## 5a. Subscribe API <a name="devportal-subscribe"></a>

1. Subscribe the API
![alt text](./images/image-30.png)

1. Click <\Subscribe\>
![alt text](./images/image-31.png)

1. Click "Create new subscription", then click <\Request\>. <br>
![alt text](./images/image-32.png)

1. Click <\Save\>. <br>
![alt text](./images/image-33.png)


1. Click on the demo-app. You should see that your subscription is successful, and acknowledged by the DataPower API Gateway. <br>

	You should also see ClientID, and ClientSecret being generated. <br>
![alt text](./images/image-34.png)

	**SAVE the ClientID, and ClientSecret to a NOTEPAD or TEXTPAD.** You will need them when testing the API. <br> 


<br> <br>


# 6. Test the API <a name="test-api"></a>


1. Click on "API Products".
![alt text](./images/image-35.png)

1. Click on the API Product Customer_Database-product, then click on the API.
![alt text](./images/image-37.png)

1. Expand "API Resources".
![alt text](./images/image-38.png)

1. Navigate to GET under /customers operation. <br>
![alt text](./images/image-39.png)

1. Click Headers tab to populate our ClientId, and Secret. <br>
![alt text](./images/image-40.png)

1. The ClientID should be populated automatically, you need to populate X-IBM-Client-Secret and its value that saved into the Notepad. <br>

1. Click **<\Send\>**. <br>
![alt text](./images/image-41.png)


1. If successful, you should get "200 OK" Result.
![alt text](./images/image-42.png)


<br><br>


# 6.Summary <a name="summary"></a>

Congratulations, you have completed the **Create, Secure, publish, subscribe, and tested your API**. Throughout the lab, you learned how to:

-   Create an API by importing an OpenAPI definition for an existing REST service

-   Configure ClientID/Secret Security, endpoints, CORS, and proxy to invoke endpoint

-   Publish an API for developers

-   Test a REST API in the Developer Portal

[Return to main APIC lab page](../ReadMe.md#lab-abstracts)
