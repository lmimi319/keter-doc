---
layout: page
title: "Pipeline script"
category: pipeline
date: 2018-01-05 15:17:55
order: 3
---
### Pipeline script summary

  In pipeline stage step definition, there is a step called script, which allows users to execute script in the server where Keter is deployed.

### Define script

  In **Edit Step** modal, select **Script** as **Type** then you can define one or more scripts in **Script** text area. For multiple scripts, each of them need to start from a new line.
  
  ![][pipeline_create_script]
  
  After the pipeline is executed, you can view the script execution result.
  
  ![][pipeline_script_result]  
  
### Script Sample

  1. You can use **curl** to call a RESTful service or Web Service in Script. For example, below script calls a BPM REST API by curl.
  
  curl -H "Accept:application/json" -H "Authorization:Basic YWRtaW46UGFzc3cwcmQ=" -k https://9.30.160.68:9444/rest/bpm/wle/v1/systems
  
  2. You can execute a wsadmin command in Script. The wsadmin command is running against the BPM server associated to the Stage BPM configuration. For example,
  
  ssh AdminTask.BPMSetEnvironmentVariable('[-containerAcronym ${PROCESSAPP_ACRONYM} -containerSnapshotAcronym ${SNAPSHOT_ACRONYM} -containerTrackAcronym Main -environmentVariableName TEST_KEY -environmentVariableValue 8899]')
  
  This Script first logon BPM server using ssh, then execute the wsadmin commmand there to update the BPM environment variable. The format of the Script to call wsadmin command is **ssh** + space + **wsadmin command**.

### Script Supported Parameters
  
  Keter supports below parameters in Script.
  
  ${PIPELINE_NAME}
  ${PIPELINE_ID}
  ${STAGE_NAME}
  ${STEP_NAME}
  ${BUILD_ID}
  ${BUILD_REPORT_URL}
  ${PROCESSAPP_ACRONYM}
  ${SNAPSHOT_ACRONYM}
	
	
[pipeline_create_script]: ../images/pipeline/pipeline_create_script.png
[pipeline_script_result]: ../images/pipeline/pipeline_script_result.png 