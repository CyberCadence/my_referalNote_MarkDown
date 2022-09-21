# App life cycle in flutter

## definition
app life cycle determines wheather the app is running,is it running in the background or app terminated (app termination niot possible in ios)


## different type of app states
*  Inactive state - when the app does not have any user input( occur only in ios )
* paused state - app is running in the background
* resume state-app is visible and running after the pause state
*  detached state(suspended state )-  only in android state


we need to create a function named<mark> didappstatechanged</mark>
this method work with both stateful and stateless widget,good with stateful widget
also this method works well when we implement  <mark>widgetbindingobserverinteface </mark>


```
  

class MyApp extends StatefulWidget {

const MyApp({Key? key}) : super(key: key);

  

@override

State<MyApp> createState() => _MyAppState();

}

class _MyAppState extends State<MyApp> with WidgetsBindingObserver {

// ##didapplifecyclechanged
@override

Widget build(BuildContext context) {

return MaterialApp(

title: 'Flutter Demo',

theme: ThemeData(

primarySwatch: Colors.blue,
),
);
}
}
```
after this we need to create a listener as soon as the class is initialised
so we we create observer inside a init method and dispose observer,we cant have dispose method in stateless widget this is why app life cycle is good with stateful widget

```
class MyApp extends StatefulWidget {

const MyApp({Key? key}) : super(key: key);

@override

State<MyApp> createState() => _MyAppState();

}

class _MyAppState extends State<MyApp> with WidgetsBindingObserver {

// ##didapplifecyclechanged

  

@override

void initState() {

super.initState();

WidgetsBinding.instance.addObserver(this); //this means observer active for current class only

}

  

@override

void dispose() {

super.dispose();

WidgetsBinding.instance.removeObserver(this);

}

  

@override

Widget build(BuildContext context) {

return MaterialApp(

title: 'Flutter Demo',

theme: ThemeData(

primarySwatch: Colors.blue,

),

);

}

}
```

nextly add this method    
```

void didChangeAppLifecycleState(AppLifecycleState state) {

super.didChangeAppLifecycleState(state);

print(state);

}
```

now this state variable will show the current state of the app