# Feature Template
Each feature is described and tracked accordingly to a precise schema aiming to track the FG Feature from its initial design up to its final implementation and testing. Each phase foresees a different template schema to be filled by the FG Architect/Developer. These different schemas are related to the different level of implementation of the feature:

* Design
* Development
* Tests and release

## Implementation plan
Shortly describes the feature, why it has been created, the problem it solves, how it will be implemented and which impacts it has on top of FG modules.

|Field|Value|Description|
|---|---|---|
|Feature name|	<mnemonic name>|Nick name of the feature preferably used to label the dedicated feature’ Git branch.|
Impacted areas|<list of FG modules>|FutureGateway modules impacted by this change.|
Abstract|<feature aims and scope>|What the new feature does, which problem solves, how its implementation improves the current release.|
Solution|<descriptive text>|Description of the implementation tests performed and issues eventually arose.|
Issues/Notes|<descriptive text>||

## Development
To track any development change, for each impacted FG component, the following template have to be filled:

|Field|Value|Description|
|---|---|---|
|Feature name|<mnemonic name>|Name assigned in the related design template.|
|Area|<area name>|One of the FG impacted components: fgdb, fgapiserver,…|
Branch|<branch_name>|Name of the branch holding depicted changes.|
|<source file name>|<changes >|Describe changes in the source code. It is not necessary to specifty exacly code changes; the use of keywords and pseudo-code is even preferable. The used keywords should be used to track these changes inside the source file (variable names, remarks, etc.).|

Fields: Area, Branch and <source file name> can be repeated for each impacted area/branch/source.

## Tests and Release
Following template have to be used to perform test the feature functionality

|Field|Value|Description|
|---|---|---|
|Feature name|<mnemonic name>|Name assigned in the related design template.|
|<test name>|Descriptive name for the test case.|
|<action>|<expected result>|<result status>|
|<results>|Status = PASSED/FAILED|
Results have to be filled in case they do not match with the specified expected results.

Fields <test name> and associated <action>s can be repeated for all tests.
Only when all tests cases are in PASSED status, all related feature branches can be committed.
