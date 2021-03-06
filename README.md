# Wordpress Mobile Automation

[//]: # (Image References)
[automationgif]: ./readme/automation_sample.gif
[automationgif1]: ./readme/automation_sample1.gif

[![CircleCI](https://circleci.com/gh/JavonDavis/Wordpress-Automation-Ruby.svg?style=svg)](https://circleci.com/gh/JavonDavis/Wordpress-Automation-Ruby)

This project demonstrates mobile app automated testing using the [parallel_appium gem](https://github.com/JavonDavis/parallel_appium) to do a lot of the heavy lifting. The 
project demos the basics of testing with Appium and Ruby, shows some advanced techniques and through the gem uses SeleniumGrid
to distribute tests across devices and execute tests in parallel.

![Automation Gif][automationgif]

![Automation Gif][automationgif1]

## What does this project do

* Run UI tests on the Wordpress mobile apps
* Demonstrate a project structure for testing with Appium, RSpec and Selenium
* Demonstrate the use of the [parallel_appium gem](https://github.com/JavonDavis/parallel_appium) for running rspec appium 
tests in a single or multi-threaded environment across platforms
* Demonstrate setting up a continuous integration flow with CircleCi, Appium and Rspec for Mobile testing
* Demonstrate techniques for locating and interacting with elements through Appium

## View Report 

A report aside from the one generated by CircleCi is provided in the artifacts of the build. You can check out the latest one 
by clicking the link under the title at the top of the README. 
Here's [a link](https://66-138766831-gh.circle-artifacts.com/0/wordpress/index.html) to the 
report for one of the builds to give you an idea of what's provided.

## Getting setup

First let's get the apps we'll be automating. 
The app we'll be automating is the Wordpress mobile app which is open source and free to use and is a pretty great app
 overall and beat all the other options I think for a demo app, kudos to the team over at Wordpress. The builds tested with this project I've made publicly available to download below,

* [Android](https://drive.google.com/file/d/1Hb2z7guNc8ch1o11mmuP5aioJ_Endal3/view?usp=sharing)
* [iOS](https://drive.google.com/file/d/18ODObtGuG3UYhgst-6h6ucn79_kYTxwD/view?usp=sharing)

If you'd like to build the apps yourself you can visit the wordpress-mobile github pages and build the app from source via the following commands
for Android and iOS. 


## [Building android app](https://github.com/wordpress-mobile/WordPress-Android) 

Executing the following command will build an unsigned version of the Android app that can be used, 

```./gradlew assembleVanillaDebug```

This will generate an apk that can be used for testing.


## [Building iOS app](https://github.com/wordpress-mobile/WordPress-iOS) 

From the project root you'll need to execute the following command with the correct sdk based on the XCode version on your machine, currently mine is 9.4,

```xcodebuild -workspace WordPress.xcworkspace -scheme WordPress -configuration “Debug” -sdk iphonesimulator11.4```

This command will build a .app file that can be used for testing on an iPhone simulator, you'll need to compress this file into a
.app.zip file or you can use the .app file if you'd like just remember to update the path in the appium-ios.txt file.


Once you've got your apk and .app.zip file you'll need to move them into the .apps folder or update the appium text
 files to point to their correct location. For CI setup I would recommend the apps folder to keep things simple.

Next you'll need to install the dependencies to run the app. That's a pretty simple step

## Install dependencies

```bundle install --path vendor``` boom and the dependencies will be installed!

## Parallel Appium depenency

The [parallel_appium gem](https://github.com/JavonDavis/parallel_appium) covers a lot of bases including starting 
the appium server, selenium server and setting up and coordinating environment variables. **For this project to work well
ensure you've followed the instructions in that repository for setting up the gem.**

## Appium text files

Appium text files are provided in the repository as per the requirement of the [parallel_appium gem](https://github.com/JavonDavis/parallel_appium)
but when running this locally please remember to adjust these to match out with your machine. 


## Running the Project

The task for testing is defined as test within the wordpress namespace and should be fired up via rake.
Recall as per the requirement of the  [parallel_appium gem](https://github.com/JavonDavis/parallel_appium) an environment
variable with the platform will need to be set prior to running. The command also accepts
a parameter which can be the path to the file or folder of the specs to be executed, this will default 
to spec/ if left blank.... Now here's a few examples: 

### Running all iOS tests

platform=ios bundle exec rake wordpress:test

### Running all android tests

platform=ios bundle exec rake wordpress:test

### Running all tests on both platforms simultaneously

platform=all bundle exec rake wordpress:test

### Running a single iOS test

platform=ios bundle exec rake wordpress:test[relative/path/to/spec]

## Viewing report locally

Reports are generated with allure and the data for the report is stored in the output folder after the tests are finished,
this includes any screenshots along with the test results and meta data. It's then compiled and stored in 
a wordpress-report folder in the project, you can open the report via Allure or you can simply execute,

```bundle exec rake wordpress:report```

and the report will open up in a browser for you. 


## Contributing and Bug reporting

Not going to say much here right now, just be polite, open issues and send in PRs if there's any 
problems or improvements you'd like to make.

This software is provided "as is" and without any express or implied warranties, including, without limitation, 
the implied warranties of merchantibility and fitness for a particular purpose.

Hope this gem makes someone's life easier!
