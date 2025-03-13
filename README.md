# Browser Images

This repository contains [Docker](http://docker.com/) build files to be used for [Selenoid](http://github.com/aerokube/selenoid).
Updated to support Chrome-for-testing releases.

## How to build an image:
### MacOS

1. Install go environment via homebrew or direct download from https://go.dev/doc/install. Check with go.mod and CI scripts to align the go version. Setup go path:
```
export GOPATH=/Users/<<USER>>/go
export PATH=$GOPATH/bin:$PATH
export DOCKER_DEFAULT_PLATFORM=linux/amd64
```
3. Install and run the packager for static Dockerfiles (required if Dockerfiles are modified):
```
go install github.com/markbates/pkger/cmd/pkger@latest
go install github.com/mitchellh/gox@latest # cross compile
go generate github.com/aerokube/images
```
4. Build the image builder binary:
go clean
go build
5. And now execute the binary like this:
```
./images chrome -b $(curl -s https://googlechromelabs.github.io/chrome-for-testing/last-known-good-versions.json | jq -r '.channels.Stable.version') -d latest -t selenoid/chrome:latest
```



Example of _~/.aerokube/selenoid/browsers.json_:
```
    {
      "chrome": {
        "default": "latest",
        "versions": {
          "latest": {
            "image": "selenoid/chrome:latest",
            "port": "4444",
            "path": "/"
          }
        }
      }
    }
```

### Documentation:
http://aerokube.com/images/latest/#_building_images
