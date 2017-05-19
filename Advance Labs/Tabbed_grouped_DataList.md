# Creating a Tabbed-view DataTable Widget
## Introduction
In this lab you will create a tabbed-view datatable widget which embeded OOB Data-table widget

### Step 1: Create a new Widget
***Go to Service Portal > Widget > Click New***
- Name: Tabbed DataTable
- ID: tabbed_DT
- Click on `Submit`


***Body `HTML` Template
- Copy and paste below `HTML` code
```HTML
<div class="tab_container">
  <input id="tab1" type="radio" name="tabs" checked>
  <label for="tab1" class="col-md-2"><i class="fa fa-code"></i><span>${Incidents Open}</span></label>

  <input id="tab2" type="radio" name="tabs">
  <label for="tab2" class="col-md-2"><i class="fa fa-pencil-square-o"></i><span>${Incidents Closed}</span></label>

  <input id="tab3" type="radio" name="tabs">
  <label for="tab3" class="col-md-2"><i class="fa fa-folder-open"></i><span>${Requests Open}</span></label>

  <input id="tab4" type="radio" name="tabs">
  <label for="tab4" class="col-md-2"><i class="fa fa-folder"></i><span>${Requests Closed}</span></label>
 
  <section id="content1" class="tab-content">
    <sp-widget widget="data.dataTableWidgetIncOpen"></sp-widget>
  </section>

  <section id="content2" class="tab-content">
    <sp-widget widget="data.dataTableWidgetIncClosed"></sp-widget>
  </section>

  <section id="content3" class="tab-content">
    <sp-widget widget="data.dataTableWidgetReqOpen"></sp-widget>
  </section>

  <section id="content4" class="tab-content">
    <sp-widget widget="data.dataTableWidgetReqClosed"></sp-widget>
  </section>
</div>
```
<br/>

***CSS/SCSS***
- Copy and Paste below `css`
```CSS
.page{
  margin:0 !important;
  padding:0 !important;
}

*,
*:after,
*:before {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

.clearfix:before,
.clearfix:after {
  content: " ";
  display: table;
}

.clearfix:after {
  clear: both;
}

body {
  font-family: sans-serif;
  background: #f6f9fa;
}

h1 {
  text-align: center;
}

a {
  text-decoration: none;
  outline: none;
}


.tab_container {
  width: 90%;
  margin: 0 auto;
  position: relative;
}

input, section {
  clear: both;
  padding-top: 10px;
  display: none;
}

label {
  font-weight: 400;
  font-size: 14px;
  display: block;
  float: left;
  width: 25%;
  padding: 1.5em;
  color: #757575;
  cursor: pointer;
  text-decoration: none;
  text-align: center;
  background: #f0f0f0;
}

#tab1:checked ~ #content1,
#tab2:checked ~ #content2,
#tab3:checked ~ #content3,
#tab4:checked ~ #content4,
#tab5:checked ~ #content5 {
  display: block;
  padding: 20px;
  background: #fff;
  //color: #999;
  border-bottom: 2px solid #f0f0f0;
}

.tab_container .tab-content .panel,
.tab_container .tab-content h3 {
  -webkit-animation: fadeInScale 0.2s ease-in-out;
  -moz-animation: fadeInScale 0.2s ease-in-out;
  animation: fadeInScale 0.2s ease-in-out;
}
.tab_container .tab-content h3  {
  text-align: center;
}

.tab_container [id^="tab"]:checked + label {
  background: #fff;
  box-shadow: inset 0 3px #0d83dd;
}

.tab_container [id^="tab"]:checked + label .fa {
  color: #0d83dd;
}

label .fa {
  font-size: 1.3em;
  margin: 0 0.4em 0 0;
}

/*Media query*/
@media only screen and (max-width: 930px) {
  label span {
    font-size: 14px;
  }
  label .fa {
    font-size: 14px;
  }
}

@media only screen and (max-width: 768px) {
  label span {
    display: none;
  }

  label .fa {
    font-size: 16px;
  }

  .tab_container {
    width: 98%;
  }
}

/*Content Animation*/
@keyframes fadeInScale {
  0% {
    transform: scale(0.9);
    opacity: 0;
  }

  100% {
    transform: scale(1);
    opacity: 1;
  }
}
```
<br/>

***Client Controller***
- Copy and Paste below code
```javascript
function($scope,$location) {
	/* widget controller */
	var c = this;
	$scope.$on('data_table.click', function(e, parms){
		console.log(parms);
		var p = $scope.data.page_id || 'ticket';
		var s = {id: p, table: parms.table, sys_id: parms.sys_id, view: 'sp'};
		$location.search(s);
	});
}
```
<br/>

***Server-Side Script***
- Copy and Paste below script
```javascript
(function(){

	data.language = gs.getUser().getLanguage();

	var sp_page = $sp.getValue('sp_page');
	var pageGR = new GlideRecord('sp_page');
	pageGR.get(sp_page);
	data.page_id = pageGR.id.getDisplayValue();
	$sp.getValues(data);

	if (input) {
		data.p = input.p;
		data.o = input.o;
		data.d = input.d;
		data.q = input.q;
	}

	data.p = data.p || 1;
	data.o = data.o || $sp.getValue('order_by');
	data.d = data.d || $sp.getValue('order_direction');

	data.page_index = (data.p - 1);
	data.window_size = $sp.getValue('maximum_entries') || 10;
	data.window_start  = (data.page_index * data.window_size);
	data.window_end = (((data.page_index + 1) * data.window_size));

	var widgetParamsIncOpen = {
		table: 'incident', 
		fields: "number,business_service,short_description,incident_state",
		o: "number",
		d: "desc",
		filter: "caller_id=javascript:gs.getUserID()^active=true^state!=6",
		window_size: 10,
		view: 'sp',
		title: gs.getMessage('Incidents'),
		show_breadcrumbs: true,
		show_keywords: true
	};

	var widgetParamsIncClosed = {
		table: 'incident', 
		fields: "number,business_service,short_description,incident_state",
		o: "number",
		d: "desc",
		filter: "caller_id=javascript:gs.getUserID()^active=false^ORincident_state=6",
		window_size: 10,
		view: 'sp',
		title: gs.getMessage('Incidents'),
		show_breadcrumbs: true,
		show_keywords: true
	};

	var widgetParamsReqOpen = {
		table: 'sc_req_item', 
		fields: "number,cat_item,short_description,state",
		o: "number",
		d: "desc",
		filter: "u_requested_for=javascript:gs.getUserID()^ORopened_by=javascript:gs.getUserID()^active=true",
		window_size: 10,
		view: 'sp',
		title: gs.getMessage('Requests'),
		show_breadcrumbs: true,
		show_keywords: true
	};

	var widgetParamsReqClosed = {
		table: 'sc_req_item', 
		fields: "number,cat_item,short_description,state",
		o: "number",
		d: "desc",
		filter: "u_requested_for=javascript:gs.getUserID()^ORopened_by=javascript:gs.getUserID()^active=false",
		window_size: 10,
		view: 'sp',
		title: gs.getMessage('Requests'),
		show_breadcrumbs: true,
		show_keywords: true
	};

	data.dataTableWidgetIncOpen = $sp.getWidget('widget-data-table', widgetParamsIncOpen);
	data.dataTableWidgetReqOpen = $sp.getWidget('widget-data-table', widgetParamsReqOpen);
	data.dataTableWidgetIncClosed = $sp.getWidget('widget-data-table', widgetParamsIncClosed);
	data.dataTableWidgetReqClosed = $sp.getWidget('widget-data-table', widgetParamsReqClosed);
	
})();

```
<br/>

### Create a new Page
- Create a new page and embeded `Tabbed DataTable` widget inside it

***Verify the end result***<br/>
![move to header](/assets/tabbed_dt.png)<br/>

## Hurray!!! Lab is done :)
