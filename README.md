<p>
  <img src="https://github.com/inspetor/slate/blob/master/source/images/logo-color.png" width="200" height="40" alt="Inspetor Logo"> </img>
</p>

# Inspetor Antifraud
Antrifraud Inspetor library for Android.

## Description
Inspetor is an product developed to help your company to avoid fraudulent transactions. This README file should help you to integrate the Inspetor iOS library into your product with a couple steps. 

P.S.: the library was made in Swift and all of the code you'll see here is Swift as well.

## Setup Guide
This is the step-by-step Inspetor integration:

### Library Repositories
The Inspetor iOS Library can be installed through [CocoaPods](https://cocoapod.org). To install all you have to do is follow this steps:

1) Add this to your Podfile: `pod 'Inspetor'` (this uses the latest version).
2) Run `pod install`.

When you import the Inspetor library you will see that you are actually installing more than one library, since the Inspetor iOS Library have some depndencies.

### Library setup
You must provide your config to setup our library. To do that, we created a data class called InspetorConfig (duh) and you just have to do something like that:

All the access to the Inspetor functions is made through our **sharedInstance** that is available by calling the `Inspetor.sharedInstance`. But before you can call any of our functions you need to configure the library. To do that all you need is the following code bellow.

You **should** instantiate the Inspetor Library in your application `AppDelegate` in the `didFinishLaunchingWithOptions` function.

```
  Inspetor.sharedInstance.inspetorConfig = InspetorConfig(appId: "cool.name", trackerName: "ID123", devEnv: true)
```

The ***"appId"*** is an unique identifier that the Inspetor Team will provide to you. The ***"trackerName"*** is a name that will help us to find your data in our database and we'll provide you with a couple of them. The ***"devEnv"*** is a boolean statement that you set to indicate that your are testing the library (development enviroment). It's set to false by default.

P.S: always remenber to import the library. You can do that using the following code: `import Inspetor`

### Library Calls
If you've already read the [general Inspetor files](https://inspetor.github.io/docs-frontend), you should be aware of all of Inspetor requests and collection functions.

Here we will show you some details to be aware in you are calling the Inspetor tracking functions.

All of out *track functions* can throw exceptions, but the only exception they will through is if you forget to configure the Inspetor Library before calling one of them. Because of that the Inspetor class have a function called `isConfigured()` that returns a boolean saying if you have configured or not the Inspetor Library. We recommend that when you call any of our tracking functions you check if the Inspetor Library is configured. Here is an example on how to do that:

```
if (Inspetor.isConfigured()) {
    try! Inspetor.sharedInstance.trackAccountCreation(accountId: "123")
}
```

### Models
If you are comming from one of our backend libraries you will notice that we do not use models in our frontend libraries. Here you just need to send us the id of the model.

**For more info you should check the [Inspetor Frontend docs](https://inspetor.github.io/docs-frontend)
