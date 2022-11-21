---
Title: How-To Develop an iOS & Android App Without a MAC Using ReactNative and Expo
draft: true
date: 2022-11-07
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

But I did not want to give up developing my first app to, someday, start my own startup. So I did some research and tested out the various big cross platform frameworks: [Flutter][flutter], [Xamarin][xamarin], and [React Native][react-native]. The problem is that I have an iPhone and no MAC but every framework requires one to build and test the app.

Then I came across [Expo][expo] which extends React Native with a lot of useful libraries and features that make the native mobile app more like a React web app. But the real power comes from its free build service: [Expo Application Services][eas]. It enables you to build, test and deploy your app without ever touching a MAC. And all in an easy and very well documented process. To get started simply follow their [documentation][expo-start] and you will have your first app up and running on your real device in under five minutes.

To create a new app run:

```shell
npx create-expo-app my-app
```

Download the [Expo Go][expo-go] app on your phone while the npm dependencies are installing. And then start the app:

```shell
cd my-app
npx expo start
```

This will get you started with the most basic app. I however used the [Ignite Boilerplate][ignite] to get me up and running with some of the best practices and a solid foundation. From there I integrated [React Native Firebase][rnfirebase] and kicked off a standalone development client build moving away from the Expo Go client.

TODO: describe standalone app

TODO: describe integrating react native firebase

TODO: show github workflows


- Problem: 
- Setting up a workflow with expo that solves the issue

Follow Up: blog post for automating expo deployments and builds using github actions

[flutter]: https://flutter.dev/
[xamarin]: https://dotnet.microsoft.com/en-us/apps/xamarin
[react-native]: https://reactnative.dev/
[expo]: https://expo.dev/
[eas]: https://expo.dev/eas
[expo-start]: https://docs.expo.dev/get-started/create-a-new-app/
[expo-go]: https://expo.dev/client
[ignite]: https://github.com/infinitered/ignite
[rnfirebase]: https://rnfirebase.io/
