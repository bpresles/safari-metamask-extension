## Safari 14 Extension

The Safari extension can be achieved from the Chrome-targeting build now, with very little changes.
First of all, before beginning, make sure you have Safari 14 and Xcode 12 installed.

### Building the extension for Chrome

```
$ nvm use 16
```

Copy .metamaskrc.dist to .metamaskrc
```
cp .metamaskrc.dist .metamaskrc
```

Edit .metamaskrc and change the INFURA_PROJECT_ID to your own project id.


Build Metamask.
```
$ yarn dist
```

### Bootstrapping the Xcode project

This step is necessary if you want to build the extension for yourself or distribute in the Apple Safari Extensions store. The generated project contains no specific patches, so the resulting output in `safari/` will be ignored by Git.

```
$ yarn safari-extension-convert
```

It runs `xcrun safari-web-extension-converter` internally, a tool provided by Apple in Xcode 12+.

Upon completion, we get the following warning that can be ignored:
```
Warning: The following keys in your manifest.json are not supported by your current version of Safari. If these are critical to your extension, you should review your code to see if you need to make changes to support Safari:
	notifications
	persistent
	externally_connectable
```

### Building the extension

```
$ open ./safari/MetaMask/MetaMask.xcodeproj
```

Will launch an Xcode instance. Just press "Start" button there.

Safari will be opened, yet extension will not appear at first sight. You need to do the following steps first:

* Safari -> preferences -> enable development menu
* Safari -> develop menu -> click allow unsigned extension (need to do this every time Safari is restarted)
* Safari -> preferences -> extensions tab -> click the extension
* Open a web site, click the icon near the address bar, and allow the access

These steps are for local non-signed builds. Do not trust any externally built extension that is not signed.
