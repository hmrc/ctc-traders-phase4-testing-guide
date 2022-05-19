---
title: CTC Traders phase 4 testing guide
weight: 1
description: Software developers, designers, product owners or business analysts. Integrate your software with Common Transit Convention Traders API.
---

# CTC Traders phase 4 testing guide

##Useful CTC page links

[CTC Traders API Roadmap](/roadmaps/common-transit-convention-traders-roadmap/)

[CTC Traders API Documentation](/api-documentation/docs/api/service/common-transit-convention-traders/1.0)

[CTC Traders API Service Guide](/guides/ctc-traders-phase4-service-guide/)

##Introduction

This guidance page signposts software developers to essential information and materials.

This is needed when testing to check your software is compatible and will work with our CTC Traders API.

Scroll down the page for further instructions.

##Before you start

When you are ready to test your software, first read and understand the [CTC Traders API Service Guide](/guides/common-transit-convention-traders-service-guide/).

We strongly advise you to start testing your software for compatibility purposes as soon as possible.

##What is Trader Test?

**Before you can get access to the live production environment, you must check that your software is fully compatible with our CTC Traders API.**

Trader Test simulates both the automated responses and also the real life experience where NCTS support staff do the tasks of Border Force personnel.

When your testing requires a manual response, they will perform the live manual steps of the process. This simulates and tests a full real-life journey from start to finish for you.

You can do this by performing a series of compatibility tests on your software using our sandbox environment. This is a replica of the live production environment. You’ll also need to do some sample scenarios and test data for both Great Britain and Northern Ireland.

##Get set up for testing

1. First **register** for a developer account. You can do this by following the instructions on the [Using the Developer Hub](/api-documentation/docs/using-the-hub) page.
2. [**Sign back in**](/developer/login) to the HMRC Developer Hub.
3. **Create an application** by going to the Create Test User API.
4. Then **create another application** by going to the [Common Transit Convention Traders API](/api-documentation/docs/api/service/common-transit-convention-traders/1.0).
5. **Create a user ID and password** for either an [individual](/api-documentation/docs/api/service/api-platform-test-user/1.0#_create-a-test-user-which-is-an-individual_post_accordion) or an [organisation](/api-documentation/docs/api/service/api-platform-test-user/1.0#_create-a-test-user-which-is-an-organisation_post_accordion).
6. **Subscribe to our Common Transit Convention Traders API** on the Developer Hub under the section called Your Specific Applications.
7. **Create a Client ID and Client Secret.**
8. Use the [Create Test User API](/api-documentation/docs/api/service/api-platform-test-user/1.0) to **generate a new test user**. Ensure that the test user has the correct enrolment by including the following request body in the call to the Create Test User API:

    ```json
    {   
        "serviceNames": [     
            "common-transit-convention-traders"   
        ] 
    }
    ```
9. You will also need to access and use the [NCTS Trader Test Access and Channels](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/940784/NCTS_Trader_Test_Access_Channels_and_Support_v1.1.pdf) reference guide (ODT document opens and downloads). You will need this guide to help you navigate between the old XML based system and our new API.

##How to test your software

First, download the latest [CTC Traders API Test Pack](https://www.gov.uk/government/publications/new-computerised-transit-system-technical-specifications) to test your software is compatible with our API.

You must do some sample scenarios and test data for both Great Britain and Northern Ireland.

You can find cURL commands and Postman collections on our [GitHub page](https://github.com/hmrc/common-transit-convention-traders-postman).

These will give you examples of how to connect to our API.

You can use the following cURL commands to simulate:

 - your software application’s actions and messages
 - the actions and messages that would come back from the NCTS
 
If you want to use the XML directly, you can extract these from the files found in the Github repository either by using:

 - Postman for the [Postman collection](https://github.com/hmrc/common-transit-convention-traders-postman/tree/master/Collections)
 - Text editor for [all files](https://github.com/hmrc/common-transit-convention-traders-postman/)

##How to test for push pull notifications

**Note**: if your endpoint is hosted by Amazon Web Services (AWS) then you must either use [edge-optimised custom domain names](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-edge-optimized-custom-domain-name.html) or [regional custom domain names](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-regional-api-custom-domain-create.html).

When testing your software, you can be sent automatic notifications using the [Push Pull Notifications API](/api-documentation/docs/api/service/push-pull-notifications-api/1.0).

This is where notifications from NCTS are sent  to your software in near real time.

To get these automatic messages, you must:

 - subscribe to the Push Pull Notifications service
 - subscribe to the CTC Traders API in the sandbox environment
 - configure the notification URL in the subscription configuration section of Developer Hub:
 
 ![NotificationWebAddress](/figures/notification_url_subscription.png)

To subscribe to the Push Pull Notifications service, go to Developer Hub.

 ![Subscription](/figures/Push_Pull_Notification_switch.png)
 
###How it works

This diagram shows an example of the process where your service needs to return a 200 HTTP status as part of the automated notification process.

![Push Message From NCTS](/figures/Push_NCTS_Diagram.png)

###Examples of Push Notification XML

The following example push notification shows how to embed the XML body within JSON for messages that are small enough to include in the notification:

    {
       "notificationId":"5049d7bf-1cae-4b7a-8dd0-fe225e0ce9f5",
       "boxId":"59cfdd13-7876-4646-a292-a271eaa8c350",
       "messageContentType":"application/json",
       "message":"{\"messageUri\":\"/customs/transits/movements/arrivals/4/messages/3\",\"requestId\":\"/customs/transits/movements/arrivals/4\",\"customerId\":\"9999999902\",\"arrivalId\":\"4\",\"messageId\":3,\"received\":\"2022-03-03T15:48:00\",\"messageType\":\"IE025\",\"messageBody\":\"<CC025A>\\n          <SynIdeMES1>RVDp</SynIdeMES1>\\n          <SynVerNumMES2>2</SynVerNumMES2>\\n          <MesSenMES3>GXLpwsEurxXkLIObahe9</MesSenMES3>\\n          <MesRecMES6>4ABk3gQBHk</MesRecMES6>\\n          <DatOfPreMES9>20220303</DatOfPreMES9>\\n          <TimOfPreMES10>1548</TimOfPreMES10>\\n          <IntConRefMES11>GgL</IntConRefMES11>\\n          <MesIdeMES19>YE9zR</MesIdeMES19>\\n          <MesTypMES20>PDSy</MesTypMES20>\\n          <HEAHEA>\\n            <DocNumHEA5>nn4eU6HeptlnkYFeVuJR</DocNumHEA5>\\n            <GooRelDatHEA176>15150103</GooRelDatHEA176>\\n          </HEAHEA>\\n          <TRADESTRD/>\\n          <CUSOFFPREOFFRES>\\n            <RefNumRES1>y9Y7TehM</RefNumRES1>\\n          </CUSOFFPREOFFRES>\\n        </CC025A>\"}",
       "status":"PENDING",
       "createdDateTime":"2022-03-03T15:48:50.171+0000"
    }

The following example push notification shows how the XML is not embedded in the body within JSON for messages where the XML is too large to include in the payload. Instead, the XML must be downloaded from the messageUri provided:

    {
       "notificationId":"f1ac5fc8-a8b5-4c8d-8f8b-1bcc7ff50057",
       "boxId":"59cfdd13-7876-4646-a292-a271eaa8c350",
       "messageContentType":"application/json",
       "message":"{\"messageUri\":\"/customs/transits/movements/arrivals/4/messages/4\",\"requestId\":\"/customs/transits/movements/arrivals/4\",\"customerId\":\"9999999902\",\"arrivalId\":\"4\",\"messageId\":4,\"received\":\"2022-03-03T15:58:00\",\"messageType\":\"IE043\"}",
       "status":"PENDING",
       "createdDateTime":"2022-03-03T15:58:28.485+0000"
    }
    
## Message size considerations

Performance tests indicate that messages up to 4.9MB in size are likely to be delivered successfully and receive the expected asynchronous responses from NCTS. However, if you are expecting an IE016 message in response, depending on the number of errors encountered within a message, it might take up to 5 minutes for the message to arrive.

**Note**: For large messages, consider making use of the [push-pull notifications API](/api-documentation/docs/api/service/push-pull-notifications-api/1.0) to have automatic notifications sent from NCTS in near real time. (See [How to test for push pull notifications](#how-to-test-for-push-pull-notifications).)

## Example IE044 message scenarios

This section provides examples of XML to illustrate particular IE044 message scenarios.

### Missing item

This example file illustrates the situation when a good item is expected but not received: <a href="figures/IE44_Missing goods item.txt" download>IE44_Missing goods item.txt</a>

### Differences and new data: differences at header level

This example file illustrates the situation when a good item has some differences at the header level: <a href="figures/IE44_Difference at Header level.txt" download>IE44_Difference at Header level.txt</a>

### New item

This example file illustrates the situation when a new item is reported: <a href="figures/IE44_New Item Found In GoodItem.txt" download>IE44_New Item Found In GoodItem.txt</a>

## Ensure Guarantee Service error list

**Note:** These errors are seen only in the event of 400 Bad Request responses. 

For each error produced by the Ensure Guarantee Service, the following table lists the expected cause and the recommended action. 

<table>
    <tr>
        <th>Error message</th>
        <th>Expected cause</th>
        <th>Suggested action</th>
    </tr>
    <tr>
        <td>Amount cannot be equal to or less than 0</td>
        <td>Special Mention (SPEMENMT2) matched with guarantee reference has an amount equal to or less than 0</td>
        <td>Ensure that all Special Mention fields (SPEMENMT2) regarding guarantees have an amount that is greater than 0</td>
    </tr>
     <tr>
        <td>Departure Empty</td>
        <td>Office of Departure field (“CUSOFFDEPEPT" \ "RefNumEPT1”) has no value</td>
        <td>Ensure that the CUSOFFDEPEPT \ RefNumEPT1 field has a value</td>
    </tr>
    <tr>
        <td>Destination Empty</td>
        <td>Office of Destination field (”CUSOFFDESEST" \ "RefNumEST1”) has no value</td>
        <td>Ensure that the CUSOFFDESEST \ RefNumEST1 field has a value</td>
    </tr>
    <tr>
        <td>GuaRefNumGRNREF1 was empty</td>
        <td>One of the guarantees with a type of 0, 1, 2, 4 or 9 has no “GuaRefNumGRNREF1” field or field value</td>
        <td>Ensure that the guarantees of types 0, 1, 2, 4 or 9 have a correctly populated GuaRefNumGRNREF1 field</td>
    </tr>
    <tr>
        <td>GuaTypGUA1 was invalid</td>
        <td>One of the guarantees found has no guarantee type</td>
        <td>Ensure that the GuaTypGUA1 field on all guarantees is populated</td>
    </tr>
    <tr>
        <td>GuaTypGUA1 was not a valid type</td>
        <td>One of the guarantees found has a guarantee type that is not recognised (we support '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', and ‘B’)</td>
        <td>Ensure that the GuaTypGUA1 field on all guarantees uses a supported code (supported codes are: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A or B)</td>
    </tr>
    <tr>
        <td>GuaTypGUA1 was too long</td>
        <td>One of the guarantees found has a guarantee type with more than one digit/character</td>
        <td>Ensure that the GuaTypGUA1 field on all guarantees has only one digit or character (supported codes are: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A or B)</td>
    </tr>
    <tr>
        <td>Inappropriate Departure Office</td>
        <td>A value in the Office of Departure field (“CUSOFFDEPEPT \ RefNumEPT1”) has been parsed that starts with neither an "XI" nor a "GB" and therefore is not supported by the CTC service</td>
        <td>Ensure that the CUSOFFDEPEPT \ RefNumEPT1 field has the correct office code and is from GB or NI (it should start with "GB" or "XI" as appropriate)</td>
    </tr>
    <tr>
        <td>Invalid Item Number</td>
        <td>A goods item (GOOITEGDS) has an item number (IteNumGDS7) that is not a valid integer</td>
        <td>Ensure that all Goods Items (GOOITEGDS) have Item Number (IteNumGDS7) fields populated with integers</td>
    </tr>
    <tr>
        <td>Missing Item Number</td>
        <td>A goods item (GOOITEGDS) is missing an item number (IteNumGDS7)</td>
        <td>Ensure that all Goods Items (GOOITEGDS) have an Item Number (IteNumGDS7) field populated</td>
    </tr>
    <tr>
        <td>OthGuaRefREF4 was empty</td>
        <td>One of the guarantees with a type of 3, 5, 6, 7, 8, A or B has no “OthGuaRefREF4” field or field value</td>
        <td>Ensure that the all guarantees of types 3, 5, 6, 7, 8, A or B have a correctly populated OthGuaRefREF4 field</td>
    </tr>
    <tr>
        <td>Parsed Amount value without currency</td>
        <td>Special Mention (SPEMENMT2) matched with guarantee reference has an amount value but no currency</td>
        <td>Ensure that all Special Mention fields (SPEMENMT2) regarding guarantees are correctly populated with an amount value and currency</td>
    </tr>
    <tr>
        <td>Transformation impossible with provided xml</td>
        <td>An unexpected error has happened when trying to apply the default guarantee requirement for this declaration</td>
        <td>Ensure that the guarantee information has been applied and resubmit. If the problem persists, forward the XML to the Software Developer Support Team for investigation by the development team</td>
    </tr>
</table>

**Note:** For Software Developer Support Team contact details, see [Get support](#get-support).
 
## Submit your results

Once you are satisfied with your tests and are confident that your software is fully compatible with our API:
 - log all your evidence and results by filling in all the sections of this [checklist form](/guides/ctc-traders-phase4-testing-guide/figures/CTC_Traders_API_Application_for_Productions_Credentials.docx) (this is a Word document which will download). You must also answer all the questions at the end of the checklist.
 - when ready, email your completed form to [SDSTeam@hmrc.gov.uk](mailto:SDSTeam@hmrc.gov.uk)
 - we’ll check your test evidence using the information you give on this form.
 - when we are satisfied that you have done enough testing, you will be granted access to the live API system.

## Get support

###General support for development and testing

Email our Software Developer Support Team at [SDSTeam@hmrc.gov.uk](mailto:SDSTeam@hmrc.gov.uk) if you have any questions or difficulties or need additional clarification on this testing process. 

###Support for Trader Test

While using the Trader Test service, you may need to request a manual intervention from Trader Test support. 

You can find more information about this in the [NCTS Access and Channels document](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/940784/NCTS_Trader_Test_Access_Channels_and_Support_v1.1.pdf), but when you need to generate a manual response, [email the Trader Test support team with your request](mailto:NCTS.tradertestteam@hmrc.gov.uk)). 

Please note - it can take 24 hours to get a response.

###Support for live user issues

Once your software is live, your point of contact is the NCTS helpdesk - [ncts.helpdesk@hmrc.gov.uk](mailto:ncts.helpdesk@hmrc.gov.uk) or **0300 322 7095**.

It can help with all user issues such as access and enrolment.

###Finding a bug

If you have found a bug in our code, you can get in touch with our developers directly on our [Github issues page](https://github.com/hmrc/common-transit-convention-traders/issues).

##Useful CTC page links

[CTC Traders API Roadmap](/roadmaps/common-transit-convention-traders-roadmap/)

[CTC Traders API Documentation](/api-documentation/docs/api/service/common-transit-convention-traders/1.0)

[CTC Traders API Service Guide](/guides/ctc-traders-phase4-service-guide/)
