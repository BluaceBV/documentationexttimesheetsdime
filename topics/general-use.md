# Manual Extended Time Sheets Dime.Scheduler

## General use

### Create project in Business Central
Create a project in Business Central. Make sure that at least one project task is Enabled for Time Sheets:

![Project Card](../images/general-use/project-card.png)

With the action Category Filter Value, a color can be defined that is used for the appointments in the planning board in Dime.Scheduler:

![Category Filter Value](../images/general-use/project-categoryfiltervalue.png)

![Category Filter Values](../images/general-use/project-categoryfiltervalues.png)

### Send project to Dime.Scheduler
Use the action on the Project to send it to Dime.Scheduler:

![Send Project](../images/general-use/project-send.png)

This makes the job task with Enabled for Time Sheets available in the Open Tasks window:

![Open Task](../images/general-use/dime-opentask.png)

### Plan project in Dime.Scheduler
Drag and drop the task from the Open Task part to the planning board. An appointment block will be created with the length that is defined during the FastTrack Wizard. In this example 4 hours.

![Planning Board](../images/general-use/dime-planningboard.png)

### Get the results as Project Planning Lines in Business Central
In the background, Dime Scheduler created a budget Project Planning Line for the chosen resource. This record has the field Resource Planning enabled and contains the starting date/time and ending date/time.

![Project Planning Line](../images/general-use/project-planningline.png)

[:arrow_left:](../README.md) [Back](../README.md)