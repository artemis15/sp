# Lab 1.1: Clone Stock Widget
### Go to Service Portal -> Service Portal Configuration 
#### open the Widget Editor and open the Stock widget

Click on the menu and choose Clone “Stock”. Give the new widget a name of My Stock and check the Create test page. Then click Submit.

Hint: You can save the widget by pressing Command + S.

Open the test page in a new window or tab without a portal associated. Remember the $sp.do?id=<page_id> trick? 





Lab Validation:
Your (awesome) new test page with your cloned widget will look something like this. Test it out by adding a known stock code (e.g. NOW).

Lab 1.2: Adding Options to the Widget

Back on the Widget Editor, click on the menu and then select Edit option schema.

Create 3 new options:
•	Label: Title		Name: title 		Type: string
•	Label: Price CSS	Name: price_css	Type: string
•	Label: Image CSS	Name: image_css	Type: string

Click Save and then reload the page.

Let’s now add those options to the HTML template:

1.	Add a h2 tag to the top of the HTML to display the title:

<h2>{{::options.title}}</h2>

2.	Locate the span element where the price is displayed and add a new style attribute with the Price CSS option:
<span style={{::options.price_css}}>{{c.data.price | currency:"$"}}</span>

3.	Locate the img element where the stock image is displayed and add a new style with the Image CSS option:
<img style={{::options.image_css}} ng-src="http://chart.finance.yahoo.com/z?s={{c.data.symbol}}&t=1d&z=l"/>

Click Save.

Open or reload the test page again
Right-click + CTRL on the widget instance and select Instance Options:

Enter some text for the Title and then some CSS style to Price CSS and Image CSS option. Click Save.

•	Title:	 	Realtime Stock
•	Price CSS:	color: green;  font-size: 30px
•	Image CSS:	border: 5px solid green; border-radius: 5px; padding: 5px;

reload the page 
you can immediately see the title you added above.

Lab Validation:
Open your test page, and again test it out. This time, open your test page with an actual portal associated (e.g. sp). The page should look something like this: 
Lab 1.3: Adding Widget specific CSS-SCSS

Let’s now add some widget specific CSS-SCSS styling!

Back in the Widget Editor,
create a new class called named myTitleClass and specify some styles of your liking.

.myTitleClass {
  
  font-size: 25px;
  color: $sp-tagline-color;
  font-weight: bold;
  text-decoration: underline;
    
}
Add the new class to the h2 element tag:

<h2 class="myTitleClass">{{::options.title}}</h2>

Click Save.


Lab Validation:
Open your test page within a portal (e.g. sp). The widget should look something like this with your new class applied:

Lab 1.4: Challenge – Working with Unspecified Options
There may be a situation where the widget instance does not have 1 or more options set.
For this, it’s best to add an additional check to ensure the option has a value.

Modify the instance options and clear the text for the Title. 
Notice how even though the title is not set, the h2 tag is still rendered and occupies a visible “empty” space on the page. 
Hint: You can use your browser’s Inspect functionality for this.
So how do we check if the option is set or not?
Take a look at how the span element that contains the localized text ${Requesting stock price}. 
This element is using a special AngularJS directive called ng-if. 
Once you’re done, the page should look something like this with NO visible empty space

Lab 1.5: Challenge – Applying Dynamic Classes

See if you can fly solo and modify your widget so that the price is 
displayed in red if the price is 60 or below or green for anything higher.
Hints:
•	You will need to work with another AngularJS directive called ng-class
•	You will need to specify new classes in the CSS-SCSS section of the widget
•	You will need to remove the inline style for “color” of the price option


Once you’re done, this is how it will/should look like: 


…And with that, you’ve successfully completed Lab 1 
