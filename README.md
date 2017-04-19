# electron-chrome-extension-messaging #

## Chrome Native Messaging (CNM) ##

## Custom protocol handler ##

It is possible to register electron app as default protocol client using `app.setAsDefaultProtocolClient`  (https://electron.atom.io/docs/api/app/#appsetasdefaultprotocolclientprotocol-path-args-macos-windows). Thus for example if you set `app.setAsDefaultProtocolClient('example')` if user tries to open any link starting with `example://` , electron app will be opened and the full url including protocol, will be passed to as a parameter (`process.args`)

**upsides**

- arguably the easiest and the most straightforward way to open electron app and/or pass message to it
- no registry amends or system tweaks needed

**downsides**

- in Chrome there is protocol open confirmation popup up until you check 'Remeber my choice' - highly annoying
- minor chances (but still chances are) that at some point this custom protocol will become generic web protocol thus it might produce unexpected issues

## Clipboard hack ##

In the essence this approach is based on chrome native messaging. Just like in CNM approach it is necessary to register native messaging host for OS. But with this hack it is unnecessary to handle process.stdin within electron app. Instead of this it is possible to interchange data between chrome extension and electron app using clipboard data.

Generally this approach seems to be reasonable when it is neccessary to easily implement cross-platform electron's callback upon some conscious user action within chrome extension (i.e. item click, form submission etc). 

**upsides**

- doesn't require platform tweaks 
- doesn't display any confirmation messages

**downsides**

- user's clipboard gets overwritten once message occur
- possible clipboard updates during application start (before clipboard is read)
