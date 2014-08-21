Getting-started-with-Mobile-Data
================================

Getting started with Mobile Data

Información tomada de https://www.ng.bluemix.net/docs/#services/mobiledata/index.html#location


IBM® Mobile Data for Bluemix™ is cloud storage service that provides a native feel for storing mobile data, while the management and implementation of the data store is hidden.

Mobile Data uses security function that is provided by IBM Mobile Application Security for Bluemix. Mobile Application Security is required with Mobile Data.You cannot add or delete the Mobile Application Security service from your Mobile Cloud application.

    Download the SDK. For more information, see Mobile cloud.
    Download a sample: bluelist-mobiledata sample
    Update the application with the following information from your Mobile Cloud application. The following information goes in a properties file in the sample and then gets passed to the initialize method.

    context
        (Android only) The value could be your main Activity class.
    applicationID
        The unique key that is assigned to the Mobile Cloud application that you created on Bluemix.
    applicationRoute
        The route that is assigned to the Mobile Cloud application that you created on Bluemix. 
    applicationSecret
        The security key that is assigned to the Mobile Cloud application that you created on Bluemix.

    Android:

    IBMBluemix.initialize(context, applicationId, applicationSecret, applicationRoute);

    iOS:

    [IBMBluemix initializeWithApplicationId: applicationId andApplicationSecret: applicationSecret andApplicationRoute: applicationRoute]

    JavaScript:

    <script> var setup = { applicationId:'<applicationId>', applicationRoute:'<applicationRoute>', applicationSecret:'<applicationSecret>' } IBMBluemix.initialize(setup); </script>

    Develop your application with the Mobile Cloud Services SDK. For more information, see:
        Android SDK Documentation: Mobile Data
        iOS SDK Documentation: Mobile Data
        JavaScript SDK Documentation: Mobile Data

Mobile Data overview

With Mobile Data, you can store, delete, update, and query objects that are stored in the cloud.
Class extension
You can extend the IBMDataObject class in the Mobile Cloud Services SDK. With this class, you can model a new class by registering the class type and provide getter and setter functions for the class definition. By extending the IBMDataObject class, you have access to the saveInBackground, deleteInBackground, and query functions for working with the data you want to store in the cloud.
Class name restrictions

Class names are restricted to 62 bytes in length and cannot contain any of the following characters: "`˜!@#$%ˆ&*()=+[]{}\|;:'",.<>/?"

IBM and _ prefixes on class names are reserved for use by IBM.
Field name restrictions

Field names cannot contain periods (.) or spaces.
Data viewer
To view the data classes, files, and objects that are stored in the cloud, click the Manage data tab. In this tab, you can also import files, such as videos or JSON database files, for use in the services in your application and then view the content of those files. If you are importing a JSON or CSV file with an existing class, you must create a mapping file. For more information about creating a mapping file, see Importing data.
Data access
You can use a REST URL to interrogate the data classes and content that is stored in the cloud. For more information, see REST API documentation.
File synchronization
With the Mobile Cloud Services SDK, you can embed a special managed directory in your application. Any files that are stored in this managed directory can be monitored and synchronized. The application can share the contents of this managed directory by connecting to Mobile Data with the same application ID and user ID. By sharing the directory contents, different instances of an application can have synchronized copies of the files.
Analytics
The Mobile Data tracks several events to provide insight into the application usage. For a visual display of data, click the Analytics tab. You can also use the REST API to fetch the event data directly.

Totals
    Two totals are listed:

        The number of Mobile Data API calls that were made from client devices in the last 30 days or in the current calendar month.
        The amount of storage that is in use.

OS Distribution
    A breakdown of the Mobile Data API calls that were made based on the type of user device.
Time Graphs
    Several graphs display data over time.

        API Activity line graph: Mobile Data API calls made over time, by the type of API call.
        Storage Activity graph: Storage that is used over time, by file or object storage.
        Totals graph: Number of files and objects in storage over time.

Importing data

You can import files, JSON, or tabular data into Mobile Data.

If you are importing files, you can select the files and they are uploaded as is.

If you import data, the data is imported into a class. If you import JSON or tabular data into a new class, the column names come from what you define in the data that you import. If you import data into an existing class, and the column names in your data import file are different from what is already defined in the class, create a mapping file to connect the column names in your import file to the column names in the class. You can specify the mapping file when you import the data to the existing class.

    Get your data in a format that you can import. If you want to import into a class, you can import a JSON file or tabular data in a CSV file.

    Field names cannot contain periods (.) or spaces.
        The JSON format is an array of JSON objects. An example JSON file follows:

        [ { "uid": "919679674", "name": "Tony Mudry", "chain": { "uid": "917916672", "name": "Isabelle Tisserand" } }, { "uid": "952545679", "name": "Anthony Tiangco", "chain": { "uid": "955956672", "name": "Bashar Nabi" } } ]

        In CSV file, the first line contains the column names. Each following line is a record. An example CSV file follows:

        uid,name,managerName 925199672,Danny Resendes,Debbie Fallbacher 907308672,Andreas Dannhauer,Jie Hu

    Optional: If you are importing data into an existing class, define a mapping file. For example, The class for which you already have data is defined in the system with the following attributes:
        serialNo
        name
        reportManager
    In the mapping file, each line is separated into two parts by a colon. Each line is a mapping from a field in the data file you are importing to a field in an existing object. Field names cannot contain periods (.) or spaces.

    uid : serialNo
    name :  name
    chain.name: reportManager

    Import your files and data into Mobile Data.
        From the Bluemix dashboard, go to the Mobile Data instance. Click the Manage Data tab. Drag the files that you want to import into the window.
        Import the data or file. To import data:
            To import to a new class, enter a new name for the Class name.
            To import to an existing class, choose a class from the Import to class field. If you defined a mapping file to define how the field names in the file you are importing map to the data that already exists for the class, choose the Mapping file.
        To import a file:
            Choose the file that you want to upload and click Import.

After you import the data, the data is displayed in the Manage Data tab. If you uploaded data, it is displayed in the Data Classes section under the class name that you defined when you imported the data. If you uploaded a file, it is displayed in the Files section.
File Sync plug-in

You can synchronize files for mobile applications through the File Sync plug-in. Many applications might use data that is naturally represented as files.
With the IBMDataFile and IBMDataFileSystem classes in the Mobile Cloud Services SDK, you can store and retrieve file data in the cloud.
Displays local copies of files that are being synchronized in the cloud with remote copies of those files.

All operations in File Sync are done within a usage context that is defined by the application ID and a secondary ID that can further distinguish between instances of an application. For example, this secondary ID can be a user name. File Sync uses the APPID and secondary ID as a unique key to identify individual managed directories. With these unique keys, you can group files together for synchronization and identify which files are shared across devices.

By default, you have full control of when to store and retrieve files with the cloud through the IBMDataFile class. File Sync automatically uses the usage context to store the file in the managed directory. You can use the IBMDataFileSystem class to synchronize the contents of this directory with the cloud. If you choose to use the optional "live" mode for File Sync, the service automatically detects changes to the managed directory and synchronizes with the cloud periodically. In this mode, you can use the IBMDataFileSystem class to get the location of the managed directory and then use standard file operations to store files in the managed directory. File Sync synchronizes the contents of the directory to the cloud for you.
Synchronization
Currently, File Sync is limited to use a "last write wins" policy when multiple applications are updating the same files. In "last write wins", the device's copy overwrites the copy stored by File Sync. The resulting behavior depends on whether you are running in automatic or manual mode.

Use the IBMDataFileSystem object to get a reference to the managed directory and turn on synchronization. When synchronization is turned on, changes to files are communicated periodically, so the application is less likely to have a stale copy of the file. If the client has not received updates in a while (for example, it has not connected to File Sync for several days), any file that the client changed while disconnected is considered to be a new update and is applied to the File Sync during the next synchronization.

If synchronization is turned off, IBMDataFile instances must call the save and fetch methods manually. The last write wins policy is still followed. The last IBMDataFile object to call the save method and reach the server is the object that the server distributes.
Data serialization

IBMDataObject objects can store all of the most common data types.
Supported data types
Table 1. Data typesIBMData Type 	iOS Type 	Android Type 	Example JSON 	Notes
String 	NSString 	String 	

{"name": "value"}

	

Number 	NSNumber 	Number 	

{"like_count": 8675309}

	

Boolean 	NSNumber 	Boolean 	

{"satisfied_customer": true}

	

Date 	NSDate 	Date 	

{"followBegin": {"__type": "Date", "iso": "2014-04-03T23:00:54.272000Z"}}

	Date format (ISO 8601): YYYY-MM-DDThh:mm:ss.ssssssTZD
Location 	CLLocation 	Location 	

{"meetupLocation": {"__type": "Location", "coordinates": [100.0, 0.0], "altitude": 99.0, "speed": 39.1, "horizontalAccuracy": 2.6, "course": 13.9, "time": {"__type": "Date,"iso":"2014-04-03T23:00:54.272000Z" }}}

	

Mandatory fields: coordinates, time

Optional fields:

altitude, speed, horizontalAccuracy, course.
Array 	NSArray 	List 	

{"favoriteParks": ["Yosemite", "Rocky Mountain", "Banff"]}

	The array must contain other types from this table only.
Bytes 	NSData 	byte[] 	

{"binaryObject": {"__type": "Bytes", "base64":"TXkgU3RyaW5nIEFzIEJ5dGVzIQ=="}

	Convert any object into a byte array, and store the bytes in the IBMDataObject object. Then, reconstruct the object from the byte array when you retrieve it from the IBMDataObject object.
Object 	NSDictionary 	

    Map<String, Object>
    JSONObject
    JSONArray

	

{"keyValueObject": {"key1": "value1", "key2":"value2"}}

	The dictionary or map must contain other types from this table only.
Pointer<IBMDataObject> 	IBMDataObject 	IBMDataObject 	

{"homeAddress": { "__type": "Pointer<IBMDataObject>", "className": "Address", "objectId":"4e712e2f-5ff9-420f-ab86-b51b9eb8f3d2"}}

	Under the covers, the IBMDataObject is replaced with a Pointer that references its objectId. When the IBMDataObject is retrieved, it contains data only if it was found in the local cache. Otherwise, the isDataAvailable() method returns NO/False. Run the fetchIfNecessaryInBackgroundWithCallback() method on the object to ensure the data is available.
Pointer<IBMDataFile> 	IBMDataFile 	IBMDataFile 	

{"profileAvatar": { "__type": "Pointer<IBMDataFIle>", "identifier": "omni://demoUser@IBMSync/9307534f-ceae-4cb6-9fe0-9686e16a447e/ IBMCloud?version=1&path=myImage.jpg"}}

	Similar to IBMDataObject, an IBMDataFile is swapped under the covers with its identifier. When the IBMDataFile is retrieved, it is a handle to the file. Whether the file contents are available, depends on whether IBMFileSync is configured in live mode. If live mode is not configured, file availability depends on whether the file is explicitly downloaded.
Unlisted object types
To store any object type that is not listed in the table, use one of the following options:

    Convert the object to a JSON representation. For example on iOS, most objects can be converted to NSDictionary and NSArray, which are the standard native containers for JSON and are supported in the table. On Android, you can use JSONObject and JSONArray.
    Serialize the object to and from Bytes and then store the Bytes value in the IBMDataObject object.
    Serialize the object to a file, add the file to IBMFileSync and then add the corresponding IBMDataFile to the IBMDataObject.

Reserved object keys
While you can generally associate your objects with any key in an IBMDataObject object, keys that begin two underscores, such as __type are reserved for internal use. You cannot use keys that follow this pattern.
Query predicates (provisional)

You can use the REST Query API to query objects that are stored in Mobile Data. REST query support is provisional and is subject to change.
REST Query API
For more information about the REST Query API, see REST Query API.
Query format
When you use the REST Query API to filter objects from Mobile Data, the query must be provided in a JSON object that includes a predicate:

Query { bookmark (string, optional): Optional. Supplied by data service after delivering first batch. Passing back to data service delivers next batch of results, predicate (string, optional): A string of terms separated by operators conforming to the syntax described in the implementation notes, limit (integer, optional): The number of results to supply for this batch, sortby (array[string], optional): This field can be safely omitted. It exists to support future features }

Predicate JSON format
The following BNF (Backus-Naur Form) defines the format of the JSON to provide for the predicate:

<predicate> ::= <nrpredicate> | <relationpredicate> <nrpredicate> ::= <term> | <op> : Array of <term> | $not : <nrpredicate> <op> ::= $and | $or <term> ::= { <field> : <value> } | { <field> : <rangeValue> } | { <field> : <geoValue> } | <value> ::= <stringORnumber> | <boolean> <stringORnumber> ::= <string> | <number> <rangeValue> ::= { <rangeop> : <stringORnumber> } <rangeop> ::= $lt | $gt | $lte | $gte <geoValue> ::= { $geowithin: { $polygon: [ <x1y1Coordinates>, <x2y1Coordinates>, <x2y2Coordinates>, <x1y2Coordinates>,<x1y1Coordinates> ] }} <relationpredicate> ::= <relationop> :{ from: <nrpredicate>, to: <nr predicate>, relation: <nr predicate>} <relationop> ::= "@from" | "@to"

JSON examples: non-relation predicates

(place=="Austin")
    JSON: {place: "Austin"}
(place == "Austin") && (type == "Restaurant")
    JSON: { $and: [ { place: "Austin" }, {type: "Restaurant"} ] }
(place == " Austin") || (place == "Round Rock")
    JSON: { $or: [ { place: "Austin" }, {place: "Round Rock"} ] }
(place == " Austin") || (place == "Round Rock")) && (type == "Restaurant")
    JSON: { $and: [ $or: [ { place: "Austin" }, {place: "Round Rock"} ], {type: "Restaurant"} ] }
(type == "Restaurant") && (price >= 10) && (price < 20)
    JSON: ​{ $and: [ {type: "Restaurant"}, { price: { $gte: 10 } }, { price: { $lt: 20 } } ] }
(type == "Restaurant") && (cuisine != "indian")
    JSON: ​​{ $and: [ {type: "Restaurant"}, { $not: { cuisine: "indian" } } ] }
(type == "Restaurant") && (location WITHIN bbox)
    JSON:

    ​{ $and: [ {type: "Restaurant"}, { location: { $geowithin: { $polygon : [[x1, y1], [x2, y1], [x2, y2], [x1, y2], [x1, y1]] } } } ] }

    Note: Use two latitudes and two longitudes for the polygon.
All the employees in department D21 who are in Sales and make over 50000 or who are in Marketing and make over 60000:
    JSON:

    { $and: [ {departmentId: "D21"}, { $or: [ { $and: [ { position: "Sales" }, { salary: {$gte: 50000 } } ] }, { $and: [ { position: "Marketing" }, { salary: {$gte: 60000 } } ] } ] } ] }

JSON examples: relation predicates
Consider a system where people can like restaurants. In this system, you might have the following relation queries:

    What are the Mexican restaurants liked by the people who work at Company A?
    Who are the people who work at Company A who like Mexican restaurants?

These queries are different. The first query results in a set of restaurants. The second query results in a set of people. The @from relation operator signifies that the returned result set is the source of the relation. The @to relation operator signifies that the returned result set is the destination of the relation. The query has three components.

    from component: Determines the set of objects from which to begin traversing the relation.
    relation component: Restricts the set of relations to consider.
    to component: Restricts the set of destination objects.

Relation queries are currently restricted:

{ @to: { from: { objectId: the source object ID }, relation: { name: the relation name } to: { } } }

In other words, you can query for and get a list of all objects that are "liked" by an object. You cannot get a list of "Restaurants" that are "liked" by an object.
Location (Beta)

Enhance your mobile application with geofence triggers and create, query, and update points of interest.
Note: Location is in Beta. All associated APIs are provisional, and are subject to change.
Location acquisition
You can get the current location of a device, or start location acquisition in the background.
Triggers

You can configure triggers to run based on position changes, entering or exiting a geofence, and dwelling inside or outside of a geofence.
Points of interest
You can define points of interest with Point, Polygon, and LineString geometries and save, query, update, and delete them with Mobile Data.
Location API
Location APIs are available in the Mobile Cloud Services SDK for Android and iOS. For more information, see:

    Mobile Cloud Services SDK Android developer guide: Location
    Mobile Cloud Services SDK iOS developer guide: Location

GeoJSON geometry objects

Point, Polygon and LineString geometries are serialized according to the GeoJSON Geometry object specification.
Table 2. GeoJSON geometry objectsData Type 	iOS Class 	Android Class 	Example JSON
Geometry 	IBMLineString 	IBMLineString 	

{ "type": "LineString", "coordinates": [ [100.0, 0.0], [101.0, 1.0] ] }

Geometry 	IBMPoint 	IBMPoint 	

{ "type": "Point", "coordinates": [100.0, 0.0] }

Geometry 	IBMPolygon 	IBMPolygon 	No holes:

{ "type": "Polygon", "coordinates": [ [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ] ] }

With holes:

{ "type": "Polygon", "coordinates": [ [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ], [ [100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2] ] ] }

Troubleshooting Mobile Data

You can work around common problems that you might encounter with the Mobile Data.

    Problem: Google Chrome warns you that the demo.zip file is not commonly downloaded and might be dangerous.

    Solution: You can ignore this warning and choose to keep the file.
    Problem: R cannot be resolved to a variable.
    Solutions:
        In ADT, click Project > Clean..
        Eclipse might automatically organize your imports by importing Android.r. Erase these imports and import com.ibm.mobile.services.data.demo.R

