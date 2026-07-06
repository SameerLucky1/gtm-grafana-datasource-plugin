# Build Instructions
Build, package and release the "Global Traffic Management (GTM) Datasource" plugin.

## Clone or fork the repository
See [Git Handbook](https://guides.github.com/introduction/git-handbook/) for instructions.  
If you clone, all changes should be made on the 'develop' branch.

## Update the version number
Edit package.json

Advance the version number.  For example:
```
  "version": "2.0.0",
```

## Build
See these references:  
* [Build a plugin](https://grafana.com/docs/grafana/latest/developers/plugins/)
* [Build a data source plugin](https://grafana.com/tutorials/build-a-data-source-plugin/)

### First time build

#### Prerequisites
This project uses Yarn v4.17.0 (Yarn Berry) via Corepack. If you haven't enabled Corepack yet:
```
corepack enable
```

#### Install dependencies
```
yarn install
```

### Build the back end
Run this command:
```
mage -v
```

My output (after having previously built), looks like this:
```
$ mage -v
Running dependency: github.com/grafana/grafana-plugin-sdk-go/build.Build.LinuxARM-fm
Running dependency: github.com/grafana/grafana-plugin-sdk-go/build.Build.Linux-fm
Running dependency: github.com/grafana/grafana-plugin-sdk-go/build.Build.Darwin-fm
Running dependency: github.com/grafana/grafana-plugin-sdk-go/build.Build.LinuxARM64-fm
Running dependency: github.com/grafana/grafana-plugin-sdk-go/build.Build.Windows-fm
exec: go build -o dist/gpx_akamai-gtm-datasource-plugin_linux_arm -ldflags -w -s -extldflags "-static" ./pkg
exec: go build -o dist/gpx_akamai-gtm-datasource-plugin_windows_amd64.exe -ldflags -w -s -extldflags "-static" ./pkg
exec: go build -o dist/gpx_akamai-gtm-datasource-plugin_darwin_amd64 -ldflags -w -s -extldflags "-static" ./pkg
exec: go build -o dist/gpx_akamai-gtm-datasource-plugin_linux_amd64 -ldflags -w -s -extldflags "-static" ./pkg
exec: go build -o dist/gpx_akamai-gtm-datasource-plugin_linux_arm64 -ldflags -w -s -extldflags "-static" ./pkg
```

### Build the front end
Run this command:
```
yarn build
```

My output (after having previously built), looks like this:
```
$ yarn build
assets by path *.md 8.96 KiB
  asset README.md 8.13 KiB [compared for emit] [from: ../README.md] [copied]
  asset CHANGELOG.md 854 bytes [compared for emit] [from: ../CHANGELOG.md] [copied]
asset module.js 12.5 KiB [compared for emit] [minimized] (name: module) 1 related asset
asset LICENSE 11.1 KiB [compared for emit] [from: ../LICENSE] [copied]
asset img/akamai-logo.png 1.72 KiB [compared for emit] [from: img/akamai-logo.png] [copied]
asset plugin.json 1.26 KiB [emitted] [from: plugin.json] [copied]
cached modules 56 KiB (javascript) 1.74 KiB (runtime) [cached] 64 modules
webpack 5.108.2 compiled successfully in 84 ms
```

## Commit your changes 
See [Git Handbook](https://guides.github.com/introduction/git-handbook/) for instructions.  
Open a Pull Request.

## Package
Copy the 'dist' directory to 'akamai-gtm-datasource' and then compress.
```
cp -r dist akamai-gtm-datasource
zip akamai-gtm-datasource-2.0.0.zip akamai-gtm-datasource/ -r
```
'2.0.0' is an example. Use your current plugin version number.

## Release
Navigate to https://github.com/akamai/gtm-grafana-datasource-plugin.
Log in. (You'll need admin rights.)

Follow the directions in [Managing releases in a repository](https://docs.github.com/en/github/administering-a-repository/managing-releases-in-a-repository).  
Tags should start with 'v', followed by the build number.  For example, 'v2.0.0'.  

