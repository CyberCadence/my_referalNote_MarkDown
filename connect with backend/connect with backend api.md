## APi connect

## ip setup
after creating the server or route, to connect it with the flutter 
here we are connecting the signup route to   flutter
```
app.listen(PORT,"0.0.0.0",function()
{

console.log(`Server started at ${PORT}`);
});
```
just vset up the ip address as 0.0.0.0 to acess from anywhere

## Authservice in flutter
all authentication part is done in this file
firstly create a function which takes the user input of name ,email,password
```
void SignUpUser ( 
{required String name,
required String email,
required String password})async{


}
```
nextly create  a usermodel
```
// ignore_for_file: public_member_api_docs, sort_constructors_first

import 'dart:convert';

  

  

class User {

  

final String id;

final String name;

final String email;

final String password;

final String token;

final String address;

final String type;

  
  

User({ required this.address,required this.id,required this.name,required this.email,required this.password,

required this.token,required this.type});

  
  

Map<String, dynamic> toMap() {

return <String, dynamic>{

'_id': id,

'name': name,

'email': email,

'password': password,

'token': token,

'address': address,

'type': type,

};

}

  

factory User.fromMap(Map<String, dynamic> map) {

return User(

id: map['_id'] as String,

name: map['name'] as String,

email: map['email'] as String,

password: map['password'] as String,

token: map['token'] as String,

address: map['address'] as String,

type: map['type'] as String,

);

}

  

String toJson() => json.encode(toMap());

  

factory User.fromJson(String source) => User.fromMap(json.decode(source) as Map<String, dynamic>);

}
```

after creating json serialisation for user model class
 then in Authservice.dart file
 with the help of htttp package ,create a post request to server before that we are creating a user model in authservice file inside a try catch block
 ```
 User user=User(address: 'address', id: ' ', name: name, email: email, password: password, token: 'token', type: 'type');
```



then create a post request also inorder to acess the localhost in  android ,we need to specify the ip address so creata url with ip address & routes of url

String Urii='http://111.92.81.152:3000';

```
class AuthService{

void SignUpUser ( {required String name,required String email,required String password})async{

  

try {

User user=User(address: 'address', id: ' ', name: name, email: email, password: password, token: 'token', type: 'type');

  

http.Response res= await http.post(Uri.parse('$Urii/api/signup'),body:

user.toJson()

,headers: <String,String>{

'Content-Type':'application/json;charset=UTF-8' // as we used middleware as app.json() we need to use to the header

}

);

  
  
  

} catch (e) {

}
```

