# Lab 1.1: Clone Stock Widget
### Go to Service Portal -> Service Portal Configuration 
- open the Widget Editor
- open the Stock widget
- Click on the menu and choose Clone “Stock”. 
- Give the new widget a name of My Stock 
- check the Create test page 
- Submit <br/><br/>
![move to header](/assets/clone.png)<br/>

`Hint:` You can save the widget by pressing Command + S.

- Open the test page in a new tab without a portal associated. <br/>
***Remember the `$sp.do?id=<page_id>` trick?***

### Lab Validation:
***Your new test page with your cloned widget will look something like this.***  <br/>
Test it out by adding a known stock code (e.g. NOW). <br/><br/>
![move to header](/assets/stock.png)<br/>

# Lab 1.2: Adding Options to the Widget

- Back on the Widget Editor
- click on the menu and select Edit option schema
- Create 3 new options:
  - `Label:` Title		  `Name:` title 		`Type:` string <br/>
  - `Label:` Price     `CSS Name:` price_css	`Type:` string <br/>
  - `Label:` Image     `CSS Name:` image_css	`Type:` string <br/><br/><br/>
  ![move to header](/assets/options.png)<br/>

- Click Save and then reload the page.

***Let’s now add those options to the HTML template:***

- Add a h2 tag to the top of the HTML to display the title:
```CSS
<h2>{{::options.title}}</h2>
```
- Locate the span element where the price is displayed 
- add a new style attribute with the Price CSS option:
```CSS
<span style={{::options.price_css}}>{{c.data.price | currency:"$"}}</span>
```
- Locate the img element where the stock image is displayed
- add a new style with the Image CSS option:
```CSS
<img style={{::options.image_css}} ng-src="http://chart.finance.yahoo.com/z?s={{c.data.symbol}}&t=1d&z=l"/>
```
- Click Save.

***Open or reload the test page again***
- Right-click + CTRL on the widget instance and select Instance Options: <br/><br/><br/>
![move to header](/assets/symbol.png)<br/><br/><br/>

- Enter some text for the Title and then some CSS style to Price CSS and Image CSS option and Click Save.
  - Title:	 	Realtime Stock
  - Price CSS:	color: green;  font-size: 30px
  - Image CSS:	border: 5px solid green; border-radius: 5px; padding: 5px; <br/><br/>
![move to header](/assets/realtime.png)<br/> <br/>
- reload the page <br/>
***You can immediately see the title you added above.***

### Lab Validation:
Open your test page, and again test it out.<br/> 
This time, open your test page with an actual portal associated (e.g. sp). <br/>
***The page should look something like this:***  <br/><br/>
![move to header](/assets/realtimestock.png) <br/>

# Lab 1.3: Adding Widget specific CSS-SCSS

Let’s now add some widget specific CSS-SCSS styling!

- Back in the Widget Editor.
- create a new class called named myTitleClass and specify some styles of your liking.
```CSS
.myTitleClass {
  font-size: 25px;
  color: $sp-tagline-color;
  font-weight: bold;
  text-decoration: underline;    
}
```
- Add the new class to the h2 element tag:
```CSS
<h2 class="myTitleClass">{{::options.title}}</h2>
```
- Click Save.


### Lab Validation:
- Open your test page within a portal (e.g. sp). 
- The widget should look something like this with your new class applied: <br/><br/>
![move to header](/assets/servicenow.png) <br/>


# Lab 1.4: Challenge – Working with Unspecified Options

There may be a situation where the widget instance does not have 1 or more options set.<br/>
For this, it’s best to add an additional check to ensure the option has a value.

- Modify the instance options and clear the text for the Title. 
Notice how even though the title is not set, the h2 tag is still rendered and occupies a visible “empty” space on the page.<br/><br/> 
`Hint:` You can use your browser’s Inspect functionality for this.<br/><br/><br/>
![move to header](/assets/serivenow1.4.jpg) <br/>
***So how do we check if the option is set or not?***
Take a look at how the span element that contains the localized text ${Requesting stock price}. <br/>
This element is using a special AngularJS directive called ng-if. <br/>
Once you’re done, the page should look something like this with `NO `visible empty space.<br/><br/><br/>
![move to header](/assets/servicenow1.4.1.png) <br/>

# Lab 1.5: Challenge – Applying Dynamic Classes

See if you can fly solo and modify your widget so that the price is 
displayed in red if the price is 60 or below or green for anything higher.<br/><br/>
`Hints:`
  - You will need to work with another AngularJS directive called ng-class
  - You will need to specify new classes in the CSS-SCSS section of the widget
  - You will need to remove the inline style for “color” of the price option

***Once you’re done, this is how it will/should look like:*** <br/><br/><br/> 
![move to header](/assets/realtimesymbol1.png) <br/><br/><br/>
![move to header](/assets/realtimesymbol2.png) <br/><br/><br/>

###  …And with that, you’ve successfully completed Lab 1 

