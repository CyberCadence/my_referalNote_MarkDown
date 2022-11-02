## LOCAL NOTIFICATIONS


### INIT
We need to initialize seperately for android and ios ,then we need to combine them both.


For initialize in android 
```
AndroidInitializationSettings androidInitializationSettings=

AndroidInitializationSettings('@mipmap/ic_launcher');
```

the 'mip-mip/ic_launcher ' is the default ap icon path


For IOS
```
DarwinInitializationSettings darwinInitializationSettings=DarwinInitializationSettings(requestAlertPermission: true);
```

nextly combining them we create 
```
InitializationSettings initializationSettings=

InitializationSettings(android:

androidInitializationSettings,

iOS: darwinInitializationSettings);

```

now we need to create a instance of the notificationssettings,as wee need t use it globally we define it outside main function

```
FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin=FlutterLocalNotificationsPlugin();
```

then we initialize the instance inside by
```
flutterLocalNotificationsPlugin.initialize(initializationSettings);
```
after initializing while running app ,ios will ask for permisiion but android wont ask as it may be allowed early

now we initialized notifications
also we need to need to initialize notification details too, for that we follow same process

```
//android

  

AndroidNotificationDetails androidNotificationDetails=

AndroidNotificationDetails('TEST', 'TEST123',

importance: Importance.max,priority: Priority.max);

  

//ios

DarwinNotificationDetails darwinNotificationDetails

=DarwinNotificationDetails(presentAlert: true,);

  
  

NotificationDetails notificationDetails=

NotificationDetails(android:

androidNotificationDetails,iOS: darwinNotificationDetails);

await flutterLocalNotificationsPlugin.show(0, 'sample note', 'this is sample one',

notificationDetails);
```

now call the function on floating action button









