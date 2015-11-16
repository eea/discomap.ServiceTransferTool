# discomap.ServiceTransferTool
Transfer tool
This tool allows migrating services from one server to another. 
	
Environment requirements
The tool is developped to run under Arcgis 10.2 (Python2.7)
The ArcGIS services sources must be placed in a path according to the following structure: \\server_name\x\arcgisserver\...
The user that executes the tool or/and the user from ArcGIS Server that uses the geoprocessing service, should be able to access to each network path where the service’s sources are placed in order to copy them. Also needs permission to store in somewhere a copy of the services. 
The server where the geoprocessing service is displayed or the one where the tool is executed requires space to store a copy of all the sources of the migrated services.

Installation
ArcGis tool is placed in the toolbox called “TransferServices”. There is located the “Transfer Services between Servers” tool.


Functionality
The script uses twelve parameters. Only one of them is optional:
[1] Input Server Name (string)
The host name of the origin server. Typically a single name or fully qualified server, such as myServer.esri.com
[2] Input Server Port (string)
The port number for the origin ArcGIS Server. Typically this is 6080. If you have a web adapter installed with your GIS Server and have the REST Admin enabled you can connect using the web servers port number.
[3] Input Server User (long)
Administrative username.
[4] Input Server Password (string) 
Administrative password.
[5] Service Type (string)
The type of the service to migrate.
[6] Services (Multiple Value)
One or more services to perform an action on. The tool will autopopulate with a list of services when the first 5 parameters are entered. Service names must be provided in the <ServiceName>.<ServiceType> style.
[7] Output Server Name (string)
The host name of the end server. Typically a single name or fully qualified server, such as myServer.esri.com
[8] Output Server Port (long)
The port number for the final ArcGIS Server. Typically this is 6080. If you have a web adapter installed with your GIS Server and have the REST Admin enabled you can connect using the web servers port number.
[9] Output Server User (string)
Administrative username.
[10] Output Server Password (string)
Administrative password.
[11] (optional) Folder (string)
A destination folder different from the original/s one/s can be introduced.
[12] sysTemp (string)
A folder where the services sources are going to be stored.

The script uses the username and the password to connect to the original and destination server with a generatetoken action. After accessing to the original server, all services are listed. When the user selects the services to migrate and fills all the parameters the process starts.
Firstly, a copy of the selected service's sources is made, this copy is placed in the sysTemp path. After that, all the service's properties are read and modified in the copy done in the sysTemp path. 
The tool checks if in the destination server exists a folder with the same name as the original one, or with the name defined as a parameter. If not the folder is created. Once the folder is created the tool publish the service using the copied sources. 
Is important to notice that if the service has special permission (cannot access to it everyone), also this permission is set in the new service. The procedure is: 
-	In case the role exists in the destination server: Only the access permission is assigned to the service.
-	In case the role does not exists in the destination server: The role is created with the same characteristics of the original one, the role privileges are assigned to the role and the users within that role are transferred.
Note: When the users are copied from one server to another it is not possible to transfer the password of the user so is set by default.
