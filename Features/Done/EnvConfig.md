# EnvConfig

|Item|Description|
|---|---|
|Feature name|EnvConfig|
|Impacted areas|fgdb, fgAPIServer, APIServerDaemon|
|Abstract|Current FG configuration does not support the use of Environment Variables. This have impacts with the FG installation using Cloud resources especially in the case of Docker containers and related ‘compose’ files.
|Solution|Foresee for each FG component the possibility to fully configure it using environment variables. More efficiently, use environment variables to store the FG node configuration inside the DB as it starts the first time. In this way, configuration should be taken from the environment, but also from the ‘fgdb’ in case of node ‘rebuild’. Each node could be configured just specifying the ‘fgdb’ settings. Other nodes could use the ‘default’ node settings, specified.
|Issues/Notes|This feature allows to centralise the FG configuration in a single place. The FG database will be the central point of reference for the other FG components. This is an important feature for properly handle FG node scalability. More than one APIServer and APIServerDaemon can be used and these will be centrally tracked by fgdb.|

## Implementation

|Item|Description|
|---|---|
|Feature name|EnvConfig|
|Area|fgdb, fgAPIServer|
|Branch|EnvConfig|
|fgapiserver.py|srv\_uuid – Associate a unique id to the running service<br>check\_db\_cfg – Check if the service is registered or not. Registration will be done in case the service is not yet in the database<br>check_db_reg -  Loads the configuration from the DB if any change has been detected<br>flask function @app.before_request has been defined in order to call check_db_cfg at eath API call. This updates configuration settings at run-time (see issue).<br>The overall configuration priority starts from the FG module configuration file, then environment variables and finally registered values in the DB, having the highest priority.<br><br>*Issue* (solved): Not all configuration settings can be handled at run-time. Some values need to restart the service (fgapiver).<br>Solution:|
|fgapiserverconfig.py|FGApiServerConfig now inherits from ‘dict’.<br>Internally values are treated as strings but boolean and integer types are specified in two class vectors named bool_types and int_types holding respectively the boolelan and integer keys.<br>Default structure has been changed and EI configurations now have their own subtree (GridEngine).<br>load_config – Load configuration settings using an input dictionary<br>Environment settings are extracted from the object instance using [] operator by fgapiserver.py|
|fgapiserverdb.py||	
|fgapiserver_db.sql|Two new tables:<br>* srv_registry<br>* srv_config|
|dbpatch/patch_0.0.12.sh|It creates two tables: srv_registry and srv_config; the first keeps track of registered FG services, while the second holds the configuration parameters in the form (key, value).|


## Tests and Release
…






