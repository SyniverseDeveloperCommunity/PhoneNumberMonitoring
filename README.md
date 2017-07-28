# PhoneNumberMonitoring
Example code to subscribe & unsubscribe for Phone Number Monitoring from Syniverse.

By downloading the attached python files, and simply adding your access token and delivery configuration Id you can quickly set up monitoring for the phone numbers in the file phonenumbers.txt.

__ Dependencies

You will first need to have an account (create at https://developer.syniverse.com ).

Secondly you will need to have subscribed to the Service Offerings for Developer Community Gateway, Media Service, Batch Automation and Event Manager. 

Do this by going to the Service Offerings tab (https://developer.syniverse.com/index.html#!/service-offerings) , clicking on each service in turn, click on Subscriptions, Click on Subscribe and then select an account from the drop down.

Thirdly you will need to create an application (or update an existing Application )

Do this by going to the Applications tab (https://developer.syniverse.com/index.html#!/applications), click on New application and follow the instructions. You also need to add (or update) the Account & APIs section to turn on the SDC Gateway Services, Media Services, Batch Automation and Event Manager. Lastly re-generate the Auth Keys, and then copy your Access token for use in the Code.

Fourth you will need to create a delivery configuration for the notifications (only used for Monitor, but not needed to unsubscribe)

Do this by going to the Event Manager tab and then to Delivery Configurations (https://developer.syniverse.com/index.html#!/ess/delivery-configurations), click on new Delivery Configuration, and then populate the Name and Address fields (the address is the URL where the notification should be sent to. The other properties can be left the same.
If you are just trying out the service you may want to try https://requestb.in/ to create an endpoint to receive the notifications.

Once you have created the delivery configuration then you can read the delivery configuration from the table of delivery configurations on the delivery configurations page. The Id is typically a 3 digit number in the delivery configuration id field.

__ Sample output when running the Monitor script is

python.exe PycharmProjects/BatchMonitor/BatchMonitor-Example.py
### Starting Engines ###

Creating file in Media Storage
create file response status code: 201
mss create response body: {"file_id":"a3b7ac34-9d86-4656-8376-cc480edc9887","company-id":"589","file_status":"CREATED","file_uri":"https://api.syniverse.com/mediastorage/v1/files/a3b7ac34-9d86-4656-8376-cc480edc9887/content","file_version":1,"file_checksum":0,"file_size":0,"file_fullsize":2000000,"creation_time":"2017-07-28T09:01:45.571 +0000","modified_time":"2017-07-28T09:01:45.571 +0000","file_retention_time":30,"expire_time":"2017-08-27T09:01:45.571 +0000"}

Uploading input file to Media Storage
upload response status code: 201
upload response: 

Scheduling the Number Monitoring batch job in Batch Automation
Scheduling response status code: 201
Scheduling response: {"schedule":{"id":"d4d5226b-e98c-4e82-9fa4-15b06afbaec8","jobId":"NIS-Monitor-v2","name":"NISMonitor","inputFileId":"a3b7ac34-9d86-4656-8376-cc480edc9887","fileRetentionDays":30,"scheduleRetentionDays":30,"outputFileNamingExpression":"DS1-NIS-Monitor-output.txt","outputFileFolder":"/opt/apps/aba/output","outputFileTag":null,"jobRuntimeContext":{"subscribedestinationid":"676","subscribeevents":"all"}}}

Waiting 20s for job to complete

Retrieving batch job execution details
Get batch job details status code: 200
Get batch job details response: {"executions":[{"id":"c75317e5-af74-43e5-be22-784c2ade6e7d","scheduleDetail":{"id":"d4d5226b-e98c-4e82-9fa4-15b06afbaec8","jobId":"NIS-Monitor-v2","name":"NISMonitor","inputFileId":"a3b7ac34-9d86-4656-8376-cc480edc9887","fileRetentionDays":30,"scheduleRetentionDays":30,"outputFileNamingExpression":"DS1-NIS-Monitor-output.txt","outputFileFolder":"/opt/apps/aba/output","outputFileTag":null,"jobRuntimeContext":{"subscribedestinationid":"676","subscribeevents":"all"}},"status":"COMPLETE","statusReason":"Final Status","startTimestamp":1501232512949,"statusUpdateTimestamp":1501232518795,"outputFileId":"dedfb622-1f2f-415e-af69-10ba9f7bfd91","errorDetailFileId":"EMPTY_FILE","retryFileId":"EMPTY_FILE","recordSuccessCount":3,"recordRetryCount":0,"recordErrorCount":0,"outputFileURI":"https://api.syniverse.com/mediastorage/v1/files/dedfb622-1f2f-415e-af69-10ba9f7bfd91/content","errorDetailFileURI":"EMPTY_FILE","retryFileURI":"EMPTY_FILE"}]}

Downloading the Output file
Download output status code: 200
Download output response: 
+18132633923,subscribe,"deactivation_event,porting_event,truedisconnect_event",2017-07-28T09:01:56.321Z[UTC]
+18135041457,subscribe,"deactivation_event,porting_event,truedisconnect_event",2017-07-28T09:01:56.316Z[UTC]
+18139551760,subscribe,"deactivation_event,porting_event,truedisconnect_event",2017-07-28T09:01:56.322Z[UTC]

Process finished with exit code 0

__ Sample output when running the Unsubscribe script is 

python.exe PycharmProjects/BatchMonitor/BatchMonitorUnsubscribe-Example.py
### Starting Engines ###

Creating file in Media Storage
create file response status code: 201
mss create response body: {"file_id":"08fb7e20-3dae-47ea-936f-469a17b9d6ac","company-id":"589","file_status":"CREATED","file_uri":"https://api.syniverse.com/mediastorage/v1/files/08fb7e20-3dae-47ea-936f-469a17b9d6ac/content","file_version":1,"file_checksum":0,"file_size":0,"file_fullsize":2000000,"creation_time":"2017-07-28T09:04:44.063 +0000","modified_time":"2017-07-28T09:04:44.063 +0000","file_retention_time":30,"expire_time":"2017-08-27T09:04:44.063 +0000"}

Uploading input file to Media Storage
upload response status code: 201
upload response: 

Scheduling the Number Monitoring Unsubscribe batch job in Batch Automation
Scheduling response status code: 201
Scheduling response: {"schedule":{"id":"cf5850e3-147a-4e7c-b32b-914b264fb501","jobId":"NIS-Unsubscribe-v2","name":"NISUnsubscribe","inputFileId":"08fb7e20-3dae-47ea-936f-469a17b9d6ac","fileRetentionDays":30,"scheduleRetentionDays":30,"outputFileNamingExpression":"DS1-NIS-Unsubscribe-output.txt","outputFileFolder":"/opt/apps/aba/output","outputFileTag":null,"jobRuntimeContext":{}}}

Waiting 20s for job to complete

Retrieving batch job execution details
Get batch job details status code: 200
Get batch job details response: {"executions":[{"id":"74e8e09f-224b-482e-a7f4-8189dedb939e","scheduleDetail":{"id":"cf5850e3-147a-4e7c-b32b-914b264fb501","jobId":"NIS-Unsubscribe-v2","name":"NISUnsubscribe","inputFileId":"08fb7e20-3dae-47ea-936f-469a17b9d6ac","fileRetentionDays":30,"scheduleRetentionDays":30,"outputFileNamingExpression":"DS1-NIS-Unsubscribe-output.txt","outputFileFolder":"/opt/apps/aba/output","outputFileTag":null,"jobRuntimeContext":{}},"status":"COMPLETE","statusReason":"Final Status","startTimestamp":1501232693409,"statusUpdateTimestamp":1501232698016,"outputFileId":"ba0f8c70-ab93-44eb-bd7a-2c0b2e14b0f7","errorDetailFileId":"EMPTY_FILE","retryFileId":"EMPTY_FILE","recordSuccessCount":3,"recordRetryCount":0,"recordErrorCount":0,"outputFileURI":"https://api.syniverse.com/mediastorage/v1/files/ba0f8c70-ab93-44eb-bd7a-2c0b2e14b0f7/content","errorDetailFileURI":"EMPTY_FILE","retryFileURI":"EMPTY_FILE"}]}

Downloading the Output file
Download output status code: 200
Download output response: 
+18132633923,unsubscribe,ALL,2017-07-28T09:04:55.564Z[UTC]
+18135041457,unsubscribe,ALL,2017-07-28T09:04:55.559Z[UTC]
+18139551760,unsubscribe,ALL,2017-07-28T09:04:55.564Z[UTC]

Process finished with exit code 0
