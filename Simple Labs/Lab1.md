# Lab 1: Create a New Portal 
## Introduction
In this lab you will create a custom portal with a custom page and populated with standard widgets. <br/>
You will also get more familiar with Page Designer.

## Step 1: Create a new Portal
### Go to Service Portal > Portals
- Create a new record.
- Assign the “Stock” theme to your portal.
- Assign the “SP Header Menu” as your Main menu.

## Step 2: Create a new Page
### Go to Service Portal > Service Portal Configuration (sp_config)
- Click on Page Designer
- Click the “Add New Page” link

## Step 3: Assign New Page to Portal Home Page
### Go to Service Portal > Portals > your new portal
- For Home Page, assign the page you just created in Step 2.

## Step 4: Design Your Page
### Go to Service Portal > Service Portal Configuration (sp_config), filter for your new home page.

On your home page, create 3 containers:

![move to header](/assets/designer.jpg)<br/>
***For Container 1:*** 
- Set to 2 columns, 8 by 4<br/>
  -	`HINT:` Start with any 2 column options, then change the Column property of each to get to 8 by 4.
- Apply a background image<br/>
  -	In the Container properties, upload a new image (http://bit.ly/SP_header - download the Large version)<br/>
  -	Set background image to Cover (In the Container Properties – Background style)

***For Container 2:***
- Set to 4 columns
- In Container properties, apply a background of `#DDDDDD` to this container.

***For Container 3:***
- Set to 2 columns
- In Container properties, apply a background of `#343d47` to this container

`NOTE`: At this point if you preview your page you won’t see anything as you have just put your containers in place, there is no content to actually expose the backgrounds and image you placed. Once you get through Step 5 you’ll see the page come to life.

## Step 5: Include Widgets
Apply the following widgets to your containers:

***For Container 1:***
- Left column:<br/>
   -	Place an “HTML” widget with a value of “Welcome” in the HTML. 
   -	Select-all and use the Paragraph dropdown (in the WYSIWYG editor) to select the “Heading 2” value. 
   -  `Note`: This turns the “Welcome” text into an H2 value (CSS).
- Right column: Place a “Simple List” widget with options of:<br/>
   -	Table: kb_knowledge
   -	Display Field: Short Description

***For Container 2:***
- Put “Icon Link” widgets in each column.
- Use a mix of Titles, Icons (Glyph), Bootstrap Colors and Templates for each widget

***For Container 3:***
- Left column: Place an “HTML” widget with the text of “© 2017 inMorphis” in the Body
- Right column: Place a “My Requests” widget

 
The result should look something like this:
![move to header](/assets/final1.png)<br/>

`NOTE`: When viewing your page, it’s best to view outside of the designer. Use the quick link to open the page in your browser. The Designer doesn’t render your specific column and page CSS properties.
 

# Bonus Challenge: 
Have one of your containers disappear on mobile. 

## Bonus Challenge Solution:
1.	Navigate to http://getbootstrap.com/css
2.	Find the “Available classes” section on the page (on the page, click Command+F and search for the words “Available classes”)
3.	You want the “hidden-xs” value
4.	Navigate back to your container and place the “hidden-xs” value into the widget option of Parent Class. <br/>
`NOTE:` You do not need to include the period of the class when using class names within the Page Designer. So you would use “hidden-xs” versus “.hidden-xs”.
5.	Test using the Preview function on the page designer.

The idea is that you an include any of the available classes from Bootstrap within your containers / rows / columns / widgets to tap into the out-of-box functionality of Bootstrap within Service Portal. 

