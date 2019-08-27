<p>
  <img src="https://inspetor-assets.s3-sa-east-1.amazonaws.com/images/inspetor-logo.png" width="200" height="40" alt="Inspetor Logo">
</p>

# Inspetor Antifraud
Antrifraud Inspetor library for iOS.

## Description
Inspetor is an product developed to help your company to avoid fraudulent transactions. This README file should help you to integrate the Inspetor iOS library into your product with a couple steps. 

P.S.: the library was made in Swift and all of the code you'll see here is Swift as well.

## Demo
If you think that this tutorial and whatever you saw 'til now wasn't clear enough, maybe you need some hand's on. Thinking about that, our team builded an Demo App to test our library and you can clone from [here](https://github.com/inspetor/inspetor-ios-demo-app). You'll find all of our tracker requests and how to instantiante our library with the best practices.

## Setup Guide
This is the step-by-step Inspetor integration:

### Library Repositories
The Inspetor iOS Library can be installed through [CocoaPods](https://cocoapod.org). To install all you have to do is follow this steps:

1) Add this to your Podfile: `pod 'Inspetor'` (this uses the latest version).
2) Run `pod install`.

When you import the Inspetor library you will see that you are actually installing more than one library, since the Inspetor iOS Library have some depndencies.

### Library setup
You must provide your config to setup our library. To do that, you need to pass us your configurations through our `setup()` function. All the access to the Inspetor functions is made through our `sharedInstance()` that is available by calling the `Inspetor.sharedInstance()`. There is an example in the code snipet bellow.

You **should** instantiate the Inspetor Library in your application `AppDelegate` in the `didFinishLaunchingWithOptions` function.

```
do {
  try Inspetor.sharedInstance().setup(appId: "123", trackerName: "cool.name", devEnv: true)
} catch TrackerException.requiredConfig(let code, let message) {
  print("code: \(code) - message: \(message)")
} catch {
  print("Error")
}
```

The ***"appId"*** is an unique identifier that the Inspetor Team will provide to you. The ***"trackerName"*** is a name that will help us to find your data in our database and we'll provide you with a couple of them. The ***"devEnv"*** is a boolean statement that you set to indicate that your are testing the library (development enviroment). It's set to false by default.

The Inspetor `setup()` function can throw an error if you pass us an invalid appId or/and nameTracker. Because of that always double check if the configuration your are passing is the right one.

P.S: always remenber to import the library. You can do that using the following code: `import Inspetor`

### Library Calls
If you've already read the [general Inspetor files](https://inspetor.github.io/docs-frontend), you should be aware of all of Inspetor requests and collection functions.

Here we will show you some details to be aware in you are calling the Inspetor tracking functions.

All of out *track functions* can throw exceptions, but the only exception they will through is if you forget to configure the Inspetor Library before calling one of them. Because of that the Inspetor class have a function called `isConfigured()` that returns a boolean saying if you have configured or not the Inspetor Library. We recommend that when you call any of our tracking functions you check if the Inspetor Library is configured. Here is an example on how to do that:

```
if (Inspetor.sharedInstance().isConfigured()) {
    try! Inspetor.sharedInstance().trackScreenView(screenName: "The name of the screen")
}
```

#### TrackScreenView
Different from the Inspetor Javascript Library the track of user pageviews (screenview) is not done automatically. You need to add the function `trackPageView` on every new page.
We **strongly recomend** that you add the functions inside the `viewDidLoad` of every ViewController in your app, since this way we can track the screenview action as soon as it happens. You can see an example of this implementation bellow:

```
override func viewDidLoad() {
  super.viewDidLoad()
  if (Inspetor.sharedInstance().isConfigured()) {
      try! Inspetor.sharedInstance().trackPageView(pageTitle: "login-page")
  }
}
```

### Models
If you are comming from one of our backend libraries you will notice that we do not use models in our frontend libraries. Here you just need to send us the id of the model.

## More Information
For more info you should check the [Inspetor Frontend docs](https://inspetor.github.io/docs-frontend)
