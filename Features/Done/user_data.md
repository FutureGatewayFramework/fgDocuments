# UserData
This feature allows to associate at FutureGateway' users level.
Data records have the same structure of the tasks' user_data.
APIs to store, retrieve, modify and delete user data are handled by the fgapiserver_ugr.py module.
The feature structure is very simple and implies one database patch from v0.0.12b to v0.0.13.

# Impacts
Only fgdb and fgAPIServer components are affected by this feature

# Notes
Under this feature first changes towards the python3 compatibility have been done
