---
title: "Best Practices"
category: references
date: 2019-01-15 15:17:55
last_modified_at: 2019-07-29 16:52:00
order: 8
---

# Best Practices
***
### Long load time AJAX call
* As we know, the modern web application always load data by AJAX call. Sometime, it may needs a long time to get the AJAX call result. The automation test case become not stable in this case. It's because that, the test case run the test steps without waiting the AJAX call end.
* Normally, there is a loading indicator on the HTML to indicate a AJAX call is completed or not. We could resolve the problem by adding the **waitElement** command after the AJAX call test step. So that the system will wait a certain seconds until the loading indicator element becomes **visible/hidden/enabled/disable**.
* The **waitElement** command:
	* **Type**: The value could be Visible, Hidden, Enabled and Disable.
	* **Timeout**: The waiting seconds.
	* **Element ID/Element CSS/XPATH**: These values can be used to locate the AJAX loading indicator HTML element on the UI page.

   ![][references-wait-element]

### IDA plug-in troubleshooting
* When you run IDA plug-in for replay you might meet issue for the plug-in. You should see the step with highlighted red color.When you move the mouse the red icon,it will show the detail issue.

   ![][references-idarecorder]

You can use below ways to collect logs of plug-in.

1. You can use the browser console to see the logs for IDA recorder plug-in console.

   ![][references-pluginConsole]

2. You can use the browser console to see the logs for  UI console.

   ![][references-browserconsole]

3.  Manage the extension of IDA plug-in.Switch the "Developer mode" on the right top page.Then click the Inspect views "background page" to see background.js console message.

    ![][references-plugin]


    ![][references-backgroundconsole]

4.  You can also check server side console to see any logs with this step.


  [references-wait-element]: ../images/references/references-wait-element.png
  [references-idarecorder]: ../images/references/IDARecorder.png
  [references-browserconsole]: ../images/references/Browserconsole.png
  [references-pluginConsole]: ../images/references/PluginConsole.png
  [references-plugin]: ../images/references/Plugin.png
  [references-backgroundconsole]: ../images/references/IDABackgroud.png