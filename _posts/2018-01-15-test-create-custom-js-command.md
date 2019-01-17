---
layout: page
title: "Write a Javascript command"
category: test
date: 2018-01-05 15:17:55
order: 55
---

### Create a javascript command

1. Navigate to **Custom Command** in the left-side menu bar, click + button to generate a group command.

   ![][test_js_command]
  
2. Enter the javascript command info.

   **Notes** The scope field has two options, the private means the command can be used only in current project, the public means the command can be used in other projects. By default the value is private.

   ![][test_js_command_info]
  
3. Define the javascript command parameter.

   ![][test_js_command_parameter]
   
4. Define your javascript command logic.

   ![][test_js_command_logic]


5. Add your javascript command in your test case.

   ![][test_add_js_command]

6. You can  reference js variable in the case step

   ![][test_js_casestep]
   ![][test_js_commandlist]

 
7. Refer to [Javascript API Reference](references/references-js-api.html) for OOTB 
Javascript functions   

  [test_js_command]: ../images/test/test_js_command.PNG
  [test_js_command_info]: ../images/test/test_js_command_info.PNG
  [test_js_command_parameter]: ../images/test/test_js_command_parameter.PNG
  [test_js_command_logic]: ../images/test/test_js_command_logic.PNG
  [test_add_js_command]: ../images/test/test_js_command_add.PNG
  [test_js_casestep]: ../images/test/test_js_casestep.PNG
  [test_js_commandlist]: ../images/test/test_js_commandlist.PNG
