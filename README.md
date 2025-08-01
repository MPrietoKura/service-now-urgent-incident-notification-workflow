# service-now-urgent-incident-notification-workflow

### <ins>System Overview:</ins><br/>
This incident notification system has been designed to ensure users in the Network Operations group receive Critical Incident assignment notifications via email. It triggers an emailed notification, following the creation of a new Network incident record with Priority level 1-Critical, or Urgency level 1-High and Impact level 1-High.

### <ins>Implementation Steps:<ins/><br/>
The pre-existing workflow was not configured correctly. It's only triggering conditions were:<br/>
Urgency is 1-High (This does not necessarily trigger Priority 1-Critical), and<br/> 
Assignment Group is not empty (This allows for ANY Critical incidents to trigger a notification. We want to specify Network incidents.)

Trigger conditions were instead changed to:<br/>
Category is Network, and<br/>
Priority is 1-Critical<br/>
*or*<br/>
Category is Network, and<br/>
Urgency is 1-High AND Impact is 1-High

Following the trigger, the Action was to send a notification with the Action Input record table set to [incident],<br/>
and the notification referring to Incident Assignment Notification.<br/>

Looking at the notification in question, it was set to send when triggered (by the workflow parameters listed above).<br/>
Notification recipients were set to Group: Networking Operations -which contains 11 group members.<br/>
Additional changes to notification contents included a change of template to get rid of the 'unsubscribe' button, and a dynamic field to include incident number.<br/>
The message read as follows:<br/>
"A new Critical incident has been assigned, Number: ${number}<br/>
Please respond immediately.<br/>
-IT Team"<br/>

After finalizing both the workflow and the notification email, a test incident was created, with category set to Network, and Urgency 1-High and Impact 1-High (i.e. Priority 1-Critical). After submitting this incident, a notification email was generated to all users in the Networking Operations group regarding the critical incident assignment.
