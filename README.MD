## Tutorial of build Mobile APP by Framework7+Vue.js+Phonegap

> Ref to: http://hollyschinsky.github.io/spotify-browser/index.html (F7+js)

#### Purpose:
quickly learn F7+Vue.js

#### Install:
1. Install template first:
```
phonegap create spotifyApp --template cordova-template-framework7-vue-webpack
cd spotifyApp
npm install
npm install uglify-js@^2.8.0
phonegap platform add browser android
phonegap run browser -- --lr
```

2. Download this git, then replace template's /src/ directory and /config.xml with git's.

#### Intruduction:
[Framework7+Vue.js Spotify播放器 - 实例详解](http://www.jianshu.com/p/976d34fcd77e)
