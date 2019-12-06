# MongooseNode - (for MongoDB, Mongoose document creation)

MongooseNode is a small utility app for creating models dynamically during scripting. Feature updates will include 

## Server - minimum requirements
1. Ubuntu 16.04 LTS (Xenial)
2. Mongoose ^v5.x
3. Node.js v10.17.0 (node -v)
4. npm 6.11.3 (npm --version)

## Installation
```bash
1. Run sudo git clone git@github.com:cosmoarunn/mongoosenode.git  
   - if facing 'permission denied' error, try git clone https://github.com/cosmoarunn/mongoosenode
2. cd mongoosenode
3. Run - `npm install`
```

##MongoDB Installation
mongoosenode uses mongodb and mongoose. If mongodb is not installed visit,
https://docs.mongodb.com/manual/installation/

#Installation instructions:
Mongodb server version 4.2

```bash
1. wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -  
   - the operation should return OK
2. sudo apt-get install gnupg
3. wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
   - the operation should return OK
4. sudo apt-get update
5. sudo service mongod start 
   - Start mongodb 
6. sudo service mongod status
   - verify mongodb started
7. mongo
   - start mongo commandline

#Create MongoDB database with username and password
use mydb
db.createUser(
   {
     user: "yourusername",
     pwd: "yourpassword",
     roles: [ "dbOwner" ]
   }
)

- once done, `quit` mongo shell and either update credentials to file config.js 
 `mongoosenode/config/config.js` 

  (or)

  conncect and use existing database like,
  ```bash
    var config    = require( "./config/config.js"  );
    var MongoNode = require('./src/mongonode')
    var mn = new MongoNode('mongodb://username:password@127.0.0.1:27017/databasename')
  ```


```
Use the Node package manager [npm](https://www.npmjs.com/) to install mongoosenode.

```bash
npm install mongoosenode
```

## Usage

```Node.JS
var MongoNode = require('mongoosenode');

var mn = new MongoNode('mongodb://username:password@127.0.0.1:27017/databasename')
    console.log(mn);

   var db = mn.connectDB().then(async(res) => { 
       try { 
           console.log(res);
        return res;  
       }catch(e) { 
           console.log(e);
       }
    });
   

    var params = {
        //id: ObjectId,
        name: {type : String, default: ''},
        pass: {type : String, default: ''},
        token: {type : String, default: ''},
        secret: {type : String, default: ''},
        updated: { type:Date, default : new Date },
        status: {type: Boolean, default : false },
        admin: {type : Boolean, default : false},
    };


    var model = mn.createModel('User', params ).then(async(res) => { 
        console.log(res);
    });
    
   
   var model = mn.retrieveModel('User','User').then(async(res) => { 
       try { 
           console.log(res);
        return res;  
       }catch(e) { 
           console.log(e);
       }
   })
   
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
File : License.MD 
[MIT](https://arunpanneerselvam.com/licenses/mit/)