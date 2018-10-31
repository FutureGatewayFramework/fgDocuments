# Scheduled Tasks

## Design
|Item|Description|
|---|---|
|Feature name|ScheduledTasks|
|Impacted areas|fgdb, fgAPIServer, APIServerDaemon, APISpecs|
|Abstract|This feature comes as the answer of the RQ6 of the EOSC-hub GEOSS TS. The requirement foresees the execution of small amount of code triggered by events, like AWS’ lambdas.<br>As natural extension, this feature provides a wider range of configuration options adding to the FG system a complete set of scheduling options ranging from the CRON style executions to Task/Application dependency|
|Solution|It uses as_queue STATUS=(CRON\|BOOK\|LAMBDA); the loop to submit tasks as to be changed. In case of CRON/BOOK/LAMBDA statuses further info is needed in order to check if the task has to be placed in the submit queue or not. This can be accomplished by a new table: task_rules having columns:<br>```task_id (link to the task)<br>cron_rule (a string that works exactly like cron)<br>dep_app_id (execution depends from execution of this app)<br>dep_task_id (dependant task_id, queued for execution only if = to dep_task_status)<br>dep_task_status (status that triggers task for execution)<br>dep_task_sandbox (IOSandbox of the dependant task)<br>exec_at (Datetime for execution >=)<br>app_id<br>lambda_evt (task triggered if the specified signal is present in the task queue as LAMBDA command)```<br>cron_rule, dep_task_id and exec_at are not mutually exclusive each other and for multiple selection FG uses 'AND' condition. Field "application" is mutually exclusive with task. At first execution the specified application will be executed and "task" value overwritten with: { "id": <task_id>, "status": "DONE" } and "application" will be set to null. This implements INFRA applications<br><br>Task definition have to deal with this new scheduling possibility with a new input json field:<br>```"scheduling": {<br>"cron": "12 0 * * *",<br>"task": {"id": 145,<br>"status": "DONE"},<br>"application" : {"id": 20},<br>"exec_at": "Tue 25 May 2018 - 15:55:"<br>}```
|Issues/Notes|Specifying application Id in scheduling fields dep_task_id and dep_task_status should be NULL and eventually ignored by the logic until the specified application has been submitted. Once the application has been executed dep_task_id and dep_task_status==’DONE’ will be filled and then used by next APIServerDaemon loops.|

## Implementation

|Item|Description|
|---|---|


## Tests and Release
…






