---
title: Tips on developing cross-platform Node.js CLI application
date: 2019-05-13 20:08:16
categories:
- Programming
tags:
- javascript
- nodejs
---

In the past few weeks, I have been working on [Koop CLI](https://github.com/koopjs/koop-cli), a Node.js CLI application for developers to build [KoopJS](https://koopjs.github.io/) plugins. It has been a big lesson for me about how to create an app that works at different platforms/OSs. Here in this blog post I am going to share some tips.

<!-- more -->

## So why do I care about cross-platform?

[KoopJS](https://koopjs.github.io/) is an open-source framework powered by community-developed plugins. Making the CLI application available to more and various developers is the key of growing the community.

{% asset_img dev-survey.png This is an example image %}

Developers are in favor of many different platforms, according to [StackOverflow](https://insights.stackoverflow.com/survey/2019#technology-_-platforms). Linux, Windows, and MacOS all have significant market share. If the CLI application is able to work on all these platforms, developers from anywhere will be able to try it, create a KoopJS plugin/applicatoin, and possible contribute it back to the community.

## Developing cross-platform CLI application

Though Node.js and many npm modules are cross-platform, it does not mean the application you develop is cross-platform. This is particuarly true when the application is processing the system info and user input.

### Make use of [os](https://nodejs.org/api/os.html)

The Node.js [os](https://nodejs.org/api/os.html) module is the only way to access any platform-specific information, like the OS version, the system hardware information, the temp file folder, etc.

Don't assume that you know about the user's machine and use `/tmp` in the code. It will blow up.

### Be careful about file path

[File path styles]((https://en.wikipedia.org/wiki/Path_(computing))) vary from one platform to another. Whenever possible, use the native [path](https://nodejs.org/api/path.html) module to handling file path processing. Don't the simple string handling (like `path.split('\')`, `paths.join('\')`, etc) or regular expression because there is always outlier and it will break.

### Newline matters

Newline is simple?

{% asset_img newline.png This is an example image %}

Although your application may not support so many platforms as listed, it is obvious that `\n` (Linux and MacOS) and `\r\n` (Windows) should be at least supported at the same time. Do try [os.EOL](https://nodejs.org/api/os.html#os_os_eol) when processing user input text and generating output.

## Testing on different platforms

Testing the application at different platforms is a trivial task for human developers. Ideally, we should write tests for the application and run tests at multiple platforms by CI automatically. So write once and test many.

Many CI/CD service providers support building and testing with different platforms. For example, we can add multiple OSs in the [Travis CI](https://travis-ci.org) configuration:

``` yaml
language: node_js
os:
  - linux
  - osx
  - windows
script:
  - npm test
```

## End

This blog post talks about a few tips from my personal experience on developing the Koop CLI project. For more details on developing cross-platform experience, do checkout the [cross-platform node guide](https://github.com/ehmicky/cross-platform-node-guide) repo. And happy coding.
