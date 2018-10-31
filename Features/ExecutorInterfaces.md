# Executor Interface

## Design
|Item|Description|
|---|---|
|Feature name|ExecutorInterfaces|
|Impacted areas|APIServerDaemon|
|Abstract|Actual ExecutorInterfaces (GridEngine and ToscaIDC) are included inside the APIServerDaemon hard-coding their behaviour inside its code. A more flexible way to manage EIs foresees the development of java classese instanciable dynamically by their class names.<br>Solution	Java allows to specify an ‘interface’ class used as skeleton to develop one or more implementation of this interface. Java also offers the possibility to instantiate classes using their names. Interfaces should be inherited in order to create more sophisticated classes starting from existing EIs|
|Issues/Notes|This changes have strong impacts on the current code.<br>Hardcoded management of GridEngne and ToscaIDC, should be removed and dedicated ExecutorInterface interface implementations should be performed. ToscaIDC the most urgent, while GridEngine should be superseded by two different new EI interface implementations: BareExecutor and SSHExecutor built on top of BareExecutor.<br>By this feature the executor interface can be specified at infrastructure level rather than at application level as actually works. Application level EI (Target) will be maintained and ignored when specified at infrastructure level. A special field (MultiInfra) shall be specified in as_queue.target field in such case.|

## Implementation

|Item|Description|
|---|---|
|Feature name|ExecutorInterfaces|
|Area|APIServerDaemon|
|Branch|ExecutorInterfaces|
|ExecutorInterface.java|Java Interface containing basic functionalities, constants and enums to manage interface implementation in the same way.<br>BareExecutor.java First ExecutorInterface implementation it just executed a specified list of command line statements.<br>SSHExecutor.java	Based on BareExecutor it uses scp/ssh -c “” statements to interact with a remote server.|
|APIServerDaemonProcessCommand.java|Current logic will be managed only by as_queue content ‘target’ and ‘action’ fields; instantiating the EI class using ‘target’ and calling the implemented ‘action’ method. For infrastructure level EIs, when its parameter is specified, ‘target’ has|
|ToscaExecutor.java|Taken from ToscaIDC it will just inherits from ExecutorInterface|

## Tests and Release
…






