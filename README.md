Cordova helps us make apps easily. The ability to run the apps inside browser greatly speeds up the development cycle. But I feel that it is hard to debug and rerun in a real device, especially I need to debug some plugin which needs real devices support. Normally I need to compile and redeploy the app. It takes at least 1 minutes to get all things ready even running inside Samsung S5.

The cordova apps are running inside a WebKit, Chrome helps to connect the apps and you can inspect element or use any javascript debugging tool. Imaging the app is loaded from a self-hosted server, in the chrome developer tool, I can refresh the browser to load modified content. This is cool because you don't need to compile and restart the app, it saves a lot of when need to go through a lot of steps to reach that page. Question: How to do it?

The basic idea is to serve /www folder in http server. You could use nodejs "http-server" as a quick start. But compare to the /platforms/android/assets/www folder, there are some files missing including cordova.js, cordova_plugins.js and plugins folder. We need to copy these files into /www folder so apps can get the cordova initialized.

We need to modify the entry page (index.html) for apps to load from the server, otherwise it will load local content inside apps. It is a simple redirect. Then we need to create a new app.html which is same as original index.html.

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta http-equiv="refresh" content="0; url=http://SERVER:IP/app.html" />
    <title></title>
</head>
</html>
```

When app is loaded, the index.html will redirect to the app.html which is hosted in server. If you want to modify the app, just modify the apps and then refresh the page.

Demo:
Clone the app: https://github.com/derekhe/speed-up-cordova/
Serve the server
```
npm install -g http-server
cd www
http-server
```

Run the app
```
cordova emulate android
```
