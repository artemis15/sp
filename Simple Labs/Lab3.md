# Lab 3: CSS Updates
## Introduction
In this lab you will use CSS to change elements on the page.<br/>
Reference the same containers from Lab 1 for this next section:<br/>
![move to header](/assets/welcome.png)<br/>
## Step 1: Update Font Color and Size of an Element on 1 Page

#### Go to Service Portal > Service Portal Configuration (sp_config) > Page Designer > Your Home Page

In Container 1, left column is the HTML widget. <br/>
Using CSS from Page Properties, your goal is to change the color and size of the “Welcome” text. 

***To accomplish this:***
- Remember the CSS element of the “Welcome” text was defined as “H2” in a Lab 1 so you need to adjust the "H2" value using CSS
- Also remember to view the page outside of the Designer (use the preview link)
- Open Page Properties and locate the Page Specific CSS field
- Here is a sample CSS value to change the H2 value:
```CSS
h2 {
   color: #FFD100; //or use whatever color you like here
   font-size: 24px;
}
```
- Try using any other declarations (http://www.w3schools.com/cssref)<br/><br/>
`NOTE:` This will only affect the H2 value of this page since the CSS was just applied to the Page Properties.
## Step 2: Change Link Colors for All Pages

Your goal for this step is to change ALL the link colors of your Portal to a new color.

***To accomplish this:***
- Go to Service Portal > CSS. 
- Create a new CSS file (i.e. custom.css)<br/>
Because you’re trying to change the link colors, that is the “A” element in CSS. <br/>
In your CSS page, put in something like this:
```CSS
a {
   color: #FFD100; //or use whatever color you like here, this is Yellow
}
```
### Go to Service Portal > Portals > Your Portal 
- Click through to the Stock theme<br/>
- Apply that CSS file to your Theme (click Edit and move over your file)
- Preview the live version of your page to see your changes (not through the Designer)

`NOTE:` sometimes you need to hard refresh so your CSS can reload if a previous declaration was changed.<br/> 
To do this, simply use Command+Shift+R.

## Step 3: Change Link Colors for Just 1 Column

In Container 3 is the My Requests widget from Lab 1. <br/>
You want to change the link colors in just THIS Column to Black (keeping the other Column links the same from Step 2).<br/> 
***To accomplish this:***
- Go to Service Portal > CSS > Your CSS File
- Add an addition element with a class of:
```CSS
.customlinks a {
   color:#000000; //this is the value for Black<br/>
}
```
- Next, head back to Page Designer > Your Home Page
- Edit the Column Properties for the right column in Container 3. 
- Add a class of “customlinks” and Save.
- Preview the live version of your page to see your changes (not through the Designer)

## Step 4: Change a Bootstrap Class Using CSS
One of the features of Service Portal is you can overwrite the OOB Bootstrap classes at the Portal, Page and Widget level. <br/>
For this Step you need to change one of the standard values `(.col-md-4)` to have a new value.

***To accomplish this:***
- Go to Service Portal > CSS > Your CSS File
- Assign a new value of:
```CSS
.col-md-4 {
   background-color:#000000;
}
```
`NOTE:` What this is doing is changing the OOB Bootstrap class of `.col-md-4`. Because you have changed this value at the CSS level 
(as opposed to the Page or Container level) which is linked to your Portal (via the Theme), every time you have a column that is set to 4 for MD it will have this same value.
- Preview the live version of your page to see your changes (not through the Designer) with a black background:
![move to header](/assets/welcome.png)<br/>
- To see it working on other columns, pick one of your other columns in one of your other containers and change the value of MD to 4     (from Column Properties). 
- Preview the live version of your page to see your changes (not through the Designer. 

### Bonus Challenge:
- At the Portal record, assign “kb_view2” as your “KB home page”.<br/> 
- Change the navbar color on just the Knowledge page.<br/>

### Bonus Challenge Solution:
- In page designer, navigate to kb_view2 and open.<br/>
- In the Page Properties, place this custom CSS code (to change to yellow, for instance):
```CSS
.navbar-inverse {
	background-color:#FFD100; //or use whatever color you like here
}
```
