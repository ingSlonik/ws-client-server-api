# WebSocket Client Server API

Create WebSocket API server and client implementation without mistakes.

## Support
* Node.js server
* Browser
* react
* react-native

## API definition

Define types to file for client and server in one file api.d.ts.
```js
import { APIWatch, APIAction } from "ws-client-server-api";

export type APIWatches = {
  watchUser: APIWatch<{ userId: string }, null | User>,
  watchUsers: APIWatch<{}, User[]>,
};

export type APIActions = {
  addUser: APIAction<Omit<User, "id">>,
  updateUser: APIAction<User>,
  removeUser: APIAction<{ userId: string }>,
};
```

## React / react-native

```js
import { clinet } from "ws-client-server-api";

import { APIWatches, APIActions } from "./api";

const { actionWS, useWS } = client<APIWatches, APIActions>("ws://localhost:8080");

function MyComponent({ userId }: { userId: string }) {
  const user = useWS("watchUser", { userId });

  function handleRemove() {
    actionWS("removeUser", { userId });
  }

  return <View>....</View>;
}
```

## Node.js server

```js
import WebSocket, { WebSocketServer } from "ws";
import { server } from "ws-client-server-api";

import { APIWatches, APIActions } from "./api";

const wss = new WebSocketServer({ port: 8080 });

server<APIWatches, APIActions>(wss, {
  watchUser: async (cb, { userId }) => {
    const users = getUserFromDB(userId);
    return user;
  },
  watchUsers: async (cb, {}) => {
    const users = getUsersFromDB();
    return users;
  },
}, {
  addUser: async (cd: user) => {
    
  },
  updateUser: async (cd: user) => {
    
  },
  removeUser: async (cd: userId) => {
    
  },
});
```
