# Creating a Real-time DataTable Widget
## Introduction
In this lab you will create a real-time datatable widget with a custom page.

### Step 1: Create a new Widget
***Go to Service Portal > Widget > Click New***
- Name: Real Time DataTable
- Id : real-time-datatable
- Click on `submit`

***Body HTML template***
- Copy and paste below `HTML Code` in Widget's HTML Template section
```HTML
<div class="panel panel-success">
  <div class="panel-heading">My Incidents</div>
  <div class="panel-body">
    <table class="table table-hover datatable" ui-jq="dataTable" id="mytable" ui-options="c.dataTableOpt">
      <thead>
        <tr>
          <th>Number</th>
          <th>Short Description</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr ng-repeat="inc in c.data.incidents">
          <td>{{inc.number}}</td>
          <td>{{inc.shortDescription}}</td>
          <td><button class="btn btn-primary" ng-click="c.showData(inc)">
            Show
            </button></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
```
<br/>
***Client Controller***
```javascript
function($scope,spUtil,$log) {
 var c = this;
spUtil.recordWatch($scope, "incident", "active=true", function(name, data) {
		c.server.refresh();
		//$log.log("name :"+name);
		//$log.log("data: "+data);
	});
  }
  ```
  <br/>
  
