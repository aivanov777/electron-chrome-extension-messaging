# electron-chrome-extension-messaging #

## Chrome Native Messaging (CNM) ##

## Custom protocol handler ##

## Clipboard hack ##

In the essence this approach is based on chrome native messaging. Just like in CNM approach it is necessary to register native messaging host for OS. But with this hack it is unnecessary to handle process.stdin within electron app. Instead of this it is possible to interchange data between chrome extension and electron app using clipboard data.

Generally this approach seems to be reasonable when it is neccessary to easily implement cross-platform electron's callback upon some conscious user action within chrome extension (i.e. item click, form submission etc). 

**upsides**

- doesn't require platform tweaks 
- doesn't display any confirmation messages

**downsides**

- user's clipboard gets overwritten once message occur
- possible clipboard updates during application start (before clipboard is read)
