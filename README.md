<p>
  <img src="https://inspetor-assets.s3-sa-east-1.amazonaws.com/images/inspetor-logo.png" width="200" height="40" alt="Inspetor Logo">
</p>

# Inspetor Antifraud
Inspetor antifraud SDK for Swift (iOS apps) integrations.

## Description
Inspetor is a product developed to help your company avoid fraudulent transactions. This README file should help you to integrate the Inspetor iOS library into your product with a couple steps. 

P.S.: the library was made in Swift and all of the code you'll see here is in Swift as well.

## Demo App
If you want to see a very simple integration of the library in action you can clone the [inspetor demo app](https://github.com/inspetor/inspetor-ios-demo-app). There you find an implementation on how to setup the library and trigger all tracking actions. Apart from that, you find the best practices when using our library.

## How to use
The Inspetor iOS Library can be installed through [CocoaPods](https://cocoapod.org). To install all you have to do is follow this steps:

1. Add our library to you Podfile (`pod Inspetor`)
1. Run `pod install` command

P.S: When you import the Inspetor library you will see that you are actually installing more than one library, since the Inspetor iOS Library have some dependencies.

## API Docs
You can find more in-depth documentation about our frontend libraries and integrations in general [here](https://inspetor.github.io/docs-frontend).

### Library setup
In order to properly relay information to Inspetor's processing pipeline, you'll need to provide customer-specific authentication credentials:
- App ID (provided by Inspetor)
- Tracker name (provided by Inspetor)

With these, you can instantiate the Inspetor tracking instance. Our integration library instantiates a singleton instance to prevent multiple trackers from being instantiated, which could otherwise result in duplicate or inconsistent data being relayed to Inspetor. Apart from that, the singleton will let you configure the library only once.

The singleton instance is instantiated as follows:

```
do {
  try Inspetor.sharedInstance().setup(appId: "appId", trackerName: "trackerName", devEnv: false)
} catch TrackerException.requiredConfig(let code, let message) {
  print("code: \(code) - message: \(message)")
} catch {
  print("Error")
}
```

Be advised, that this function can throw an exception if you pass an invalid appId or/and trackerName (empty strings or not in the format required).

We **strongly** recommend you instantiate the Inspetor Library in your application `AppDelegate` in the `didFinishLaunchingWithOptions` function, since this way you will configure the library as soon as the app loads enabling you to call the library functions.

All the access to the Inspetor functions is made by calling the `inspetor.sharedInstance()`. 

The parameters passed are the following, in order:

Parameter | Required | Type | Description 
--------- | -------- | ---- | ----------- 
appId           | Yes | String  | An unique identifier that the Inspetor Team will provide to you
trackerName     | Yes | String  | A name that will help us to find your data in our database and we'll provide you with a couple of them
devEnv          | No  | Boolean | Indicates that your are testing the library (development environment), meaning that data is not ready for production. All boolean parameters are `false` by default.

P.S: always remember to import the library using the  `import Inspetor`

### Library Calls
If you've already read the [general Inspetor files](https://inspetor.github.io/docs-frontend), you should be aware of all of Inspetor requests and collection functions.

Here we will show you some details to be aware of if you are calling the Inspetor tracking functions.

All of out *track functions* can throw exceptions, but the only exception they will through is if you forget to configure the Inspetor Library before calling one of them. Because of that the Inspetor class have a function called `isConfigured()` that returns a boolean saying if you have configured or not the Inspetor Library. We recommend that when you call any of our tracking functions you check if the Inspetor Library is configured. Here is an example on how to do that:

```
if (Inspetor.sharedInstance().isConfigured()) {
    try! Inspetor.sharedInstance().trackAccountCreation(accountId: "123")
}
```

#### TrackScreenView
Different from the Inspetor Javascript Library the track of user pageviews (screenview) is not done automatically. You need to add the function `trackPageView` on every new page.
We **strongly recommend** that you add the functions inside the `viewDidLoad` of every ViewController in your app, since this way we can track the pageview/screenview action as soon as it happens. You can see an example of this implementation bellow:

```
override func viewDidLoad() {
  super.viewDidLoad()
  if (Inspetor.sharedInstance().isConfigured()) {
      try! Inspetor.sharedInstance().trackPageView(pageTitle: "login-page")
  }
}
```

### User Location
The Inspetor iOS Library can use the user location to help us provide more accurate results, but it will **never** ask for it. If your app already has access user location the library will automatically capture it, otherwise it won't send the location to us.

### Models
If you are coming from one of our backend libraries you will notice that we do not use models (e.g. Account, Sale) in our frontend libraries. Here you just need to send us the id of the model (e.g. sale ID, account ID).

## More Information
For more info you should check the [Inspetor Frontend docs](https://inspetor.github.io/docs-frontend)
