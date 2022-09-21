## Hive
add dependency flutter hive
```
hive_flutter: ^1.1.0
```


 hive docs for ref-   [https://docs.hivedb.dev/#/]
 additinal packages needed are


```
dependencies: 
hive: ^[version]
hive_flutter: ^[version] 

dev_dependencies: 
hive_generator: ^[version]
build_runner: ^[version]
```

for saving files into hive db ,firstly we need to create data model and mark it with annotations to show hive db

```
class Student{
final String name;

final String age;
Student({required this.name,required this.age});}
```

above given is a normal model data but we need to make some changes in data model inorder to write data inside hive, for that we need to have ADAPTERS
## type adapters
Adapters act as a bridge between applicatiuon and hive db, these adapters create the required functions for binding the app and db  for that we need build runner package and it will automatically create the functions in new generated file

```
part'classmodel.g.dart'

@HiveType(typeId: 1)

class Student {

@HiveField(0)

final String name;

@HiveField(1)

final String age;

Student({required this.name,required this.age});

}
```

mention the  unique typeid for the class, so  the  student database can be easily foundout from hive with that unique type id

nextly create hivefield for each parameters with unique numbers
 then run build runner package with following command 
 ```
 flutter packages pub run build_runner watch --use-polling-watcher --delete-conflicting-outputs
```
after creating the generated files 
in main() make it Future function and initialise hive and register the adapter

```
Future< void> main() async{
await Hive.initFlutter();  

if(!Hive.isAdapterRegistered(StudentAdapter().typeId))
/**/studentAdapter in generatedfile**


{
Hive.registerAdapter(StudentAdapter());
}
runApp(const MyApp());

}
```










