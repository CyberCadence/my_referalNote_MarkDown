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

## login page setup
create a new route for login page
```
router.post("/login", async function(req, res) {}
```


save the email and password value inside the req.body inside a variable
```
const email = req.body.email;

const password = req.body.password;
```

 
```
const foundUser = await UserModel.findOne({ email: email });// search for email value provided by user in req inside in mongodb 

if(!foundUser) {    // if email is not found  it will return this messsage

res.json({ success: false, error: "user-not-found" });

return;

}
```

```
  

const correctPassword = await bcrypt.compare(password, foundUser.password); 
      // will compare the password provided by user inside req.body with the password of the user saved inside db whenever the above email condition is met true
      
if(!correctPassword) {

res.json({ success: false, error: "incorrect-password" });

return;

}
```


if both email and password is met true condition ,returns this

```
res.json({ success: true, data: foundUser });
```

complete code of login route
```
router.post("/login", async function(req, res) {

const email = req.body.email;

const password = req.body.password;

  

const foundUser = await UserModel.findOne({ email: email });

if(!foundUser) {

res.json({ success: false, error: "user-not-found" });

return;

}

  

const correctPassword = await bcrypt.compare(password, foundUser.password);

if(!correctPassword) {

res.json({ success: false, error: "incorrect-password" });

return;

}

  

res.json({ success: true, data: foundUser });

});
```

## new route with userid



```
  

router.get('/:userid',async function(req,res){

  

const userid= req.params.userid;

const foundUser= await UserModel.findOne({userid:userid});

if(!foundUser){

  

res.json({success:false,error:"user not found"});

return;

  

}

  

res.json({success:true,data:foundUser});

  
  

});
```

## product model creation


alike above ,now we have toi create the product model,product routes also


```
const{Schema,model} = require('mongoose');

  
  

const productSchema= new Schema({

  

productid:{type:String,required:true,unique:true},

  

title:{type:String,required:true},

description:{type:String,default:""},styles:{type:Array,default:[]},

  

price:{type:Number,required:true},

images:{type:Array,default:[]},

createdOn:{type:Date,default:Date.now}

});

  

const productModel=model("Product",productSchema);

module.exports=productModel;
```


## Product route page setup
### create product page setup
```
const router=require('express').Router();

const ProductModel=require('./../models/product_model');

  
router.post("/addproduct",async function(req,res){

  
const ProductData=req.body;

const newProduct= new ProductModel(ProductData);

await newProduct.save(function(err){

if(err){

  res.json({success:false,error:err});

return;

}

res.json({success:true,data:newProduct});

});

});

  
module.exports=router;
```

aslike other routes import it in server.js 
```
const CategoryRoute=require('./routes/categoryroute');

app.use("/api/category",CategoryRoute);
```

### get all category
inorder to list all categories ,create a new route ,then

by using CategoryModel.find( ) function alone we can show all of the categories for error handling we are using here .exec( ) execute function hich contains a callback of error and docs,the docs will hold all values
```
router.get('/',async function(req,res){

  
await CategoryModel.find().exec(function(err,categories){

  
if(err){

res.json({success:false,error:err});

}

res.json({success:true,data:categories});

})

});
```


till now we don t know the products & its related category, so inorder to list the product along with the category,
we need to add the category property to the product model

```
category:{type:Schema.Types.ObjectId,ref:"Category"} // "Category" is name provided while creating model
```
add new property to older one 
```
  

const productSchema= new Schema({

  

productid:{type:String,required:true,unique:true},

 category:{type:Schema.Types.ObjectId,ref:"Category"},

  

title:{type:String,required:true},

description:{type:String,default:""},styles:{type:Array,default:[]},

  

price:{type:Number,required:true},

images:{type:Array,default:[]},

createdOn:{type:Date,default:Date.now}

});
```

after creation of category in productmodel, now while adding new products, we need to mention the category id in to the  new products just like below

![[postman get categorydetails.png|500]]
here copy the _id of the particular category  and paste it while creating new product_
![[addproduct with category(postman.png]]
now create a new route for listing all products and also add populate ( ) function and mention the the property so it will now list the product with details 

```
router.get('/',async function(req,res){

  
  

await ProductModel.find().populate('category').exec(function(err,products){

  

if(err){

res.json({success:false,error:err});

}

res.json({success:true,data:products});

  

})

});
```
![[s3.png]]


## delete product by id
```
router.delete('/',async function(req,res){

const productId= req.body.productid

const result= await ProductModel.findOneAndDelete({productid:productId});

if(!result){

  

res.json({success:false,err:'not found'});

return;

}

res.json({success:true,data:result});

  
  

});
```

now delete product by just inputing productid 

## Update data
for updating the existing data we are using put method
```
router.put('/',async function(req,res){

  

const ProductData= req.body;

  
const productid= ProductData.productId;

const result= await ProductModel.findOneAndUpdate({productid:productid},ProductData);

if(!result){

  res.json({success:false,err:"not found data ,can't update"});

}

  res.json({success:true,data:ProductData});

  

});
```


==here in below code ,while we update data  data  we are using product id as a reference because there is no use with the updation of productid so productid of the req.body is used and compared with productid inside the database,then contents need to be updated is stored inside ProductData.==
const result= await ProductModel.findOneAndUpdate({productid:productid},ProductData);

likely update create routes for update inside categoryroute and userroute also
