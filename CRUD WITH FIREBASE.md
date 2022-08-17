## GET FILES FROM FIREBASE


CREATE A INSTANCE OF FIREBASE FOR EASYT ACESSING
```
FirebaseFirestore _firestore= FirebaseFirestore.instance;

```

in firebase files are stored as collections ,inside colllections there will be documents with documnet id, thewse document will contains datas as map
```
getdata() async {

  
  
  

 

DocumentSnapshot snapshot = await FirebaseFirestore.instance

.collection("product")

.doc("qg5BxItXQS13pOlpHEA4")

.get();

print(snapshot.data());

  

}
```
by above code we can acess the specific document inside a collection

```
QuerySnapshot snapshott= await _firestore.collection('users').get();
```
by above code we can acess the entire collection inside the 'users' named colllection,

## add files

in firebase data is been stored as Map
```
Map<String,dynamic> usermap={

  

'username':"dilse",'age':"22"

  

};

_firestore.collection('users').add(usermap);

print('messege added');

  

}
```

above code will add new data to collection 'users' with unique id created by firebase 
```

_firestore.collection('users').doc('myid').set(usermap);
```

above will add   new data with id provided by the user
## update data
```
_firestore.collection('users').doc('myid').update({

'age':'33'

});
```
