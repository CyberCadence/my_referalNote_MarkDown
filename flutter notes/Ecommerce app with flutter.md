## setup server
* install node
* setup project with node by
* npm init
* folder structure                           backend=> src=>server.js
* set entrypoint as src/server.js
then inside package.json
```

"scripts": {

"test": "echo \"Error: no test specified\" && exit 1",

"start": "node src/server.js",

"dev": "nodemon src/server.js"

},
```
then add express,nodemon
* open a local port in 5000
* create a mongodb and create it and connect with  help of mongoose
```
  

const express=require('express');

const app=express();

const PORT=5000;

const mongoose=require('mongoose');

const mongoDB='mongodb+srv://user1:user1@cluster0.s2wcd4k.mongodb.net/?retryWrites=true&w=majority';

mongoose.connect(mongoDB).then(function(){

  

app.get('/',function(req,res){

res.send('ecomerce started');

});

});


app.listen(PORT,function(){

console.log(`server started at port ${PORT} `);

});
```



## create a usermodel and schema 
initialy we are a creating usermodel ,for that we need to create a schema
schema means a model of json data
```
const { Schema, model } = require('mongoose');
```

above code will only get Schema and model property from mongoose

nextly we are creating a userschema for usermodel
```

const userSchema = new Schema({

  
userid: { type: String, unique: true },

  
fullname: { type: String },

email: { type: String, unique: true },

password: { type: String }, phone: { type: String, unique:true },

address: { type: String },

Country: { type: String }, city: { type: String }, pincode: { type: String },

addeddate: { type: Date, default: Date.now }
}

```
afterv creating a userschema ,now we are creating  model 
```

const userModel = model("User", userSchema);
```



then export the current usermodel file with 
```
  

module.exports=userModel;
```



## Creation of routes files
```
const routes=require('express').Router();

const userModel=require('./../models/userModel');
```
now create a route file for creating a user


```
  

routes.post('/create acoount',async function(req,res){

  
  

req.body;

  
  

});
```

in above code the 'req',will contain all the data submitted by the user ,so by getting req.body  ,will contain all data, but  the data is in json data but api wont understand the json format, so inorder to understand the json data need to add a npm package called body parser.

```
npm install body parser
```


after installing body parser ,need to give acess for bodyparser to use inside  express(),inside server.js

```
  

const bodyParser=require('body-parser');

  

app.use(bodyParser.json);

app.use(bodyParser.urlencoded({extended:false}));
```
then inside routes.js file
```
const Userdata = req.body;

//storing the json file in to a variable

	const newUser= new userModel(Userdata); 
	
	
	//                              
            creating a new user model which takes map as input,as req.body contains json file , we dont need to give data seperatly




await newUSer.save(function(err){

if(err){
res.send({sucess:false,error:err});


}else 
{
res.send({sucess:true,data: newUser});

}



});

```
after importing file in server.js
```
const userroutes=require('./routes/routes');

app.use('/api/user',userroutes); // now routes willl be created inside api/user/ routes
```

test the routed file with help of postman by sendiung a json data of model object,

## password encryption
while we sent data of create user, password of new user need to be encrypted for that we need to use bcrypt package
```
npm install bcrypt
```

after getting bcrypt require it in server.js
```
const bcrypt=require('bcrypt');
```
then we are storing the password data of the req inside a variable

```
const password= userData.password;
```
then using bcrypt package
```
const salt=await bcrypt.genSalt(10);
```

the above bcrypt.gensalt(10) will convert the given password string in to 10  different type of ways, more the number ,more will be comple the encryption also will take time
```
const hashedpassword= await bcrypt.hash(password,salt)
```
then we are encrypting the password and storing inside a varriable 
```
userData.password=hashedpassword;
```

then encrypted password is stored in to body of req


complete encryption of password steps below
```
//encryption of password

  

const password= userData.password;

const salt=await bcrypt.genSalt(10);

const hashedpassword= await bcrypt.hash(password,salt)

userData.password=hashedpassword;
```
 ==these should be done before assigning the jsonvalue to the new object  ==,
 
 that is  const newUser=new userModel(userData);

## database name change
```
const mongoDB = 'mongodb+srv://user1:user1@cluster0.s2wcd4k.mongodb.net/?retryWrites=true&w=majority';
```
to
```
const mongoDB = 'mongodb+srv://user1:user1@cluster0.s2wcd4k.mongodb.net/newname?retryWrites=true&w=majority';
```
database name change can be done by providing a name infront of ?

