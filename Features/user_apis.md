# User APIs

## Design
|Item|Description|
|---|---|
|Feature name|User APIs|
|Impacted areas|fgAPIServer, APISpecs|
|Abstract|This function allows to setup users, groups and roles values using FutureGateway APIs. This feature was necessary to setup the [rstudio](https://github.com/ricsxn/EOSC-hub/tree/master/T13.3/fgsg/demo_apps/r_studio) use case for EOSC-hub T13.3 activity.
|Solution|Foresee the following API calls:|
||GET `/user/<usrname>` To retrieve user informations|
||POST `/user/<usrname>` To setup user informations|
||PUT `/user/<usrname>` To modify user informations|
||GET `/user/<usrname>/groups` To retrieve group informations|
||POST `/user/<usrname>/groups` To assign a group to the given user|
||GET `/groups` To retrieve installed groups|
||POST `/groups` To setup given groups|
||PUT `/groups` To modify given groups|
||GET `/groups/<group_id>` To retrieve group information|
||PUT `/groups/<group_id>` To modify group information|
||GET `/groups/<group_id>/roles` Show roles associated to the given group|
||DELETE `/groups/<group_id>/roles` Remove associated roles to the given group|
||GET `/groups/<group_id>/apps` Show applications associated to the given group|
||DELETE `/groups/<group_id>/apps` Remove associated applications to the given group|
||GET `/roles` To retrieve installed roles|
||GET/POST `/auth` specifying param `user`, to generate a session token on behalf of given user. Grant user_behalf must be present. Available only with baseline token handling|

## Implementation

|Item|Description|
|---|---|
|Feature name|User APIs|
|Impacted areas|fgAPIServer, APISpecs|
|Branch|user_apis|
|fgapiserver_user.py|Use Flask Blueprint to separate specific user APIs calls to this file|
|fgapiserverdb.py|New database queries to handle users, groups and roles|
|fgapiserver.py|Changes are necessary to handle externalized APIs throug the Blueprint mechanism|

## Tests and Release
|Item|Description|
|---|---|
|tests/test_fgapiserver.py|New unit and functionalt tests added for this feature|
|tests/MySQLdb.py|New database queries to simulate users, groups and roles handling|






