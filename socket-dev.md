### Http server
- create a tcp socket connection on port
- bind a listen to server
- create a loop for accepting different connections
- for each connection read avilable sockets
- read socket content
    - handle new connection
        - accept socket
        - add socket to a list
    - handel requests
        - read request data
        - parse http

## handeling handshake
- check for request endpoint (eg: /ws or /websocket or /socket.io)
- check for valid handshake
    - check for version (above 1.1)
    - check if 'upgrade' header exist and is eq 'websocket'
    - check if 'conection' header exist and is eq 'Upgrade'
    - store web-socket-key from 'sec-websocket-key' header
- generate new websocket key
    - append magic uuid to key '258EAFA5-E914-47DA-95CA-C5AB0DC85B11'
    - hash new key with sha1
    - encode to base64
- return a response ('HTTP/1.1 101 Switching Protocols\r\n'+'Upgrade: websocket\r\n'+'Connection: Upgrade\r\n'+Sec-WebSocket-Accept: `newkey`\r\n')

## handle websocket frame