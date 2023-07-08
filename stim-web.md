#stimstore #stim-web

Stim-Web is the frontend web service that handles all the client-side interactions for stimstore

Stack:
NextJS (may be subject to change)
Typescript
TailwindCSS
Zustand Atomic Store

Stim-Web will only EVER communicate with [[stim-core|Stim-Core]]. It should never have the keys to authenticate with other services. 

Stim-Web will not include a server-key. It will only authenticate with the server via user [[session tokens]]. Anonymous access routes like [[GET]]ing [[Core.Items|/items]] are acceptable without a key

