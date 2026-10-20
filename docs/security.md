# Local API security

The API listens on the LAN, so any device on the network, and any web page open in a browser on the network, can reach it. Rules:

1. **Pairing.** A client requests pairing; the TV shows a 6-digit code; the client submits it and receives a long random token. Tokens are listed and revocable in settings.
2. **Token on every state-changing request**, sent as `Authorization: Bearer`. Never accept cookies alone (blocks cross-site request forgery from web pages).
3. **Host header check.** Reject requests whose `Host` is not one of the device's own names (`openstick.local`, the configured name) or IP addresses (blocks DNS rebinding).
4. **CORS.** No wildcard. Allow only the device's own web UI origin.
5. **Rate-limit pairing attempts**; lock out after repeated wrong codes.
6. **Guest senders** never get an API token; they only reach casting receivers, and only while guest mode is on.
