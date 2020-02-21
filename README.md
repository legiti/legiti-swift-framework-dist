<p>
  <img src="http://files.lgtcdn.net/images/legiti_logo_black.png" width="200" height="55" alt="Legiti Logo">
</p>

# Legiti Antifraud
Legiti antifraud SDK for Swift (iOS apps) integrations.

## Description
Legiti is a product developed to help your company avoid fraudulent transactions. This README file should help you to integrate the Legiti iOS library into your product with a couple steps.

P.S.: the library was made in Swift and all of the code you'll see here is in Swift as well.

## How to use
The Legiti iOS Library can be installed through [CocoaPods](https://cocoapod.org). To install all you have to do is follow this steps:

1. Add our library to you Podfile (`pod Legiti`)
1. Run `pod install` command

P.S: When you import the Legiti library you will see that you are actually installing more than one library, since the Legiti iOS Library have some dependencies.

## API Docs
You can find more in-depth documentation about our frontend libraries and integrations in general [here](https://docs.legiti.com).

### Library setup
In order to properly relay information to Legiti's processing pipeline, you'll need to provide your customer-specific authentication credential:
- authToken (provided by Legiti)

**P.S:** Remember to use the *sandbox* `authToken` when you are not in production

With these, you can instantiate the Legiti tracking instance. Our integration library instantiates a singleton instance to prevent multiple trackers from being instantiated, which could otherwise result in duplicate or inconsistent data being relayed to Legiti. Apart from that, the singleton will let you configure the library only once.

The singleton instance is instantiated as follows:

```
do {
  try Legiti.sharedInstance().setup(authToken: "authToken")
} catch TrackerException.requiredConfig(let code, let message) {
  print("code: \(code) - message: \(message)")
} catch {
  print("Error")
}
```

Be advised, that this function can throw an exception if you pass invalids authToken (empty strings or not in the format required).

We **strongly** recommend you instantiate the Legiti Library in your application `AppDelegate` in the `didFinishLaunchingWithOptions` function, since this way you will configure the library as soon as the app loads enabling you to call the library functions.

All the access to the Legiti functions is made by calling the `Legiti.sharedInstance()`.

The function only takes one parameter:

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
authToken       | Yes | String  | An unique identifier that the Legiti Team will provide to you

P.S: always remember to import the library using the  `import Legiti`

### Library Calls
If you've already read the [general Legiti files](https://docs.legiti.com), you should be aware of all of Legiti requests and collection functions.

Here we will show you some details to be aware of if you are calling the Legiti tracking functions.

All of out *track functions* can throw exceptions, but the only exception they will through is if you forget to configure the Legiti Library before calling one of them. Because of that the Legiti class have a function called `isConfigured()` that returns a boolean saying if you have configured or not the Legiti Library. We recommend that when you call any of our tracking functions you check if the Legiti Library is configured. Here is an example on how to do that:

```
if (Legiti.sharedInstance().isConfigured()) {
    try! Legiti.sharedInstance().trackUserCreation(userId: "123")
}
```

#### TrackScreenView
Different from the Legiti Javascript Library the track of user pageviews (screenview) is not done automatically. You need to add the function `trackPageView` on every new page.
We **strongly recommend** that you add the functions inside the `viewDidLoad` of every ViewController in your app, since this way we can track the pageview/screenview action as soon as it happens. You can see an example of this implementation bellow:

```
override func viewDidLoad() {
  super.viewDidLoad()
  if (Legiti.sharedInstance().isConfigured()) {
      try! Legiti.sharedInstance().trackPageView(pageTitle: "login-page")
  }
}
```

### User Location
The Legiti iOS Library can use the user location to help us provide more accurate results, but it will **never** ask for it. If your app already has access to user location the library will automatically capture it, otherwise it won't send the location to us.

### Models
If you are coming from one of our backend libraries you will notice that we do not use models (e.g. Account, Sale) in our frontend libraries. Here you just need to send us the id of the model (e.g. sale ID, account ID).

## More Information
For more info you should check the [Legiti Frontend docs](https://docs.legiti.com)
