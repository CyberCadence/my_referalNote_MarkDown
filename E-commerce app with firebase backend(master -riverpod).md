# E-commerce app

## What is Firebase?

Firebase is a Google product that enables developers to build rich, collaborative applications by allowing secure access to databases and other **services directly from the client-side**.


## firebase cli setup
for this project we will be using firebase as backend, we will be setting up firebase wit the help of terminal
if you are not familiar with the cli setup please have a look at my cli setup documentation here 


[Firebase-cli setup docs](https://medium.com/@DILJITH_77/flutterfire-cli-setup-535c8b5d4d96)


* We will be using firebase authentication 
* enable email and password 
* create a firebase database and start it with test mode




## flutter packages needed

```
  cupertino_icons: ^1.0.2
  firebase_core: ^1.14.0 # core
  firebase_auth: ^3.3.12 # for authentication
  cloud_firestore: ^3.1.11 # for database
  firebase_storage: ^10.2.10 #for storage
  flutterfire_ui: ^0.4.0 # for pre-built uis

```

also add flutter_riverpod package for state management



if you are working with ios ,you might get ***podfile error***, you need to uncomment below line
```
platform :ios, '12.0'
```
Also, change the platform in XCode by opening XCode, and opening inside the ios folder the white XCode project file. Change the deployment target to 12.0 inside the project runner and change the deployment info inside Target runner to 12.0.

## Folder structure






