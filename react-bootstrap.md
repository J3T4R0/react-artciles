## TL;DR
A place for different bootstraps, either for making or for compiling
### Article Link
github.com/loq24/wp-react-typescript/
build.affinity.co/sharing-code-between-web-react-native-why-how-to-configure-metro-for-code-sharing-d6ec73427e08
github.com/expo/turtle-cli-example/
### Author
Alvise Susmel 
## Key Takeaways
* How to interoperate between react native web and react native 
* How to develop a react app with typescript and a wordpress backend
* metro

## Useful Code Snippets
```sh
git clone https://github.com/loq24/wp-react-typescript
cd wp-react-typescript
yarn install OR npm install
yarn start OR npm start
```
rn-client-config.js
```javascript
let path = require("path")

module.exports = {
  getTransformModulePath() {
    return require.resolve("react-native-typescript-transformer")
  },
  sourceExts: ["ts", "tsx"],
  // Set projectRoot to the web front-end root (Realization 1 above)
  projectRoot: path.resolve(__dirname, "../assets/javascripts"),
  // Set watchFolders to include the current directory, parent node_modules
  // and the mobile node_modules (Realization 2 above)
  watchFolders: [
    path.resolve(__dirname),
    path.resolve(__dirname, "./node_modules"),
    path.resolve(__dirname, "../node_modules"),
  ],
  resolver: {
    // Set extraNodeModules to include the directories that you want to import
    // files from (in our case, we wanted to import files specifically from
    // util and types)
    extraNodeModules: {
      util: path.resolve(__dirname, "../assets/javascripts/util"),
      types: path.resolve(__dirname, "../assets/javascripts/types"),
    },
  },
}
```

expo sdk config
```yaml
android:
  # WARNING: medium (default) seems not to be enough for Turtle
  resource_class: xlarge
  docker:
    # https://github.com/expo/expo-turtle-android
    - image: dsokal/expo-turtle-android
  working_directory: ~/expo-project
  environment:
    EXPO_SDK_VERSION: 37.0.0 # << REPLACE WITH THE EXPO SDK VERSION OF YOUR APP
    TURTLE_VERSION: 0.14.6   # << REPLACE THE LATEST TURTLE-CLI VERSION HERE
    PLATFORM: android
    YARN_CACHE_FOLDER: ~/yarn_cache

ios:
  macos:
    xcode: 10.1.0
  working_directory: ~/expo-project
  environment:
    EXPO_SDK_VERSION: 37.0.0 # << REPLACE WITH THE EXPO SDK VERSION OF YOUR APP
    TURTLE_VERSION: 0.14.6   # << REPLACE THE LATEST TURTLE-CLI VERSION HERE
    PLATFORM: ios
    YARN_CACHE_FOLDER: /Users/distiller/yarn_cache
    HOMEBREW_NO_AUTO_UPDATE: 1
 ```
 
 Upgrading app through travis
 ```yaml
 env:
  global:
    - EXPO_SDK_VERSION="37.0.0"  # << REPLACE WITH THE EXPO SDK VERSION OF YOUR APP
    - TURTLE_VERSION="0.14.6"    # << REPLACE THE LATEST TURTLE-CLI VERSION HERE
    - NODE_VERSION="12.13.1"
    - YARN_VERSION="1.21.1"
```


## Useful Tools
* metro
* turtle cli

## Comments/ Questions
