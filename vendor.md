# Vendor Procedure

In order to make sure that a released version of *pipeline* can be
reproduced, dependencies are vendored in using
[dep](https://golang.github.io/dep/docs/introduction.html). Whenever a
dependency is added or updated, install and test.

[dep cheat sheet for glide users](https://gist.github.com/subfuzion/12342599e26f5094e4e2d08e9d4ad50d)

## How to bring vendor code in under the vendor directory

(1) Add library versions to use in [Gopkg.toml](https://github3.cisco.com/ROBOT/pipeline/blob/develop/Gopkg.toml) use
[version for git tag or revision for commit hash](https://github.com/golang/dep/blob/master/docs/Gopkg.toml.md)
    

(2) Pull in libraries via dep

    dep ensure -add github.com/foo/bar github.com/baz/quux


(3) Apply the file `vendor.patch` to fix an issue in a json google library manifested 
    when streaming json out to kafka.

    make patchvendor (or) git apply --verbose ./vendor.patch
    
(4) To update a existing library, update the version in [Gopkg.toml](https://github.com/ganesh-karthick/bigmuddy-network-telemetry-pipeline/blob/master/Gopkg.toml) 
and run
    
    dep ensure

(5) To remove a library, remove it in [Gopkg.toml](https://github.com/ganesh-karthick/bigmuddy-network-telemetry-pipeline/blob/master/Gopkg.toml) and
run
    ```dep ensure```

(6) Build and test
    
  ```bash
go clean;go build
```
