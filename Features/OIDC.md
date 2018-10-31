# OIDC
OpenId Connect support for API server (fgAPIServer)

## Design
|Item|Description|
|---|---|
|Feature name|OIDC|
|Impacted areas|fgapiserver|
|Abstract|FutureGateway currently supports OIDC only by the PTV module. This feature allows the APIServer to directly manage OIDC authentication.|
|Solution|FlaskOIDC allows to registrer the APIServer as a service provider.<br>Tests have been made allowing to login, register the user and then use the tokens to use FG APIs|
|Issues/Notes|It is not yet clear how to link this with an existing portal who already manages OIDC authN.|

## Implementation

|Item|Description|
|---|---|


## Tests and Release
…






