go-push-server
[![Build Status](https://travis-ci.org/dougt/go-push-server.png)](https://travis-ci.org/dougt/go-push-server.png)

==============

Simple Push Server in Go
https://wiki.mozilla.org/WebAPI/SimplePush
https://wiki.mozilla.org/WebAPI/SimplePush/Protocol


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

To test:
```
  git submodule update
  cd simplepush_test
  make
  bin/python bin/activate_this.py
  bin/python smoke_test.py
  bin/python run_all.py
```
The tests assume that the push server is running as the
default port number and not running TLS


To test WebSockets with TLS, you will need a certificate. Here are simple
instructions to create your own self-signed certificate for testing:

http://www.akadia.com/services/ssh_test_certificate.html

TLS TL;DR?
```
  openssl genrsa -des3 -out test.key 1024
  openssl req -new -key test.key -out test.csr
  cp test.key test.key.orig
  openssl rsa -in test.key.orig -out test.key
  openssl x509 -req -days 365 -in test.csr -signkey test.key -out test.crt
```

Then edit your `config.json` to enable TLS and point to your test certificate:
```
  "useTLS"           : true,
  "certFilename"     : "test.crt",
  "keyFilename"      : "test.key"
```

Because your certificate is self-signed, no push client will trust it yet. Open
https://yourtestservername:8080/admin (*https*!) on your push client and, when
prompted, accept the certificate and add a permanent exception.
