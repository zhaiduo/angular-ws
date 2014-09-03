# angular-ws
[![Build Status](https://travis-ci.org/neoziro/angular-ws.svg?branch=master)](https://travis-ci.org/neoziro/angular-ws)
[![Dependency Status](https://david-dm.org/neoziro/angular-ws.svg?theme=shields.io)](https://david-dm.org/neoziro/angular-ws)
[![devDependency Status](https://david-dm.org/neoziro/angular-ws/dev-status.svg?theme=shields.io)](https://david-dm.org/neoziro/angular-ws#info=devDependencies)

WebSocket service for Angular.js.

## Install

```
bower install angular-ws
```

## Usage

```js
angular.module('app', ['ws'])
.config(function (wsProvider) {
  wsProvider.setUrl('ws://echo.websocket.org');
})
.controller('WebSocketCtrl', function ($scope, ws) {
  ws.connect();

  ws.$on('message', function (msg) {
    // ...
  });

  ws.send('custom message');
});
```

### Provider

#### wsProvider.setUrl(url)

Set the url of the WebSocket.

```js
wsProvider.setUrl('ws://echo.websocket.org');
```

#### wsProvider.setProtocols(protocols)

Set the protocols used by the WebSocket.

```js
wsProvider.setProtocols(['protocol']);
```

### Service

#### ws.connect([config])

Connect the WebSocket, you can provide a custom config.

```js
ws.connect({
  url: 'ws://echo.websocket.org',
  protocols: ['protocol']
})
.then(function () {
  $log.debug('WebSocket is connected.');
}, function () {
  $log.debug('An error occurs during WebSocket connection.');
});
```

#### ws.getReadyState()

Get the ready state of the WebSocket.

```js
ws.getReadyState() // WebSocket.CLOSED, WebSocket.OPEN...
```

#### ws.on(event, listener)

Listen an event on the WebSocket, the function is already wrapped in `$rootScope.$apply()`.

```js
ws.on('message', function (event) {
  $log.info('New message', event.data);
});
```

#### ws.close()

Close the connection of the WebSocket.

```js
ws.close();
```

## License

MIT