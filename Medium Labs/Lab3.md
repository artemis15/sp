# Lab 2.1: Create a Bootstrap Table
This lab will teach you how to load data, in that case active HR Case records, into a table. Let’s start with building the HTML for a Bootstrap table, before we load data to populate the table with. 

You can find documentation on how to create Bootstrap tables here:
•	https://getbootstrap.com/css/#tables
•	http://www.w3schools.com/bootstrap/bootstrap_tables.asp
o	Hint: when you click on Try it yourself, you will be able to copy/paste the full HTML of a table 

You will create that table in a new Widget. Go to Service Portal -> Service Portal Configuration, open the Widget Editor and create a new Widget in which you will write your code.

The table heading (<th>) should contain the following fields:
•	Number, Short Description, Opened for, State, Priority, Task Type, Created on

Also create a table row (<tr>) of demo data, the actual data should reside in a <td> (column) tag.

Hint: All copied code from Word can be quickly re-formatted by marking all the code (Command + A) and then pressing Shift + Tab, which will prettify the code 


Lab Validation:
Your table should look something like this. 
That is all great, but you probably do not want to create HTML for hundreds, maybe even thousands of records (I wouldn’t for even 2 records ). Let’s change this by loading data and adding AngularJS after.

Here is the HTML for that example:
Lab 2.2: Writing the Server Script

Before we start adding AngularJS to our form, let’s make sure we have all the data we need.

To load the cases we use the same API that we would also on the Backend side of things: the GlideRecord.


A step by step description on how to write the code, could sound like this:

Initialize a new, blank, array called hrCases, which will live in the data object.

After that we create a new GlideRecord on the HR Case table to retrieve only active HR cases.

We will make use of the $sp Service Portal Server Side API to retrieve values, display values and even a set of field labels.

For our table we need the following data:
•	Table Headings 
o	Which are the labels of all the fields that we want to see in the table
•	Table Rows
o	Which are the actual HR Case records with their values


ng-repeat is the AngularJS directive that we will use. It awaits an array, so we are initializing an hrCases array that we are populating by iterating over the GlideRecord result.
And that’s how the code looks like:
(function() {
	/* populate the 'data' object */
	/* e.g., data.table = $sp.getValue('table'); */

	//Initialize the 'hrCases' Property in the data object
	data.hrCases = [];

	//Iterate over the HR Case table to retrieve all active cases ordered by number (descending - newest ones first)
	var grHRCase = new GlideRecord("hr_case");
	grHRCase.addActiveQuery();
	grHRCase.orderByDesc("number");
	grHRCase.query();

	//We will use the fields array for ng-repeat on the <tr> level since we want to have all <tr>'s created automatically instead of manually assigning values
	data.fields = ["number", "short_description", "opened_for", "state", "priority", "sys_class_name", "sys_created_on"];
	
	//make use of the $sp API and get all field labels for the provided fields
	data.labels = $sp.getFields(grHRCase, 'number,short_description,opened_for,state,priority, sys_class_name, sys_created_on');

	while(grHRCase.next()) {
		var hrCase = {};
		
		//get all display values for the fields below and write them into the hrCase object
		$sp.getRecordDisplayValues(hrCase, grHRCase, 'number,short_description,opened_for,state,priority, sys_class_name, sys_created_on');
		
		//get the value for sys_id and also write it into the hrCase object
		$sp.getRecordValues(hrCase,grHRCase,'sys_id');

		//push the whole hrCase object into the hrCases array
		data.hrCases.push(hrCase);
	}

	//log the data object to the browser console, so we can click through it and see our results
	$sp.log(data);
	
	return data;

})();
Lab 2.3: Adding AngularJS to the Bootstrap form
Now that we have our data object populated, let’s access that data in the HTML section.

Step 1 – ng-repeat over the table headings
At first we are going to eliminate the double <th> tags by repeating over a single <th> tag.

In our server script we populated a property called labels with all the label names. As everything is in the data object, we will have to use data.labels to access them.

Within that property labels we have an attribute called label, that holds the actual label name. fieldLabel is a key that represents each label object and is only defined here in the HTML – that is part of the notation of the ng-repeat AngularJS directive.

Example:
<th ng-repeat="fieldLabel in data.labels">{{fieldLabel.label}}</th>
Notice the double curly brackets, opening and closing.
This is the actual AngularJS markup to retrieve a value.

Step 2 – ng-repeat over the table rows
Our rows represent the number of records. Let’s say we have 20 records on the server, then we will need 20 rows. You probably already figured it out, but that’s how the <tr> repeat looks like:
<tr ng-repeat="case in data.hrCases">
All our cases are stored in the hrCases array as separate objects.

Step 3 – ng-repeat over the table columns
Now, this is a bit trickier than the heading and rows. The reason for this is that we got changing values in each <td>. So unless you want to write a <td> for each field, here’s where the data.fields object comes into play. We have all technical field names stored in that object. Because of that we can now say for each case get the value of the actual field name that we are currently processing.
<td ng-repeat="field in data.fields">{{case[field]}}</td>
If you would not do that you would have to write:

<td>{{case.number}}</td>
<td>{{case.short_description}}</td>
… etc. 
Lab 2.4: Adding a Record Watcher to the list
Wouldn’t it be awesome if our list would update itself any time a record is deleted or inserted into the HR Case table? You bet it would be! And how hard can it be? Well, not at all 

Just replace your client script with the following code snippet:
function(spUtil, $scope) {
  /* widget controller */
  var c = this;

  spUtil.recordWatch($scope, "hr_case", "active=true", function(name, data) {
		//If there is a new record we want to re-render our list (which is simply executing the server script again)
		c.server.update();
  });
}
The Service Portal spUtil API includes the so called Record Watcher. We are basically just telling it to watch the HR Case table and only records with the defined filter. If the watcher detects a change (like an insert, update or delete), then we want to execute our server script again – because that is the script that builds the list of records. This can be achieved by simply writing c.server.update().

Now you can insert a record in the backend and then come back to your list, that record should now be on top of the list without having to reload the page.

If you want you can add some styling to your table, e.g. by adding the panel class to the top <div> element.

With that you successfully completed Lab 3  
