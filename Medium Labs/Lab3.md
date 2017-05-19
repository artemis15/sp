# Lab 3.1: Create a Bootstrap Table
This lab will teach you how to load data, in that case active HR Case records, into a table.<br/>
Let’s start with building the HTML for a Bootstrap table, before we load data to populate the table with.<br/> <br/>
You can find documentation on how to create Bootstrap tables here:
- https://getbootstrap.com/css/#tables
- http://www.w3schools.com/bootstrap/bootstrap_tables.asp

`Hint:` when you click on Try it yourself, you will be able to copy/paste the full HTML of a table <br/> 

You will create that table in a new Widget. 
### Go to Service Portal -> Service Portal Configuration, 
- open the Widget Editor and create a new Widget in which you will write your code.
- The table heading (```<th>```) should contain the following fields:
  - Number
  - Short Description
  - Opened for
  - State
  - Priority 
  - Task Type
  - Created on

- Also create a table row (```<tr>```) of demo data, the actual data should reside in a ```<td>``` (column) tag.

`Hint:` All copied code from Word can be quickly re-formatted by marking all the code (Command + A) and then pressing Shift + Tab, which will prettify the code. <br/>


### Lab Validation:
***Your table should look something like this.*** <br/><br/>
![move to header](/assets/tableservice.png)<br/>

Let’s change this by loading data and adding AngularJS after.<br/>

Here is the HTML for that example:
```HTML
<!-- Table without AngularJS  -->
<div class="container">
  <div class="table-responsive">
    <table class="table">
      <thead>
        <tr>
          <th>Number</th>
          <th>Short Description</th>
          <th>Opened for</th>
          <th>State</th>
          <th>Priority</th>
          <th>Task Type</th>          
          <th>Created</th>                    
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>123</td>
          <td>This is a Short Description</td>
          <td>Rita Requester</td>
          <td>In Progress</td>
          <td>2 - High</td>
          <td>HR Benefits</td>          
          <td>2016-07-08 14:30:00</td>                    
        </tr>        
      </tbody>
    </table>
  </div>
</div>

```
# Lab 3.2: Writing the Server Script

Before we start adding AngularJS to our form, let’s make sure we have all the data we need. <br/>

To load the cases we use the same API that we would also on the Backend side of things: the GlideRecord.<br/>

A step by step description on how to write the code, could sound like this:<br/>

- Initialize a new, blank, array called hrCases, which will live in the data object.
- After that we create a new GlideRecord on the HR Case table to retrieve only active HR cases.
- We will make use of the $sp Service Portal Server Side API to retrieve values, display values and even a set of field labels.
- For our table we need the following data:
  - Table Headings 
  - Which are the labels of all the fields that we want to see in the table
  - Table Rows
  - Which are the actual HR Case records with their values

ng-repeat is the AngularJS directive that we will use.<br/> 
It awaits an array, so we are initializing an hrCases array that we are populating by iterating over the GlideRecord result.<br/><br/>
***And that’s how the code looks like:***
```javascript
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
```
# Lab 3.3: Adding AngularJS to the Bootstrap form
Now that we have our data object populated, let’s access that data in the HTML section.

### Step 1 – ng-repeat over the table headings
At first we are going to eliminate the double ```<th>``` tags by repeating over a single ```<th>``` tag.

In our server script we populated a property called labels with all the label names. <br/>
As everything is in the data object, we will have to use data.labels to access them.<br/>
Within that property labels we have an attribute called label, that holds the actual label name. <br/>
fieldLabel is a key that represents each label object and is only defined here in the HTML – that is part of the notation of the <br/>
ng-repeat AngularJS directive.

### Example:
```HTML
<th ng-repeat="fieldLabel in data.labels">{{fieldLabel.label}}</th>
```
Notice the double curly brackets, opening and closing.<br/>
This is the actual AngularJS markup to retrieve a value.<br/>

### Step 2 – ng-repeat over the table rows
Our rows represent the number of records. Let’s say we have 20 records on the server, then we will need 20 rows. <br/>
You probably already figured it out, but that’s how the ```<tr>``` repeat looks like:
```HTML
<tr ng-repeat="case in data.hrCases">
All our cases are stored in the hrCases array as separate objects.
```
### Step 3 – ng-repeat over the table columns
We got changing values in each ```<td>.``` So unless you want to write a ```<td>``` for each field, here’s where the data fields object comes into play. We have all technical field names stored in that object. Because of that we can now say for each case get the value of the actual field name that we are currently processing.
```HTML
<td ng-repeat="field in data.fields">{{case[field]}}</td>
```
If you would not do that you would have to write:
```HTML
<td>{{case.number}}</td>
<td>{{case.short_description}}</td>
… etc. 
```
# Lab 3.4: Adding a Record Watcher to the list
- Just replace your client script with the following code snippet:
```javascript
function(spUtil, $scope) {
  /* widget controller */
  var c = this;

  spUtil.recordWatch($scope, "hr_case", "active=true", function(name, data) {
		//If there is a new record we want to re-render our list (which is simply executing the server script again)
		c.server.update();
  });
}
```
The Service Portal spUtil API includes the so called Record Watcher.
We are basically just telling it to watch the HR Case table and only records with the defined filter. If the watcher detects a change (like an insert, update or delete), then we want to execute our server script again – because that is the script that builds the list of records. This can be achieved by simply writing ```c.server.update().```

- Now you can insert a record in the backend and then come back to your list, that record should now be on top of the list without having to reload the page.

If you want you can add some styling to your table, e.g. by adding the panel class to the top ```<div>``` element.

## With that you successfully completed Lab 3  
