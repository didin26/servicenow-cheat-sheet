<h1>servicenow-cheat-sheet</h1>

# <h2>Content</h2>
<br/>

# <h2>Encrypter</h2>
    var sys_id = '99d9bb41-1234-5678-9def-a934646209fb';
    
    var gr = new GlideRecord('u_table_name');
    gr.addQuery('sys_id', sys_id);
    gr.query();
    if(gr.next()){ 

      var Encrypter = new GlideEncrypter();
        var dcrypt_cls = Encrypter.decrypt(gr.u_client_secret);

        gs.print(dcrypt_cls);

    } 

# <h2>OR Condition</h2>
    var sys_id = '99d9bb41-1234-5678-9def-a934646209fb';
    
    var parent_task = new GlideRecord('pm_project_task');
    parent_task.addQuery('sys_id', sys_id);
    var cond = parent_task.addQuery('short_description','Install A Service(s)');
    cond.addOrCondition('short_description','Install B Service(s)');
    cond.addOrCondition('short_description','Activate A Service(s)');
    cond.addOrCondition('short_description','Activate B Service(s)');
    cond.addOrCondition('short_description','Activate C Service(s)');
    parent_task.query();

# <h2>Switch Case</h2>
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
