# service-now-urgent-incident-notification-workflow

### <ins>System Overview:</ins><br/>
This incident notification system has been designed to ensure users in the Network Operations group receive Critical Incident assignment notifications via email. It triggers an emailed notification, following the creation of a new Network incident record with Priority level 1-Critical, or Urgency level 1-High and Impact level 1-High.

### <ins>Implementation Steps:<ins/><br/>
The pre-existing workflow was not configured correctly. It's only triggering conditions were:<br/>
Urgency is 1-High (This does not necessarily trigger Priority 1-Critical), and<br/> 
Assignment Group is not empty (This allows for ANY Critical incidents to trigger a notification. We want to specify Network incidents.)

<img width="1405" height="703" alt="Original Workflow" src="https://github.com/user-attachments/assets/21cfb258-85d7-4112-8b1c-e5244dcd5753" />



Trigger conditions were instead changed to:<br/>
Category is Network, and<br/>
Priority is 1-Critical<br/>
*or*<br/>
Category is Network, and<br/>
Urgency is 1-High AND Impact is 1-High

<img width="1917" height="887" alt="Fixed Workflow" src="https://github.com/user-attachments/assets/cdf84f76-d882-47fc-bed8-a76ea8c40121" />

Following the trigger, the Action was to send a notification with the Action Input record table set to [incident],<br/>
and the notification referring to Incident Assignment Notification.<br/>
<img width="585" height="432" alt="Action" src="https://github.com/user-attachments/assets/969d973d-4f92-4da6-8485-409032f7f4c7" />

Looking at the notification in question, it was set to send when triggered (by the workflow parameters listed above).<br/>
Notification recipients were set to Group: Networking Operations -which contains 11 group members.<br/>
Additional changes to notification contents included a change of template to get rid of the 'unsubscribe' button, and a dynamic field to include incident number.<br/>
<br/>
The message read as follows:<br/>
"A new Critical incident has been assigned, Number: ${number}<br/>
Please respond immediately.<br/>
-IT Team"<br/>
<img width="1892" height="840" alt="Notification" src="https://github.com/user-attachments/assets/6919d34d-35cd-42df-810e-00e1e6c91a3f" />

After finalizing both the workflow and the notification email, a test incident was created, with category set to Network, and Urgency 1-High and Impact 1-High (i.e. Priority 1-Critical). After submitting this incident, a notification email was generated to all users in the Networking Operations group regarding the critical incident assignment.

### <ins>Architecture Diagram:<ins/><br/>

<img width="1081" height="641" alt="Diagram" src="https://github.com/user-attachments/assets/2a2bc11b-b60a-4194-9317-bb3fedecf3fa" />
<br/>

### <ins>AI Scenario Analysis:<ins/><br/>
In a scenario where AI agents could globally orchestrate incident resolution times, according to engineer expertise and workload, and time zone availability, I imagine the AI Agent workflow would look something like Uber, where instead of a rider reaching a destination by choosing a driver- according to proximity and vehicle specs, an incident reaches a resolution by choosing an engineer- according to time zone availability (proximity) and engineer seniority/expertise (vehicle specs). The same way Uber knows to queue rides because a driver cannot handle multiple rides simultaneously, this AI agent will queue incidents to ease workflow. If, like Uber, the AI agent sees that an engineer has not picked up an incident in a certain amount of time, it will confirm with the engineer that it is being reassigned to another engineer more available. And finally, in lieu of a rating system that punishes or rewards drivers with more/better drives, the AI agent can discern which engineers are more reliably able to resolve critical incident cases.


