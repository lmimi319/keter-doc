---
layout: page
title: "Testing command Reference"
category: references
date: 2018-01-05 15:17:55
order: 1
---

This document refers to the Command Editor options and not JavaScript API to call a command. JavaScript API for the test case step can be viewed by clicking the label for the step. API inputs may not be named exactly the same as Command Editor fields. The correspondence is shown in the following table. For example, **Assignee** in the Dialog box corresponds to a **user** in the API.

  ![][command_start_process_javascript_API] 
  
  ![][command_start_process_editor] 

There are four category of commands:

* [BPM](#bpm)
* [BPM Assertion](#bpm-assertion)
* [UI](#ui)
* [UI assertion](#ui-assertion)
* [Utility](#utility)

___

### **BPM** 

This category of commands are for calling server side components. There are a lot of common input fields. Below are some statements which are common for most of the commands in this category.  

___

**Assignee:** When specified, the command is executed by the specified BPM user. Drop down lists all *BPM user names* defined in the BPM Configuration of the Test Project which is connected to. More details refer to [**BPM Configuration/Add user to a BPM server**][1].

**Exception:** is an exception case. Checked means we are expecting to get an error for the test case. Unchecked means we are expecting to get a normal result from the test case.

**Comment:** Optional. Not part of any command and can be used for documenting test case step.

**Params:** Json format. If the template of parameters is rendered successfully by selecting service, the field is required. The parameters are defaulted based on the service signature. The template of parameters includes keys of data and you only need to fill in value. *e.g:*

    {
	"variable_name": "value",
	"variable2_name": "value2"
    }

The ![][command_params_error_icon] icon will appears below *Expected Output* input box when the wrong *Params* is filled out after click ![][command_expected_output_refresh_button] button in the Command Editor Dialog. The error message can be got by hovering on the ![][command_params_error_icon] icon.

**Expected Output:** Used for validating command response. In some cases, there is a refresh button, which can be used to get default expected results. Make sure to fill out params before clicking refresh. If refresh does not work, execute the case step with out expectedOutput set. If passed, edit the step and click on ![][command_expected_output_refresh_button] button in the Command Editor Dialog to capture the results.

**TaskName:** Drop down lists all task names in the Process Application of the Test Project which is connected to. 

**Json Path:** Json path to a variable in the output json data.

**Variable Name:** Variable name to save the value the json path points to. This variable can be accessed via ${variable_name} in later commands in this test case.

___


  |   Field                          |Parameters                          | Description                                                                       |
  | -------------------------------- |-----------------------------------------------------------------------------------|                                          
  | loginPortal                      |Assignee: select a user defined in BPM Configuration.|Login into BPM portal. As a result BPM Portal page is opened.                                                                   | 
  | loginBPMoC                  	 |Assignee: select a user defined in BPM Configuration.|  Login into BPM on cloud.As a result BPM on cloud page is opened.  
  | openInstanceDetail               |Assignee: select a user defined in BPM Configuration.|Open the instance detail page for current instance in the context.|
  | startProcess                     |Process : name of the process to be started.<br>Params: : (optional) input parameters in JSON format. Tip: when creating a case from the Test case menu for a Process, the default parameters are generated.<br>|Start a BPM process by REST API, only exposed process are supported by default. Install Keter Toolkit to support all processes. |                                                                        
  | startHumanService                |Service : name of a human service to be started.Select from drop down.<br>Params: human service input list. Only simple input arguments are supported.|Tests Human Service in stand alone mode.| 
  | startExposedHertiageHumanService |Service : name of a human service to be started.Select from drop down.<br>Params: human service input list. Only simple input arguments are supported.|Tests Human Service in stand alone mode, please make sure the human service is exposed to a specify team
  | startAjaxService                 |Exception: is an exception case.<br>Service: service name, select from drop down.<br>Params: service input list.<br>Expected Output: expected service output in JSON.Tip: first, execute the case step with out expectedOutput set. If passed, edit the step and click on ![][command_expected_output_refresh_button] button in the Command Editor Dialog to capture the results.|Start an ajax service edited in Eclipse PD by REST API.To call services created in Web PD, use startServiceFlow command.|
  | startSystemService               |Exception: is an exception case.<br>Service: service name, select from drop down.<br>Params: service input list.<br>Expected Output: expected service output in JSON.Tip: click on ![][command_expected_output_refresh_button] button in the Command Editor Dialog to capture the example output.|Starts a Generic or Integration service edited in Eclipse PD,please install Keter Toolkit to support system service.To call services created in Web PD, use startServiceFlow command|      
  | saveSQLQueryResult               |SQL: sql statement. <br>Data Source Name: data source JNDI name as defined in target BPM environment. Default dataSourceName is jdbc/TeamWorksDB.<br>Key: key name.|Save the SQL query result into context.|
  | startSQLQuery                    |SQL: sql statement. <br>maxRows: max rows<br>Data Source Name: data source JNDI name as defined in target BPM environment. Default dataSourceName is jdbc/TeamWorksDB.<br>Expected Output: expected output.<br>Json Path: json path to a variable in the output.|Perform SQL Query by REST API, please install BPM Testing Asset Toolkit to support SQL Query.|   
  | startUCA                         | UCA: uca name, select from drop down.<br>Params: UCA inputs.|Start message UCA.                               |    
  | startServiceFlow                 |Exception: is an exception case. <br>Service: select service name from drop down.<br>Params: service input list.<br>Expected Output: expected service output in JSON, click on refresh to auto generate.| Executes a Service developed in Web PD.|
  | startAdHoc                       |Ad Hoc Name: Ad Hoc name, select from drop down. |Start AdHoc event (depreciated) for stand alone activities use runAdHocActivity. Can be executed in a context of a business process instance. Can be added to a test case created based on a process or bpd.|    
  | runAdHocActivity                 | Ad Hoc Activity Name: ad Hoc activity name,select from drop down. |Starts AdHoc Activity, can be executed in a context of a business process instance. Can be added to a test case created based on a process or bpd.|    
  | runTaskByDisplayName             |Task Name: task name, select from drop down. |  Run task by display name.       |    
  | runTaskByActivityName            |Task Name: task name, select from drop down.|Run task by Activity name. Can only be used in a context of process instance execution.|                                 
  | assignTask                       |Task Name: task name, select from drop down.<br>To User: select from drop down list of users defined in Keter/BPM Admin for target BPM server. |  Assign task. Can only be used in a context of process instance execution .|
  | claimTask                        |Task Name: task name, select from drop down.|   Claim task.                   | 
  | finishTask                       |Task Name: task name, select from drop down.<br>Output: task output, json format. Set this value to the output of the task.|Complete a given task and set output for the task. Can only be used in a context of process instance execution.| 
  | addInstanceId                    |Instance ID: instance id of the process.|Add the process instance id to context. Use this command if the process was not started as part of the current use case.                                | 
  | openBPMDefaultUrl                |Assignee: select a user defined in BPM Configuration.|Go to the default BPM Process Portal landing page.                          | 
  | setCurrentInstanceIndex          |Index: current instance index.    |Switch the working instance by specify the index of the multiple process instances.|
  | getTaskIdByName                  |Task Name: task name, select from drop down.|Get task id by name.| 
  | getLatestInstanceIdByProcess     |Process Name: Process name to get latest instance. Select from drop down.|   Get the latest process instance id by process name and adds it to the context.| 
  | getInstanceIdByInstanceName      |Process Name: Process name to get instances. Select from drop down.<br>Instance Name: instance name of the instance id.|  Get the process instance id by process name and instance name.    | 
  | getInstanceIdByTaskName      |Process Name: Process name to get tasks. Select from drop down.<br>Task Name: task name.  |  Get the process instance id by process name and task subject name.      | 
  | getInstanceIdByTaskUrl           |Assignee: select a user defined in BPM Configuration.|   Get the process instance id by the task id in url.                                  | 
  | getInstanceIdByBusinessData      | processName: process name, select from drop down.<br>Business Data Alias: business data alias name.<br>Business Data Value: business data value.     |  Get the process instance id by process name and business data.    | 
  | fireTimer                        |Token: timer name selected from drop down.|     Fire timer for the current instance.                           |                                 
  | startRestApi                     | API Name:rest api name.<br>Parameter: rest api parameter template.  <br>Expected Value: the expected rest api response.   |   Assert rest api result.|  
 
___                         
  
### **BPM Assertion**  

This category is for asserting server side components. Here are statements of common input fields.

___

**Assignee:** When specified, the command is executed by the specified BPM user. Drop down lists all *BPM user names* defined in the BPM Configuration of the Test Project which is connected to. More details refer to [**BPM Configuration/Add user to a BPM server**][1].

**Task Name**: Name of the task that needs to be asserted. Drop down lists all *Task names* of current process.

**Comment:** Optional. Not part of any command and can be used for documenting test case step.
 
___

  |   Field                                 | Parameters                                |Description                                                        |
  | --------------------------------------- |------------------------------------------------------------------ ------- ------- ------- - ------- -------  |                                          
  | assertProcessInstanceStatus             |Instance Status: expected status of the current process instance.|Check current process instance status. <br>Possible values: <br>*Active*<br>*Completed*<br>*Failed*<br>*Terminated*<br>*Suspended*|                                                         
  | assertProcessInstanceData               |Expected Value: JSON object, expected value of the data.<br>**Notes:** <br>  Before adding this step, run the test case and look at the report. In the **Process Instance** section, click on the **click to show full data** link. <br>![][command_instance_data_template]<br>Copy the shown JSON into the **Expected Value** as data template. Then change the value as you need. If your data has auto generated fields, like current dates, instance ids or some other unique identifiers, they have to be removed from the JSON.| Assert the data of current process instance. Can only be used in a context of process instance execution.|  
  | assertTaskAssignmentByUser              | Task Name: name of the task that needs to be asserted. Select from drop down.|   Check user is  assigned (claimed ) to the task. Can only be used in a context of process instance execution.
  | assertTaskStatus                        | Task Name: name of the task that needs to be asserted. Select from drop down.<br>Task Status : expected status of the task.|    Check the status of a BPM task for current process instance. <br>Valid task status values: <br>*Received* <br>*Closed*|  
  | assertNextTaskName                      |Task Name: name of the task that needs to be asserted. Select from drop down.|   Check the task is received.| 
  | assertTaskNotGenerated                  |Task Name: name of the task that needs to be asserted. Select from drop down.|  Check the task is not generated.                     |  
  | assertTaskData                          |Task Name: name of the task that needs to be asserted. Select from drop down.<br>Expected Value: expected value of the data.<br>**Notes:**<br>Before adding this step, run the test case and look at the report. In the **Task Data** section, click on the **click to show full data** link.<br>![][command_task_data_template]<br> Copy JSON value into the **Expected Value** as data template. Then change the value as you need. If your data has auto generated fields, like current dates, instance ids or some other unique identifiers, they have to be removed from the JSON.|  Check the task data of current process instance.It checks the variables saved in BPM Task execution context. Use UI Assertions to check on page contents during the coach execution.|  
  | assertServiceData                       |Expected Value: expected value of the data.<br>**Notes:**<br>Before adding this step, run the test case and look at the report. In the **Service Data** section, click on the **click to show full data** link. <br>![][command_service_data_template]<br>Copy JSON value into the **Expected Value** as data template. Then change the value as you need. If your data has auto generated fields, like current dates, instance ids or some other unique identifiers, they have to be removed from the JSON.|      Check the currenct service data.                                                 |   
  
___

### **UI**  

In most cases, the UI commands are recorded using the Keter plug in. If you find a need to add a command manually, for example, validation command, look at the recorded command for the element and copy the location information from it. 
<br>*e.g:*
Any one or combination of the recorded values can be used to identify the control:  Control ID, Element ID or XPATH. If Label is unique on the page, it can be used as well. Enough location arguments are required to uniquely identify an element on the page. **Keter** cycles through available ids until it finds the element. For example, if you recorded a select step and later moved the control around on the page, the Control ID and XPATH are probably different from the recorded step, but Element ID is still the same.

Here are statements of common input fields.

___

**Assignee:** When specified, the command is executed by the specified BPM user. Drop down lists all *BPM user names* defined in the BPM Configuration of the Test Project which is connected to. More details refer to [**BPM Configuration/Add user to a BPM server**][1].

**Label:** The label of the control.

**Value:** The value of the control.

**Contorl ID:** The ID of the control. Control ID is the PATH control IDs leading to the selected control id. 

**Element ID:** The ID of the element.

**XPATH:** The xpath of the control.

**Comment:** Optional. Not part of any command and can be used for documenting test case step.

___
   
  |   Field                | Parameters                          | Description                       |
  | ---------------------- |-------------------------------------------------------------------------|                                
  | bpmFileDropzone        | Value: the value of the BPM file.<br>Control ID: the control id of BPM file drop zone.<br>Default value: the value of default. |  BPM file drop zone.   |  
  |bpmFileUploader         | Value: the value of the BPM file.<br>Control ID: the control id of BPM file that needs to be Uploaded. <br>Default value: the value of default. | BPM file uploader.|
  | checkbox               |Refer to common statement.  |Set the value of checkbox control. To clear checkbox, leave Value blank.To check the box, value should be the same as Label of the Checkbox CV.<br>*e.g:*<br>![][command_UI_Checkbox]<br> The value should be set to *Bool1*.|  
  | click                  |Value: Click text.<br>Type: *Link* or *Button*.|   Click an element by id , CSS or xpath.<br>**Notes:**<br>BPM UI toolkit has *id* on a button and Coach v8 and BP3 do not. Thus the later two can only be identified by XPATH. Moving the coach view around the page may change its xpath and break the use case.| 
  | coachControl           |value type: select type from drop down. <br>Default Value: default value of the control.|  Set the value of coach control. This is a generic setter. Value should match the selected control type.|  
  | confirmOK              |  N/A                                   |   Click ok button.                                 | 
  | confirmCancel          |  N/A                                   |   Click the cancel button. |  
  | doubleClick            |Value: Click text.| Double click an element by id, CSS or xpath. Be similar to **click**.| 
  |file                    |Value: file name that needs to be uploaded.|  Upload file.|
  | open                   |  URL: the URL of browser.              |Open an browser. Should always follow by **selectWindow**.|
  | cleanCookies           |  Refer to common statement.            |Close selected user's cookies.|
  | close                  |  Refer to common statement.            |Close current opened browser.|
  | radio                  |  Refer to common statement.            |Set the value of radio control. Value should be the LABEL on the CV control.<br>*e.g:*<br>![][command_UI_radio]<br> Value should be set to *Make a selection*.|
  | saveCoachControl       | Key : Key is a name of a variable, which can later be referenced as ${key} in a value field of any command. |  Put the control value into a key. <br>Tip:<br> a) record a step to set the value of the control;<br>b) edit the recorded step in Command Editor and change the command to saveCoachControl;<br>c) set the Key.<br> If the control you try to save is read only, record any other control in the located at the same level ( e.g in the container ).  Modify the Control ID path to match the control you are trying to save.|  
  | saveText               | Key : Key is a name of a variable, which can later be referenced as ${key} in a value field of any command. |  Put the output text value to a key.                                  |   
  | select                 |Refer to common statement.              |  Set the value of select (drop down) control. Value is a json list of selected display values for this Select or Multi Select CV. <br>*e.g:*``["Selected value1","Selected value2"] ``| 
  | selectWindow           |  info : window information.                 |    Select window by window info.|                                      
  | text                   |Refer to common statement.                   |Set the value of any control, which UI accepts textual input. Example: input text CV, Integer CV, Date Picker.|    
 
___
     
     
### **UI Assertion** 

___
 

  |   Field                | Parameters                          | Description                                                             |
  | ---------------------- |-------------------------------------------------------------------------|                                
  | assertSelect           | controlId : control id<br>Setion:the section ID of the control<br>Label:the label name of the control<br>Element ID:the ID of the element<br>Element CSS:the css of the Element<br>XPATH: the xpath of the coach control<br>Expected Value: the expected value of the control<br> |  Check select value   |  
  | assertInputText        | controlId :  control id<br>Setion:the section ID of the control<br>Label:the label name of the control<br>Element ID:the ID of the element<br>Element CSS:the css of the Element<br>XPATH: the xpath of the coach control<br>Expected Value: the expected value of the control<br> |  Check coach text field value       |                                    
  | assertOutputText       | controlId :  control id<br>Setion:the section ID of the control<br>Label:the label name of the control<br>Element ID:the ID of the element<br>Element CSS:the css of the Element<br>XPATH: the xpath of the coach control<br>Expected Value: the expected value of the control<br> |  Check coach output text  value     |
  | assertTextarea         | controlId :  control id             |    assert the textarea value                                |                                                                         
  | assertDatePicker       | controlId :  control id<br>Setion:the section ID of the control<br>Label:the label name of the control<br>Element ID:the ID of the element<br>Element CSS:the css of the Element<br>XPATH: the xpath of the coach control<br>Expected Value: the expected value of the control<br> |  Assert the date picker value     |
  | assertCheckbox         | controlId :  control id<br>Setion:the section ID of the control<br>Label:the label name of the control<br>Element ID:the ID of the element<br>Element CSS:the css of the Element<br>XPATH: the xpath of the coach control<br>Checked: the checkbox is checked or not  |     assert checkbox is checked or not                               |      
  | assertSwitch           | controlId :  control id<br>Setion:the section ID of the control<br>Label:the label name of the control<br>Element ID:the ID of the element<br>Element CSS:the css of the Element<br>XPATH: the xpath of the coach control<br>Checked: the Switch box is on or off |  assert Switch box is on or off                                   |                                   
  | assertRadio            | controlId :  control id<br>Setion:the section ID of the control<br>Label:the label name of the control<br>Element ID:the ID of the element<br>Element CSS:the css of the Element<br>XPATH: the xpath of the coach control<br>Checked: the radio box is checked or not   |assert radio box is on or off                                 |                                      
  | assertTableRows        | Control ID: the id of table<br>Expected Rows: the row number of the table |     assert row number of the table                               |   
  | assertTableContent     | Control ID: the id of table<br>Column: the name of the column <br> Row Number: the row number of table<br>Expected value: the cell value of the table   |    assert the cell value of the table                                | 
  | assertElement              |  Element ID: the id of element<br>Element css: the css of element <br> Xpath: the xpath of element<br>Expected value: the expected value of the element<br>Expected visibility: the visibility  of element <br> Ignore Element XPATHs: ignore the element xpath   |   assert the value of the element |
  | assertTextPresent          | Text: the text on the UI           |   assert text is appear on UI                                 |  
  | assertTextNotPresent       | Text: the text on the UI         |   assert text is not appear on UI                                
  | assertValidationPassed                  | errorMessage : error message       |  Check whether the coach page is passed the validation or not.                  |
  | assertCoachControl                      |  value : coach value <br>label - control label <br>controlId : coach control id <br>elementId : element id of the control<br>xPath : xpath of the control <br>Expected Value: the expected value of the control <br>Expected Value Tyep: the  value Type of the control (Integer,String) <br>Expected Visibility:the visibility of the control|  assert the control value,type,visibility                   |
  
___  
  
### **Utility**

___  


  |   Field                | Parameters                          | Description                                                             |
  | ---------------------- |-------------------------------------------------------------------------|                                          
  | debug                  |  log - log text will be shown in console  |   Command for debug, case will stop at this step                                 |      
  | wait                   | time - the seconds to be wait  |   Wait for specify seconds                                 |     
  | putContext             |  key - name of key <br>value - name of value |  Put a key-value pair to context                                  |     
  | addContext             |   key - name of key <br>value - name of value | Add a key-value pair to list of context                                   |                                    |     
  | randomString           |    length : length of the generated random string |Generate a specified length random string.                                |                                     
  | randomNumber           |    length : length of the generated random string |Generate a specified length random number                                |                                       
  | dateString             |   key : key for save data string <br>Days:  Use currenct date add the number of days <br>Format: Formate of date   |      Calculate a new date String                               |  

___  

[1]: ../administration/administration-bpm-configuration.html#add-user-to-a-bpm-server
[command_expected_output_refresh_button]: ../images/command/command_expected_output_refresh_button.png
[command_start_process_editor]: ../images/command/command_start_process_editor.png
[command_start_process_javascript_API]: ../images/command/command_start_process_javascript_API.png
[command_params_error_icon]: ../images/command/command_params_error_icon.png
[command_instance_data_template]: ../images/command/command_instance_data_template.png
[command_task_data_template]: ../images/command/command_task_data_template.png
[command_service_data_template]: ../images/command/command_service_data_template.png
[command_UI_radio]: ../images/command/command_UI_radio.png
[command_UI_Checkbox]: ../images/command/command_UI_Checkbox.png