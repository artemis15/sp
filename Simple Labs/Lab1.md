# Lab 1: Create a New Portal 
## Introduction
In this lab you will create a custom portal with a custom page and populated with standard widgets. You will also get more familiar with Page Designer.

## Step 1: Create a new Portal
Go to Service Portal > Portals
•	Create a new record.<br/>
•	Assign the “Stock” theme to your portal.<br/>
•	Assign the “SP Header Menu” as your Main menu.<br/>

## Step 2: Create a new Page
Go to Service Portal > Service Portal Configuration (sp_config)
•	Click on Page Designer<br/>
•	Click the “Add New Page” link<br/>

## Step 3: Assign New Page to Portal Home Page
Go to Service Portal > Portals > your new portal<br/>
•	For Home Page, assign the page you just created in Step 2.<br/>

## Step 4: Design Your Page
Go to Service Portal > Service Portal Configuration (sp_config), filter for your new home page.

On your home page, create 3 containers:

![move to header](/assets/designer.jpg)
### •	For Container 1: 
o	Set to 2 columns, 8 by 4
	HINT: Start with any 2 column options, then change the Column property of each to get to 8 by 4.
o	Apply a background image
	In the Container properties, upload a new image (http://bit.ly/SP_header - download the Large version)
	Set background image to Cover (In the Container Properties – Background style)
### •	For Container 2:
o	Set to 4 columns
o	In Container properties, apply a background of #DDDDDD to this container.
### •	For Container 3:
o	Set to 2 columns
o	In Container properties, apply a background of #343d47 to this container

NOTE: At this point if you preview your page you won’t see anything as you have just put your containers in place, there is no content to actually expose the backgrounds and image you placed. Once you get through Step 5 you’ll see the page come to life.

## Step 5: Include Widgets
Apply the following widgets to your containers:
### •	For Container 1:
o	Left column:
	Place an “HTML” widget with a value of “Welcome” in the HTML. 
	Select-all and use the Paragraph dropdown (in the WYSIWYG editor) to select the “Heading 2” value. Note: This turns the “Welcome” text into an H2 value (CSS).
o	Right column: Place a “Simple List” widget with options of:
	Table: kb_knowledge
	Display Field: Short Description
### •	For Container 2:
o	Put “Icon Link” widgets in each column.
o	Use a mix of Titles, Icons (Glyph), Bootstrap Colors and Templates for each widget
•	For Container 3:
o	Left column: Place an “HTML” widget with the text of 
“© 2017 inMorphis” in the Body
o	Right column: Place a “My Requests” widget

 
The result should look something like this:
