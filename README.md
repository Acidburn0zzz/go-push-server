go-push-server
==============

Simple Push Server in Go
https://wiki.mozilla.org/WebAPI/SimplePush

To build:
```
  cd go-push-server
  GOPATH=$PWD go build mozilla.org/push
```

To run:
```
  cp config-example.json config.json
  # ... edit config.json if required
  ./push
```
