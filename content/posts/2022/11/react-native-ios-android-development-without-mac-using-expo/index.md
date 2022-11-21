---
Title: How-To Develop an iOS & Android App Without a MAC Using ReactNative and Expo
date: 2022-11-28
cover:
  image: cover.jpg
tags:
- app-development
- react-native
- expo
- entrepreneurship
categories:
- App Development
---

## Developing an iOS App Without a MAC is Hard

You know what I am talking about if you ever tried it...  

But I did not want to give up [developing my first app][starting]. So I did some research and tested out the various big cross platform frameworks: [Flutter][flutter], [Xamarin][xamarin], and [React Native][react-native]. The problem is that I have an iPhone and no MAC but every framework requires one to build and test the app for iOS.

### Expo Application Services to the Rescue

Then I came across [Expo][expo] which extends React Native with a lot of useful libraries and features that make the native mobile app more like a React web app. But the real power comes from its free build service: [Expo Application Services][eas]. It enables you to build, test and deploy your app without ever touching a MAC. And all that in an easy and very well documented process. To get started simply follow their [documentation][expo-start] and you will have your first app up and running on your real device in under five minutes.

To create a new app run:

```shell
npx create-expo-app my-app
```

Download the [Expo Go][expo-go] app on your phone while the npm dependencies are installing. And then start the app:

```shell
cd my-app
npx expo start
```

### Expo Standalone Development Client

This will get you started with the most basic app. I however used the [Ignite Boilerplate][ignite] to get me up and running with some of the best practices and a solid foundation. From there I integrated [React Native Firebase][rnfirebase] and kicked off a [standalone development client][devclient] build moving away from the Expo Go client.

Every additional native library needs a new development client build as it bundles the required dependencies into the client and allows you to serve the web bundle compiled by `eas update`. Try to forsee some of the libraries you'll want to use in the future and bundle them into your standalone client. This will save you a lot of time waiting for `eas build` slots. Just make sure to throw out unneeded dependencies before your first release to the app stores.

---

How is Expo working for you? Did you come across any problems? Leave a comment below.

In one of my next posts I am going to show you how I automated everything using Github actions.

 <!-- TODO: add link to next blog post about github actions -->

[starting]: ../how-i-started-working-on-my-dream-beside-my-main-job
[flutter]: https://flutter.dev/
[xamarin]: https://dotnet.microsoft.com/en-us/apps/xamarin
[react-native]: https://reactnative.dev/
[expo]: https://expo.dev/
[eas]: https://expo.dev/eas
[expo-start]: https://docs.expo.dev/get-started/create-a-new-app/
[expo-go]: https://expo.dev/client
[ignite]: https://github.com/infinitered/ignite
[rnfirebase]: https://rnfirebase.io/
[devclient]: https://docs.expo.dev/development/create-development-builds/
