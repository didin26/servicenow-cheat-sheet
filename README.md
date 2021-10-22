# ServiceNow Cheat Sheet

## Content
[Encrypter](https://github.com/didin26/servicenow-cheat-sheet/blob/main/README.md#encrypter), [OR Condition](https://github.com/didin26/servicenow-cheat-sheet/blob/main/README.md#or-condition), [Switch Case](https://github.com/didin26/servicenow-cheat-sheet/blob/main/README.md#switch-case), [setWorkFlow(false)](https://github.com/didin26/servicenow-cheat-sheet/blob/main/README.md#setworkflow)

## Encrypter
    var sys_id = '99d9bb41-1234-5678-9def-a934646209fb';
    
    var gr = new GlideRecord('u_table_name');
    gr.addQuery('sys_id', sys_id);
    gr.query();
    if(gr.next()){ 

      var Encrypter = new GlideEncrypter();
        var dcrypt_cls = Encrypter.decrypt(gr.u_client_secret);

        gs.print(dcrypt_cls);

    } 

## OR Condition
    var sys_id = '99d9bb41-1234-5678-9def-a934646209fb';
    
    var parent_task = new GlideRecord('u_table_name');
    parent_task.addQuery('sys_id', sys_id);
    var cond = parent_task.addQuery('short_description','Install A Service(s)');
    cond.addOrCondition('short_description','Install B Service(s)');
    cond.addOrCondition('short_description','Activate A Service(s)');
    cond.addOrCondition('short_description','Activate B Service(s)');
    cond.addOrCondition('short_description','Activate C Service(s)');
    parent_task.query();

## Switch Case
    var state = current.state;

    switch (state.toString()){
      case '2' : {synchRelatedIncidents(current);} break; //assigned
      case '3' : {synchRelatedIncidents(current);} break; //in progress
      case '4' : {pendingRelatedIncidents(current);} break; //pending
      case '5' : {resolveRelatedIncidents(current);} break;	//resolve
      case '6' : {closeRelatedIncidents(current);} break; //closed
      case '7' : {cancelRelatedIncidents(current);} //cancelled
    }

    function synchRelatedIncidents(inc){
      gs.log('Synch Related Incidents Executed');
    }
    ...

## setWorkFlow
function : to disable all business rule run after it.

    var gr = new GlideRecord('u_table_name');
    gr.addQuery('u_customer_name.name','PT. Angin Ribut');
    gr.addQuery('u_customer_uniqueid','001234');
    gr.query();
    while(gr.next() ){

    gr.u_customer_uniqueid = '004321';
    gr.setWorkflow(false);
    gr.update();

    }
