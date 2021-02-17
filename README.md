# What is RudderStack?

[RudderStack](https://rudderstack.com/) is a **customer data pipeline** tool for collecting, routing and processing data from your websites, apps, cloud tools, and data warehouse.

More information on RudderStack can be found [here](https://github.com/rudderlabs/rudder-server).

## Integrating Amplitude with RudderStack's iOS SDK

1. Add [Amplitude](https://amplitude.com) as a destination in the [RudderStack dashboard](https://app.rudderstack.com/) and define all the fields.


3. Rudder-Amplitude is available through [CocoaPods](https://cocoapods.org). To install it, simply add the following line to your Podfile:

```ruby
pod 'Rudder-Amplitude'
```

## Initialize ```RudderClient```

Put this code in your `AppDelegate.m` file under the method `didFinishLaunchingWithOptions`:

```XCode
RSConfigBuilder *builder = [[RSConfigBuilder alloc] init];
[builder withDataPlaneUrl:DATA_PLANE_URL];
[builder withFactory:[RudderAmplitudeFactory instance]];
[RSClient getInstance:WRITE_KEY config:[builder build]];
```

Add the below logic just after initalizing ```RudderClient``` in ```AppDelegate.m``` if you would like to send ```IDFA``` of ```iOS device``` as device id to Amplitude
```XCode
[Amplitude instance].adSupportBlock = ^{
return [[ASIdentifierManager sharedManager] advertisingIdentifier];
};
```

Then, add the below logic if you would like to ```track location``` (latitude, longitude)
```XCode
[Amplitude instance].locationInfoBlock = ^{
        return @{
                  @"lat" : @37.7,
                  @"lng" : @122.4
                };
};
```

## Send Events

Follow the steps from [RudderStack iOS SDK](https://github.com/rudderlabs/rudder-sdk-ios).

## Contact Us

If you come across any issues while configuring or using this integration, feel free to start a conversation on our [Slack](https://resources.rudderstack.com/join-rudderstack-slack) channel. We will be happy to help you.
