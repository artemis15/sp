# Lab 2: Search Groups and Messages
## Introduction
In this lab you will add a new table to your Search Results and create a new Message to be used within a widget.


## Step 1: Add Additional Knowledge Base to Search Groups

 Go to Service Portal > Portals > Your Portal

 Under Search Groups on the Portal record, Add a new value:<br/>
 -	Table = kb_knowledge
 -	Optional Label = HR Knowledge Base
 -	Page = kb_view2
 ***Conditions:***
  - Knowledge Base = Human Resources General Knowledge
  - Workflow = Published

Test on your live portal:<br/>
-	Try the type ahead search with “Email”. You should see some addition KB article values included.<br/>
-	Try the search results page to see the Label as a filter.


## Step 2: Create a New Message for English

Go to System UI > Messages

Create a new Message:<br/>
•	Key = portal_welcome_home<br/>
•	Language = English<br/>
•	Message = Welcome<br/>

Go to Page Designer > Your Home Page <br/>
•	Edit the HTML widget in Container 1<br/>
•	Change the “Welcome” text value to “${portal_welcome_home}” (no quotes).<br/> <br/>
HINT: Paste this value from the code view (< >).

Preview the live version of your page to see your changes (not through the Designer).


## Step 3: Create a New Message for Spanish

Activate the Internationalization Plugin to turn on Spanish:<br/>
•	Go to System Definition > Plugins<br/>
•	Filter for Name = I18N: Internationalization<br/>
•	Click Activate/Upgrade, then Activate in the pop-up window<br/>
•	Once complete, select “View Plugins List” to get back to System Definition > Plugins<br/>
•	Filter for Name = I18N: Spanish Translations<br/>
•	Click Activate/Upgrade, then Activate in the pop-up window (will take a few minutes to finish)<br/>

Create an addition Message:<br/>
•	Go to System UI > Messages<br/>
•	Create a new Message:
  o	Key = portal_welcome_home<br/>
  o	Language = Spanish<br/>
  o	Message = Bienvenido<br/>

Go preview your portal to see the English text.<br/> 
Then go into the Platform View and update your user settings to Spanish (use the Settings gear in the platform view to switch):

NOTE: You might need to refresh your platform view after activating the Internationalization plugin.
Reload the page to see the Spanish text instead. 

HINT: make sure to switch BACK to English!

## Bonus Challenge: 
Add a Module to your Service Portal application that is just a filtered list of your Portal Messages.

## Bonus Challenge Solution: 
Go to System Definition > Modules
Create a New Module:<br/>
•	Title = Portal Messages<br/>
•	Application menu = Service Portal<br/>
•	Order = 6000<br/>
•	Link Type:<br/>
  o	Link type = List of Records<br/>
  o	Table = Message [sys_ui_messages]<br/>
  o	Filter = Key, starts with, “portal_”<br/>
•	Submit

Check under Service Portal for the “Portal Messages” module as the last value. Click on the module to expose a list of your portal messages. 

