# Exercise 1 - Discover, design and run pre-built standard integration on Edge Integration Cell

In the previous exercise, you have familiarized yourself with the SAP Integration Suite capabilities and navigation. Now let's look at how we can discover, design and run pre-built standard integrations on Edge Integration Cell. In this exercise, we will use a pre-built standard content to connect to an SAP S/4HANA backend system, trigger execution of the content deployed on Edge Integration Cell and perform operations like update of the S/4HANA data objects.

### Note

For all the subsequent steps in this exercise, please replace the **XX** in **userXX** with your respective id e.g user99.

##  Description

After completing these steps, you will have deployed a standard integration on Edge Integration Cell and successfully executed it with the on-premise SAP S/4HANA system.

1. Navigate back to Home. In the Home page navigate to Capabilities and click on "Discover Integrations" under Build Integration Scenarios tile.

<br>![](/exercises/ex3/images/image.png)

2.  In the "Discover (Integrations)" view, navigate to the Search text box and enter the following package name, then click Enter:

```yaml 
SAP Order Management Foundation Integration with SAP S/4HANA
```

3. From the list of results, click on the listed package "SAP Order Management Foundation Integration with SAP S/4HANA".

<br>![](/exercises/ex3/images/package%20search.png)

4.  In the package detail view, click on Copy button placed at top-right corner of the detail view.

<br>![](/exercises/ex3/images/4.png)

5.  In the Messages pop-up, click on "Create copy" to create a named copy.

<br>![](/exercises/ex3/images/5.png)

6.  In the Provide suffix pop-up, enter the username that was provided to you. Clear the existing text which is shown as timestamp and enter username **userXX** with **XX** the number assigned to you, and Click OK.

<br>![](/exercises/ex3/images/6.png)

8.  Upon confirmation, a toast message "Package copied" will be shown. Click Close in the messages pop-up.

<br>![](/exercises/ex3/images/7.png)

9.  Click Design from the sub navigation item in the left pane and click on "Integrations and APIs" and search the copied package (see the next step).

<br>![](/exercises/ex3/images/8.png)

10.  In the search box, type **userXX** which you used as suffix during package copy operation. Package name with suffix as ".userXX" be listed e.g. "SAP Order Management Foundation Integration with SAP S/4HANA.user130". 
Click the listed package and navigate to the Package details view.

<br>![](/exercises/ex3/images/9.png)

12.  Click on Artifacts tab and click the Configure entry from the Actions menu of the "Replicate Order from SAP Order Management Foundation to SAP S4HANA" integration flow.

<br>![](/exercises/ex3/images/10a.png)

13.  In the "Configure Selected Artifacts" dialog, change the following parameter under Sender tab under Connection section. Suffix the Address with the **userXX** assigned to you: **/s4onpremise/order_userXX**.

<br>![](/exercises/ex3/images/changesenderaddress.png)

14.  Switch to the Receiver tab and change the following parameter values:

<br>In the "Address" field, copy and paste: 
```yaml 
https://proxyavrdev.hana.ondemand.com/Proxy/jenkslave55.cpi.c.eu-de-1.cloud.sap/9912/sap/bc/srt/scs_ext/sap/salesorderbulkrequest_in
```

<br> In the "Proxy Type" field choose **Internet** from the drop down menu,

and for "Authentication", choose **None** from the drop down menu.

After changing the values, click on "Save"

<br>![](/exercises/ex3/images/changereceiveraddress.png)

15. Ignore the popup with the warnings, and click "Deploy".

<br>![](/exercises/ex3/images/configureanddeploy.png)

16.	In the upcoming dialog, select the Runtime Profile as "Edge Integration Cell" from the drop-down, since we want to deploy this integration flow to this runtime. And click Yes.

<br>![](/exercises/ex3/images/deployonedge.png)

17.	Click Ok on the Deployment confirmation dialog. 

<br>![](/exercises/ex3/images/confirmdeployment.png)

18.	Once the deployment is successful, a confirmation message will be shown.

<br>![](/exercises/ex3/images/deployedsuccess.png)

19.	Click on "Integrations and APIs" from the Monitor navigation item on the left pane. 

<br>![](/exercises/ex3/images/navigatetomonitorview.png)

20.	In the Overview page, from the listed Runtime, select "Edge Integration Cell - ..." where the artifact was deployed to.

<br>![](/exercises/ex3/images/chooseedgeinmonitoring.png)

21.	For the selected Edge runtime, click on tile "All" under "Manage Integration Content".

<br>![](/exercises/ex3/images/tileselect.png)

22.	Verify that your integration flow is in **Started** state. Check the details like ID; it should be suffixed with your user - **userXX**. If there are too many log entries, you can filter based on your user.

<br>![](/exercises/ex3/images/iflowstarted.png)

23.	Copy the generated endpoint.

<br>![](/exercises/ex3/images/copyendpoint.png)

24.	Open the Insomnia installed in your system.
    
25.	Use "Scratch Pad" option when prompted to login.

<br>![](/exercises/ex3/images/insomniascratchpad.png)

26. Create a new HTTP Request by clicking on '+' sign.

<br>![](/exercises/ex3/images/insomnianewrequest.png)

27. Change the Request method from 'GET' to 'POST' and paste the URL copied beforehand in the URL box.

<br>![](/exercises/ex3/images/insomnianewpostrequest.png)

28. Set the payload. In the 'Body' tab, select JSON to add the JSON payload.

<br>![](/exercises/ex3/images/insomniasetbody.png)

29. Add the following payload in the body text area.

```json
{
  "id": "dc3ea1c1-b4fb-4fa0-a83f-c6ae843b879c",
  "orderId":"dabe136b-8efd-45de-a792-b73596af25f9",
  "fulfillmentRequestId": "f876e666-ed01-4435-8ff2-8f3e8a276389",
  "version": 1,
  "orderNumber": 456789,
  "precedingDocument": null,
  "metadata": {
    "createdAt": "2020-03-27T17:16:52.968Z",
    "createdBy": null,
    "changedAt": "2020-03-27T15:16:52.968Z",
    "changedBy": null
  },
  "owner": "ruth@domain.com",
  "market": {
    "marketId": "A1",
    "marketName": "US East",
    "currency": "EUR",
    "salesArea": {
      "salesOrganization": "1710",
      "distributionChannel": "10",
      "division": "00"
    }
  },
  "timeZone": "America/New_York",
  "paymentData": [
    {
      "method": "Card",
      "paymentCardToken": "as324dad333dddas22415ga"
    }
  ],
  "customer": {
    "customerNumber": "17100009",
    "addresses": [
      {
        "street": "Billing Street",
        "houseNumber": "1196",
        "building": "buildBill-1",
        "roomNumber": "11",
        "floorNumber": "1",
        "postalCode": "H1A 1H6",
        "city": "Montreal",
        "country": "CA",
        "district": "bill2-district",
        "state": "QC",
        "phone": "5141112233",
        "email": "Bill@Samplecustomer.Com",
        "fax": "5141113344",
        "additionalAddressInfo": null,
        "correspondenceLanguage": "Fr",
        "addressType": "BILL_TO",
        "person": {
          "firstName": "Bill",
          "middleName": "MiddleBill",
          "lastName": "LastNameBill",
          "academicTitle": "Ms"
        },
        "pOBox": "1100"
      },
      {
        "street": "Shipping Street",
        "houseNumber": "2242",
        "building": "ship-2",
        "roomNumber": "22",
        "floorNumber": "2",
        "postalCode": "24152",
        "city": "Chicago",
        "country": "US",
        "district": "ship2-district",
        "state": "IL",
        "phone": "2122223344",
        "email": "Ship2@Samplecustomer.Com",
        "fax": "2122224455",
        "additionalAddressInfo": "test notes ship",
        "correspondenceLanguage": "En",
        "addressType": "SHIP_TO",
        "person": {
          "firstName": "Shipster",
          "middleName": "MiddleShip",
          "lastName": "LastNameShip",
          "academicTitle": "Mr"
        },
        "pOBox": "abc"
      }
    ]
  },
  "description": "ruth's order",
  "status": "RELEASED",
  "priceType": "Net",
  "customReferences": [],
  "orderItems": [
    {
      "id": "4cd1629a-85be-41b4-b379-656288f25b21",
      "lineNumber": "1",
      "itemType": "physicalItem",
      "quantity": {
        "value": 3,
        "unit": "PCE"
      },
      "product": {
        "id": "e0981039-8298-464e-a8f0-32be92a8ba32",
        "sourceSystemReference": {
          "sourceSystemProductId": "TG11"
        }
      },
      "customReferences": [],
      "price": {
        "aspectsData": {
          "physicalItemPrice": {
            "priceTotals": [
              {
                "priceCategory": "onetime",
                "finalAmount": 40.68
              }
            ]
          }
        }
      },
      "aspectsData": {
        "physicalItem": {
          "scheduleLines": [
            {
              "deliverySource": {
                "sourceId": "1710",
                "sourceType": "STORE",
                "sourceName": "Downtown"
              },
              "availableFrom": "2020-03-28T19:16:52.968Z",
              "quantity": {
                "unit": "PCE",
                "value": 3
              }
            }
          ]
        }
      }
    }
  ]
}
```
<br>![](/exercises/ex3/images/insomniabodypayload.png)

30. Navigate to 'Auth' tab and select 'Basic Auth'

<br>![](/exercises/ex3/images/insomniasetbasicauth.png)

31.	Add the following credentials

<br>USERNAME =
```yaml
sb-3009327f-3dc1-4e3e-9853-5bd7c23e221d!b44358|it-rt-cpisuite-europe-03!b18631
```
<br>PASSWORD = 
```yaml 
e507568e-892c-443f-a6ba-4d53f76fecac$wS5Kq2nV25PlNT-U8bh8Yd-HGoBZpO-XW7Za9X3URE0=
```
<br>![](/exercises/ex3/images/insomniabasicauthset.png)

32.	Trigger the message by clicking on 'Send'. Upon success, you will receive '200 OK' status as a response. Copy the "message ID" from the response 'message'.

<br>![](/exercises/ex3/images/insomniasuccessfulpost.png)

33. Switch back to the Integration Suite UI, and navigate to the monitoring overview page.

<br>![](/exercises/ex3/images/navigatebacktooverview.png)

34. Navigate to tile "All Artifacts" under "Monitor Message Processing"

<br>![](/exercises/ex3/images/mpltile.png)

35.	Search the corresponding message processing log using the "message ID" copied in Step 32 by putting it in the ID search box and click enter. A completed message processing entry will be shown against the "Message ID", if message processing was successful.

<br>![](/exercises/ex3/images/mplsuccess.png)

## Summary

You've now completed the following:
1. Discover and use standard integration content
2. Configure and deploy it on Edge Integration Cell
3. Send message to the backened system using an Integration flow

Continue to - [Exercise 2 - Design and run an API on Edge Integration Cell](../ex4/README.md)

