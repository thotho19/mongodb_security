### Really, never do so. No authentication means inviting everyone out there to enter your databases, seize everything and potentially ransom you for your data.

## User Administrator Procedures
1. Start MongoDB without access control. 
 ```
mongod --port 27017 --dbpath /var/lib/mongodb
```
2. Connect to the instance.
  ```
  mongo --port 27017
```
3.  Create the user administrator.
```
use admin
db.createUser(
  {
    user: "myUserAdmin",
    pwd: passwordPrompt(), // or cleartext password
    roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
  }
)
```

4. Configurationn and Re-start the MongoDB instance with access control. <br>
config
```
1- C:\Program Files\MongoDB\Server\4.4\bin -> open mongodb.cfg file -> seek for security -> eanble the security 
2- security:
    authorization: enabled
3- save and exit
```
Restart
```
Control Panel -> administrative Tools -> services -> seek for MongoDB Server(MongoDB) -> Restart the service
```
5. Connect and authenticate as the user administrator.
```
mongo --port 27017  --authenticationDatabase "admin" -u "myUserAdmin" -p "myPassword"
```
Usefell commands
|command | the value |
|----------|----------|
db.dropUser("mynewuser") | drops the administrator user from the database(disable security is required)

