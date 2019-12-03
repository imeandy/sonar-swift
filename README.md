<p align="left">
  <img src="https://www.backelite.com/wp-content/uploads/2016/09/logo-backelite-square.png" width="100"/>
</p>

| Branch   |      Status                                                                                                                                |
|----------|:------------------------------------------------------------------------------------------------------------------------------------------:|
| master | [![Build Status](https://travis-ci.org/Backelite/sonar-swift.svg?branch=master)](https://travis-ci.org/Backelite/sonar-swift)  |
| develop| [![Build Status](https://travis-ci.org/Backelite/sonar-swift.svg?branch=develop)](https://travis-ci.org/Backelite/sonar-swift) |

SonarQube Plugin for Swift
================================

This is an open source initiative for Apple Swift language support in SonarQube.
The structure of the plugin is based on the [sonar-objective-c](https://github.com/octo-technology/sonar-objective-c) plugin.

<p align="center">
  <img src="screenshot.png" alt="Example iOS SonarQube dashboard" width="100%"/>
</p>

In SonarQube under Quality Profiles the used Linter can be specified by selecting either the SwiftLint Profile or the Tailor Profile as Default profile for Swift Projects:
<p align="center">
  <img src="SwitchProfiles.png" alt="Set preferred profile (SwiftLint or Tailor) to default in SonarQube." width="100%"/>
</p>

### Features

| Feature 		| Supported	| MacOS	      | Unix        |
|---------------|-----------|:-----------:|:-----------:|
| Complexity	|YES		|Uses [Lizard](https://github.com/terryyin/lizard)| Uses [Lizard](https://github.com/terryyin/lizard)|
| Design		|NO			|			  |             |
| Documentation	|YES		|			  |             |
| Duplications	|YES		|			  |             |
| Issues		|YES		| Uses [SwiftLint](https://github.com/realm/SwiftLint) and/or [Tailor](https://github.com/sleekbyte/tailor) for Swift. [OCLint](http://oclint-docs.readthedocs.io/en/stable/) and [Faux Pas](http://fauxpasapp.com/) for Objective-C| Uses [Tailor](https://github.com/sleekbyte/tailor)|
| Size			|YES		|			  |             |
| Tests			|YES		| Uses xcodebuild + xcpretty [xcpretty](https://github.com/supermarin/xcpretty)	| Not Supported |
| Code coverage	|YES	    | Uses [slather](https://github.com/venmo/slather)			| Not Supported|


### 0.4.4 CHANGELOG

```Passed On MacOS 10.14.1```

- Supported SonarQube Community Version 7.4
- Fixed: compiler warning error
- Fixed: Lizard parser error. because of wrong lizard xml report format
- Fixed: OCLint Parser error. can not find file caused null pointer exception
- Fixed: Slather Parser error. can not find file caused null pointer exception

### Prerequisites

- a Mac with Xcode 9 or +
- [SonarQube](https://docs.sonarqube.org/display/SONAR/Setup+and+Upgrade) and [SonarQube Scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner)
- [xcpretty](https://github.com/supermarin/xcpretty) (see instructions below)
- [SwiftLint](https://github.com/realm/SwiftLint) ([HomeBrew](http://brew.sh) installed and ```brew install swiftlint```). Version 0.3.0 or above.
- [Tailor](https://github.com/sleekbyte/tailor) ([HomeBrew](http://brew.sh) installed and ```brew install tailor```). Version 0.11.1 or above.
- [slather](https://github.com/SlatherOrg/slather) (```gem install slather```). Version 2.1.0 or above (2.4 since Xcode 8.3).
- [lizard](https://github.com/terryyin/lizard) ([PIP](https://pip.pypa.io/en/stable/installing/) installed and ```sudo pip install lizard```)
- [OCLint](http://oclint-docs.readthedocs.io/en/stable/) installed. Version 0.13.0 recommended (0.13.0 since Xcode 9).

### Download

Checkout the [Releases](https://github.com/imeandy/sonar-swift/releases) page.

The full release history is also available in [CHANGELOG.md](./CHANGELOG.md).

### Launching an analysis
If you use [fastlane](https://fastlane.tools), please read [our fastlane integration doc](docs/sonarqube-fastlane.md).
Otherwise, run the ```run-sonar-swift.sh``` script from your Xcode project root folder


### Installation of xcpretty with JUnit reports fix

At the time, xcpretty needs to be fixed to work with SonarQube.

To install the fixed version, follow those steps :

	git clone https://github.com/Backelite/xcpretty.git
	cd xcpretty
	git checkout fix/duration_of_failed_tests_workaround
	gem build xcpretty.gemspec
	sudo gem install --both xcpretty-0.2.2.gem

### Installation (once for all your Swift projects)
- Download the plugin binary into the $SONARQUBE_HOME/extensions/plugins directory
- Copy [run-sonar-swift.sh](https://raw.githubusercontent.com/imeandy/sonar-swift/develop/run-sonar-swift/run-sonar-swift.sh) somewhere in your PATH
- Restart the SonarQube server.

### Configuration (once per project)
- Copy [sonar-project.properties](https://raw.githubusercontent.com/imeandy/sonar-swift/develop/sonar-project.properties) in your Xcode project root folder (along your .xcodeproj file)
- Edit the ```sonar-project.properties``` file to match your Xcode iOS/MacOS project

**The good news is that you don't have to modify your Xcode project to enable SonarQube!**. Ok, there might be one needed modification if you don't have a specific scheme for your test target, but that's all.

### Update (once per plugin update)
- Install the lastest plugin version
- Copy ```run-sonar-swift.sh``` somewhere in your PATH

If you still have *run-sonar-swift.sh* file in each of your project (not recommended), you will need to update all those files.

### Faux Pas support

[Faux Pas](http://fauxpasapp.com/) is a wonderful tool to analyse iOS or Mac applications Objective-C source code, however it is not free. A 30 trial version is available [here](http://fauxpasapp.com/try/).

The plugin runs fine even if Faux Pas is not installed (Faux Pas analysis will be skipped).

### Contributing

Thank you for your interest in the project! Contributions are welcome and appreciated.

Make sure to read these guides before getting started:

- [Code of Conduct](./CODE_OF_CONDUCT.md)
- [Contribution Guidelines](./CONTRIBUTING.md)

### License

SonarQube Plugin for Swift is released under the GNU LGPL v3 license. See the [LICENSE](./LICENSE.md) file for more info.
