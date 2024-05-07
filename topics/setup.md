# Manual Extended Time Sheets Dime.Scheduler

## Setup

Because the Dime.Scheduler platform is a cloud service, data must be sent from Business Central to Dime.Scheduler to be able to plan projects. When an appointment is created in Dime.Scheduler, the system will need a web service connection to Business Central to send the result.
The following steps set up a basic integration for jobs with Dime.Scheduler. 
For more detailed information, please visit https://docs.dimescheduler.com.

### Business Central

**FastTrack Wizard**

1.	Choose the Search icon, Enter Dime.Scheduler FastTrack Wizard and choose the related link.
2.	On the first page of the wizard, supply a unique identifier for your environment/company combination as Source App. The fields Scheduler Url, Scheduler User and Scheduler Password must be filled with the information supplied by Dime.Scheduler.

![FastTrack Connection](../images/setup/fasttrack-connection.png)

3.	When clicking Next, the information is checked. When a connection could be established based on the entered information, the following dialog is shown:

![FastTrack Connection OK](../images/setup/fasttrack-connectionok.png)

4.	In the following steps, at least the following information must be entered:

![FastTrack Resources](../images/setup/fasttrack-resources.png)

![FastTrack Jobs](../images/setup/fasttrack-jobs.png)

5.	After finishing the wizard, the system will ask to synchronize to Dime.Scheduler. Answer this question with Yes, which synchronizes at least the resources from Business Central to Dime.Scheduler.

![FastTrack Synchronize](../images/setup/fasttrack-synchronize.png)

**Filter Groups**

1.	Choose the Search icon, Enter Dime.Scheduler Filter Groups and choose the related link.
2.	Create a record for Type ‘Category’ with as Group Name ‘Jobs’. This category will define the color of the appointment for the job in Dime.Scheduler.

![FilterGroup Jobs](../images/setup/filtergroup-jobs.png)

3.	Go to the Filter Group Sources

![FilterGroup Sources](../images/setup/filtergroup-sources.png)

4.	Create the following record. This will be used to determine which value will be opened from the Project Card/Project List later.

![FilterGroup Source](../images/setup/filtergroup-source.png)

**Scheduled Sync**

1.	Choose the Search icon, Enter Job Queue Entries and choose the related link.
2.	Create a new entry for codeunit 2087634 (Dime DS Scheduled Synch.). This entry must be scheduled periodically to ensure that all setup data regarding Dime.Scheduler from Business Central is synchronized.

![Scheduled Sync](../images/setup/scheduledsync.png)

### Dime.Scheduler

**Connection to Business Central**

Dime Scheduler communicates with Business Central through SOAP web services. For this purpose, two records are automatically added to the Web Services table in Business Central when the Dime.Scheduler app is installed. To be able to access the web service from Dime.Scheduler, a registered application must be created in Microsoft Entra. More information on how to do that can be found here: https://docs.dimescheduler.com/backoffice/bc/install/authentication 
Please note that when setting up the registered application in Business Central, at least also permission sets for License Permission User, Extended Time Sheets and Extended Time Sheets (Dime Scheduler) must be included. In this demo SUPER (DATA) is used, but a more fine-grained permission set is advised.
When the published application is granted permission in Business Central, the Business Central connector can be added to Dime.Scheduler:

![Dime.Scheduler Connectors](../images/setup/dime-connectors.png)

Enter a Name and a Description for the connector. Make sure that the field Source Application is filled with exactly the value that is also used during the setup in Business Central. Send appointment must be enabled.

BackOffice system must be set to Dynamics Business Central (SaaS) and the Web Service URL is the SOAP URL of the web services for Appointments.

![Dime.Scheduler BC Connector](../images/setup/dime-bcconnector.png)

The field Login must be filled with the Microsoft Entra Tenant ID.
In the password field, take the following string and replace **CLIENTID** and **CLIENTSECRET** with the corresponding values from the app registration: **client_id=CLIENTID&client_secret=CLIENTSECRET**

**Add localization for Enabled for Time Sheets**

In Dime.Scheduler go to Localization:

![Dime.Scheduler Localization](../images/setup/dime-localization.png)

Select FreeBit2 for Source Table ‘Task’ and make sure that the following translations are set
- English (US) / en-US: Enabled for Time Sheets
- Dutch / nl: Ingeschakeld voor urenstaten

![Dime.Scheduler Enabled for Time Sheets](../images/setup/dime-enabledfortimesheets.png)

**Filter open task**

To make sure that open tasks part of the scheduler only contain project tasks that are enabled for Time Sheets, we have to add the field Enabled for Time Sheets. This can be done by clicking the small triangle next to an existing field name, go to columns and check the field Enabled for Time Sheets.

![Dime.Scheduler Add Field](../images/setup/dime-addfield.png)

When the field is added. Set a filter on the field. Again, this can be done by clicking on the small triangle and go to Filters:

![Dime.Scheduler Filter](../images/setup/dime-filter.png)

When this is done, the field Enabled for Time Sheets may be removed again from the open tasks part. 

> [!IMPORTANT]
Make sure that the modifications to the part are saved in a profile.

[:arrow_left:](../README.md) [Back](../README.md)