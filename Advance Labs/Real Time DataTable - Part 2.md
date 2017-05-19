# Creating a Real-time DataTable Widget - Part 2
## Introduction
In this lab you will continue from [Real Time DataTable - Part 1](Real_Time_DataTable_Part_1.md)

***Create a new record in `sp_dependency` table***
- Name: ui.utils
- Angular Provider Name: ui.utils
- Include on page load: true
- Save the record
- Add the following `JS Includes` in the given order<br/>

| Order | Source | Display Name & JS File URL|
| :------ | :----| :-------------------------------------------------------------------|
| 100 | URL| https://cdn.datatables.net/buttons/1.3.1/js/buttons.html5.min.js|
| 100 | URL| https://cdnjs.cloudflare.com/ajax/libs/angular-ui-utils/0.1.1/angular-ui-utils.min.js|
| 100 | URL| https://cdn.datatables.net/buttons/1.3.1/js/buttons.print.min.js|
| 100 | URL| https://cdn.datatables.net/buttons/1.3.1/js/dataTables.buttons.min.js|
| 100 | URL| https://cdn.datatables.net/buttons/1.3.1/js/buttons.flash.min.js|
| 110 | URL| //cdn.datatables.net/1.10.15/js/jquery.dataTables.min.js|
| 120 | URL| https://cdn.datatables.net/1.10.12/js/dataTables.bootstrap.min.js|

- Add the following `CSS Include` <br/>

| Order | Source | Name & CSS File URL|
| :------ | :----| :-------------------------------------------------------------------|
| 100 | URL| https://cdn.datatables.net/1.10.12/css/dataTables.bootstrap.min.css|

- Update dependency

***Open `Real Time DataTable` widget and add `ui.utils` dependency from `dependency` related list***

***Modify `HTML` Template***
- Replace below code<br/>
```HTML
<table class="table table-hover">
```
<br/>

`WITH`
```HTML
<table class="table table-hover datatable" ui-jq="dataTable" id="mytable" ui-options="c.dataTableOpt">
```
<br/>

***Modify `Client-controller` Script***
- Add below code
```javascript
c.dataTableOpt = {
   //custom datatable options 
  // or load data through ajax call also
  "aLengthMenu": [[5,10, 25,50, 100,-1], [5,10,25, 50, 100,'All']]
  };
```
<br/>

***Verify Widget***
- End result will look like below<br/>
![move to header](/assets/realdt2.png)
