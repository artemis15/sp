# Lab 4: Add Widgets
## Introduction
In this lab you will create a new page, add it to your Menu and load it up with some OOB widgets.

## Step 1: Create a new Page
***Go to Service Portal > Service Portal Configuration (sp_config)***
- Click on Page Designer
- Click the “Add a New Page” link
	- Name = Dashboard 
	- ID = dashboard

## Step 2: Build your page layout
With Page Designer open to your new page:
- Add 1 additional Container so there are 2 total containers
  - Container 1: apply a 2-column layout (6 by 6)<br/>
  - Container 2: apply a 1-column layout (12)

## Step 3: Add your Page to your Menu
***Go to Service Portal > Portal > Your Portal***
- Click through to the Main Menu (SP Header Menu)
- Add a New Menu Item:<br/>
  - Label = Dashboard<br/>
  - Order = 500<br/>
  - Type = Page<br/>
  - Page = dashboard<br/>

## Step 4: Add OOB Widgets to your Columns

### Container 1
 ***Left Column:***
- Place a “Data Table from Instance Definition” widget
- Open Widget Options:
  - Title = Recent Incidents
  - Table = incident
  - Fields = Number, Short Description, Caller
  <br/>
 ***Right Column:***
- Place a “Simple List” widget
- Open Widget Options:
  - Table = hr_task
  - Display field = Short Description
  - Bootstrap Color = pick one

### Container 2
- Place a “Form” widget

## Step 5: Preview and Update

Preview your Portal (not from the Designer):
-	Click the “Dashboard” menu item in your Menu
-	You should see your 2 widgets in Container 1 loaded with correct values
-	Add this to the end of your URL: `&table=incident&sys_id=-1`
-	You should then see the Form widget exposed with the standard form loaded
-	Add this to the end of your URL: `&view=ess`
-	You should now see the form widget loaded with the standard form, but within the ESS View (the final URL should read something like: `?id=dashboard&table=incident&sys_id=-1&view=ess`



