# Creating Process flow in service portal
## Introduction
In this lab you will create a custom process flow with a custom page and populated with standard widgets.

## Step 1: Create a new Widget
***Go to Service Portal > Widget > Click New***
- Name: Process Flow
- Id: process-flow
- Click on `submit`

***Body HTML template***
- Copy and paste below `HTML Code` in Widget's HTML Template section
```HTML
<div class="container">
  <div class="process">
    <div class="process-row">
      <div class="process-step" ng-repeat="d in c.data.choices">
        <button type="button" disabled="disabled" class="btn btn-default btn-circle" ng-if="c.data.currentValue!=d"><i class="fa fa-check fa-3x" aria-hidden="true"></i></button>
        <button type="button" disabled="disabled" class="btn btn-success btn-circle" ng-if="c.data.currentValue==d"><i class="fa fa-check fa-3x" aria-hidden="true"></i></button>  
        <p>{{d}}</p>       	
      </div>
    </div>
  </div>
 </div>
```
<br/>

***CSS/SCSS***
- Copy and paste below `CSS` in Widget's CSS/SCSS Section
```CSS
.btn-circle {
  width: 40px;
  height: 40px;
  text-align: center;
  padding: 6% 0;
  font-size: 6px;
  line-height: 0.6;
  border-radius: 100%;
}

.process-row {
    display: table-row;
}

.process {
    display: table;     
    width: 100%;
    position: relative;
}

.process-step button[disabled] {
    opacity: 1 !important;
    filter: alpha(opacity=100) !important;
}

.process-row:before {
    top: 20px;
    bottom: 0;
    position: absolute;
    content: " ";
    width: 100%;
    height: 1px;
    background-color: #ccc;
    z-order: 0;
    
}

.process-step {    
    display: table-cell;
    text-align: center;
    position: relative;
    padding-left: 0%;
    padding-right: 5%;
}

.process-step p {
    margin-top:10px;
    
}

.btn-circle.active {
    border: 2px solid #cc0;
}

```
<br/>

***Server Side Scripts***
- Copy and Paste below `Server-Side Script` in Widget's Server Side Section
```javascript
(function() {
  /* populate the 'data' object */
  /* e.g., data.table = $sp.getValue('table'); */

	data.choices=[];
	
	
	var grInc=new GlideRecord("incident");
	if(grInc.get('8662791bdbac36401466f78dbf9619cc'))
		{
			data.currentValue=grInc.getDisplayValue('state');
		}
	
	var gr = new GlideRecord('sys_choice');
	gr.addEncodedQuery("name=incident^element=state^orderBysequence");
	gr.query();
	while(gr.next())
		{
			var _choiceLabel = gr.getValue('label');
			data.choices.push(_choiceLabel);
		}
})();
```
<br/>

## Step 2: Create a new Page
***Go to Service Portal > Page > Click New***
- Name: process_flow - Test Page
- ID: process_flow
- Click on `Submit` button.
- Once submitted, Click on `Open in Page Designer` related link
- In Page designer, Place `Process Flow` widget inside a container > row > Column at top location.
- View paget from following link `http://instance-name.service-now.com/sp?id=process_flow`. End result will be like below:<br/>
![move to header](/assets/process_flow.PNG)<br/>

# Challenge
- Embed `process flow` widget with `Form` widget
