# IBM API Connect

## Create and Secure an API to Proxy an Existing REST Web Service

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

-   Publish an API for developers into Developer Portal 

-   Testing a REST API in the Developer Portal

<br>

![alt text](./images/apic-lab1-component-diagram.png)


<br>

# 2. IBM App Connect - Deploying the backend REST Service <a name="deploy"></a>

First, you will deploy a Customer Database REST service and then you will download the OpenAPI file for the Customer Database REST service that you deployed.

1\. In a browser, enter the URL for the Platform Navigator URL that is provided by your instructor.


2\. Filter instances by the student(number). You will see your instances.(br)

3\. Navigate to the **App Connect Dashboard**.

![alt text][pic92]

4\. Click on the **Dashboard** icon in the left navigation.

![alt text][pic93]

5\. For this lab, we already have the REST service built and available as a **bar** file. You can download the **CustomerDatabaseV3.bar** file for the service [<u>**here**</u>](./resources/CustomerDatabaseV3.bar).

6\. Click on **Deploy integrations**.

![alt text][pic94]

7\. Click **Quick start integration** and click **Next**.

![alt text][pic95]

8\. Drag and drop the BAR file that you just downloaded or click to upload.  Once you have dragged and dropped or uploaded, you will see the bar file listed under **to be imported**.  Click **Next**.

![alt text][pic96]

9\. Click **Next**.

![alt text][pic97]

10\. Give the Integration Server a **Name** (e.g., student(n)-customerdb) and click **Create**. Replace (n) with your student number, for example student1-customerdb. <br>

![alt text][pic98]


11\. This will take you back to the Runtimes Dashboard where you will see your new server. It will likely be showing Pending while it is starting up the pod.

**Note:** It may take a several minutes to start up. You can refresh the page. Once it is up and running it will show the following:

Click on the newly created Runtime.

![alt text][pic99]


12\. Confirm that the **Overview** tab is selected and click **Download OpenAPI Document As JSON (or) Download OpenAPI Document As YAML**. Either format can be used to import in API Connect.<br>

![alt text][pic103]

[pic0]: images/0.png
[pic1]: images/1.png
[pic2]: images/2.png
[pic3]: images/3.png
[pic4]: images/4.png
[pic5]: images/5.png
[pic91]: images/91.png
[pic92]: images/92.png
[pic93]: images/93.png
[pic94]: images/94.png
[pic95]: images/95.png
[pic96]: images/96.png
[pic97]: images/97.png
[pic98]: images/98.png
[pic99]: images/99.png
[pic100]: images/100.png
[pic101]: images/101.png
[pic102]: images/102.png
[pic103]: images/103.png

<br><br>

# 3. IBM Api Connect - Import backend REST API <a name="import_api"></a>

You will be importing the backend REST API definition into IBM API Connect Studio, then you will configure the API to enable Security, CORS, and finally publish the API to community. <br>

1\. Navigate to the API Connect instance.

From the IBM Cloud Pak for Integration Platform Navigator, navigate to apim-demo an IBM API Connect capability. <br>

Click on apim-demo instance. <br>

![alt text][pic6]


2\. If this is your first time logging in, the login page is presented. Click **Cloud Pak User Registry**.

![alt text][pic8]

3\. Confirm that you are in the provider organization for your username (upper right).

![alt text][pic9]


4\. We are now able to begin to create APIs and Products.  Click **API Studio**

![alt text][pic10]



## 3a. Create project <a name="create-project"></a>

1\. Click **Create New Project**.

![alt text][pic12]

Name it customer-database-agw, where agw stands for the API Gateway. <br>

![alt text](images/12a.png)

2\.  Open the project customer-database-agw. 

![alt text](images/12b.png)


## 3b. Add API <a name="add-api"></a>

![alt text](images/12c.png)

![alt text](images/12d.png)

![alt text](image-1.png)

Select Customer_Database-1.0.0.yaml <br>

![alt text](image.png)

Click \<Create\>. <br>

![alt text](image-2.png)

Your backend REST API has been imported successfully. <br>

## 3c. Configure API - Add Gateway Policy<a name="config-api-gateway-policy"></a>

Click (+) sign next to "Policy Sequence". <br>

![alt text](image-3.png)

Select "DataPower API Gateway", and name the policy as "customer-database-agw-policy", then select the API using the drop-down. <br>
Click \<Add\>.

![alt text](image-4.png)

Click on "Invoke" policy. <br>

![alt text](image-5.png)

Append "$(api.operation.path)" at the end of the backend URL. <br>

![alt text](image-6.png)


## 3d. Configure CORS<a name="config-api-cors"></a>

Click on the API Customer_Database under APIs section (left), then scroll down and click on CORS (Cross-Origin Resource Sharing). <br>

Click <\Add\>. <br>

![alt text](image-7.png)

Enter name, namespace (project), then click <\Add\>. <br>

![alt text](image-8.png)

Edit CORS. <br>

![alt text](image-9.png)

SCROLL down, and uncheck "Expose headers", then Save. <br>

![alt text](image-10.png)


## 3e. Configure Security<a name="config-api-security"></a>

Scroll down to "Components" section, then on the right side again scroll down to "Security Schemas" section. <br>

Click <\Add Security Schema\>. <br>

![alt text](image-11.png)

Add "X-IBM-Client-Id". <br>

![alt text](image-12.png)

Similarly, add "X-IBM-Client-Secret". <br>

![alt text](image-13.png)

Now, click "Security" section and then click on <\Add Security Schema\>. <br>

![alt text](image-14.png)

First, select both apikeys, then click on <\Create AND group (2 selected)\> button. <br>

![alt text](image-15.png)

Now, click <\Add\>. <br>

![alt text](image-16.png)

![alt text](image-17.png)




# 4. Publish API<a name="publish-api"></a>

Here, you will publish the API to IBM DataPower API Gateway and Developer Portal community for consuming the API. <br>

![alt text](image-18.png)

![alt text](image-19.png)

![alt text](image-20.png)

Click on Catalog button. Don't worry if that little window disappears quickly, you should be able to access the Catalog through Manage section in the left. <br>

![alt text](image-21.png)

Navigate to the Portal Section under Catalog Settings, then click on the Portal URL. <br>

![alt text](image-22.png)


# 5. API Connect Developer Portal<a name="devportal"></a>

![alt text](image-23.png)

Click on <\Sign up\> button. <br>

![alt text](image-24.png)

![alt text](image-25.png)

Login as student(n) now. <br>

![alt text](image-26.png)


THis is the Developer Portal Welcome page. <br>

![alt text](image-27.png)

Click on "API Products". <br>

![alt text](image-28.png)

You should see Customer_Database API that was published earlier, then Click on the API. <br>

![alt text](image-29.png)


## 5a. Subscribe API <a name="devportal-subscribe"></a>

Subscribe the API

![alt text](image-30.png)

![alt text](image-31.png)

![alt text](image-32.png)

![alt text](image-33.png)

Click on the demo-app. You should see that your subscription is successful, and acknowledged by the DataPower API Gateway. <br>

You should also see ClientID, and ClientSecret being generated. <br>

**SAVE the ClientID, and ClientSecret to a NOTEPAD or TEXTPAD.** You will need them when testing the API. <br> 

![alt text](image-34.png)





# 6. Test the API <a name="test-api"></a>


Click on "API Products". <br>

![alt text](image-35.png)

Click on the API Product Customer_Database_product, then click on the API. <br>

![alt text](image-36.png)

![alt text](image-37.png)

Expand "API Resources". <br>

![alt text](image-38.png)

![alt text](image-39.png)

Click Headers tab to populate our ClientId, and Secret. <br>

![alt text](image-40.png)

The ClientID should be populated automatically, you need to populate X-IBM-Client-Secret and its value that saved into the Notepad. <br>

Then click **<\Send\>**. <br>

![alt text](image-41.png)


If successful, you should get "200 OK" Result.

![alt text](image-42.png)





![alt text][pic15]
    
[pic6]: images/6.png
[pic7]: images/7.png
[pic8]: images/8.png
[pic9]: images/9.png
[pic10]: images/10.png
[pic11]: images/11.png
[pic12]: images/12.png
[pic13]: images/13.png
[pic14]: images/14.png
[pic15]: images/15.png
[pic104]: images/104.png
















# 6.Summary <a name="summary"></a>

Congratulations, you have completed the **Create and Secure an API** lab. Throughout the lab, you learned how to:

-   Create an API by importing an OpenAPI definition for an existing REST service

-   Configure ClientID/Secret Security, endpoints, and proxy to invoke endpoint

-   Test a REST API in the Developer Toolkit

-   Publish an API for developers

[Return to main APIC lab page](../ReadMe.md#lab-abstracts)
