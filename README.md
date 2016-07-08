# drone-ui

This project contains the source code for the drone user interface. The generated javascript and css assets are embedded into a Go source file which is imported into the main drone application, using `go get`.

This is currently being tested with `node v4.4.7`

## Developing

To compile the source and create minified css and javascript assets:

```bash
npm install
npm run build
```

To watch for changes and (re)create css and javascript assets:

```bash
npm run watch
```

## Running

To test the user interface with Drone we have created a simple proxy server. This will proxy requests from the react application to a real Drone instance. Before running the proxy server you must download dependencies:

```
go get github.com/drone/drone-go/drone
go get github.com/koding/websocketproxy
```

To run the proxy server you must provide the location of your drone server (scheme and hostname) and your Drone API token for authentication. You can get your Drone API token from your profile page.

```
go run server.go --scheme <drone scheme> \
                 --host   <drone host> \
                 --token  <drone api token>
```

When the server is running you can open the following url in your browser:

```
http://localhost:9000
```

__Note__ this proxy server currently requires front-end developers have Go installed and configured. We are interested in contributions that replace the Go implementation with a pure javascript implementation, limiting this potential barrier to entry.

## Bundling

To bundle and embed the code in a Go source file install the following command line utilities:

```bash
go get github.com/jteeuwen/go-bindata/...
go get github.com/elazarl/go-bindata-assetfs/...
```

To generate the Go source file run the following command:

```bash
npm run embed
```

__Note__ that for security reasons we will not accept a pull request that updates embedded Go asset file since we are not able to easily review the embedded, minified code. This file is instead automatically generated by our build server to prevent tampering.
