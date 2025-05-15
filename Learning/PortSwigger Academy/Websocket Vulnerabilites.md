WebSockets are widely used in modern web applications. They are initiated over HTTP and provide long-lived connections with asynchronous communication in both directions. 
You can use Burp Suite to:

- Intercept and modify WebSocket messages.
- Replay and generate new WebSocket messages.
- Manipulate WebSocket connections.

**Common Web Sockets Vulnerabilities : -**
- User-supplied input transmitted to the server might be processed in unsafe ways, leading to vulnerabilities such as SQL injection or **XML external entity** injection.
- Some blind vulnerabilities reached via WebSockets might only be detectable using out-of-band (OAST) techniques.
- If attacker-controlled data is transmitted via WebSockets to other application users, then it might lead to XSS or other client-side vulnerabilities.

A good example would be : - 
For example, suppose a chat application uses WebSockets to send chat messages between the browser and the server. When a user types a chat message, a WebSocket message like the following is sent to the server:

`{"message":"Hello Carlos"}`
The contents of the message are transmitted (again via WebSockets) to another chat user, and rendered in the user's browser as follows:
`<td>Hello Carlos</td>`
In this situation, provided no other input processing or defenses are in play, an attacker can perform a proof-of-concept XSS attack by submitting the following WebSocket message:
`{"message":"<img src=1 onerror='alert(1)'>"}`


Some WebSockets vulnerabilities can only be found and exploited by manipulating the WebSocket handshake. These vulnerabilities tend to involve design flaws, such as:

- Misplaced trust in HTTP headers to perform security decisions, such as the                    **`X-Forwarded-For`** header.
- Flaws in session handling mechanisms, since the session context in which WebSocket messages are processed is generally determined by the session context of the handshake message.
- Attack surface introduced by custom HTTP headers used by the application.


##### My Experience with the Lab Manipulating WebSocket Handshakes 

So I had a lot of trouble solving this lab because the WAF will immediately blacklist my IP if I try to access it. 
I had to leverage the **X-Forwarded-For** for this. 
Steps are : - 
1. Initiated a Live Chat and hence a websocket opened up.
2. Then sent it to repeater.
3. Tried a basic payload to invoke the alert.
4. The WAF blocks the IP and I couldn't connect.
5. Then I used `X-Forwared-For: 1.1.1.X`
6. Then tried a basic payload : - `<iframe src="javascript:alert(1)"></iframe>`
7. But didn't work and got blocked again. Then again from Step 5 tried.
8. Finally the payload  worked : -
```
<iframe src="javascript:alert`1`"></iframe>

```

