# PostMessage Communication POC

This project demonstrates how to use the `postMessage` method in JavaScript to send and receive messages between two browser windows (or a window and a popup).

## Overview

The project consists of two HTML files:

- **start.html**: This file acts as the sender. It opens a popup window and sends a message to it.
- **index.html**: This file acts as the receiver. It listens for messages from other windows and displays the received data on the screen.

## How It Works

1. **Sender (start.html):**
   - Opens a popup window to a specified URL (`game_url`).
   - Sends a message to the popup window with JSON data that includes a user's readiness and name.
   - The message is sent after a short delay of 1 second to ensure the popup window is fully loaded.

2. **Receiver (index.html):**
   - Listens for incoming messages via the `postMessage` event.
   - When a message is received, it checks if the `readyToPlay` flag is `true`.
   - If `readyToPlay` is `true`, it updates the UI to reflect the readiness of the user and personalizes the message with the user's name.

## Files

- **start.html**: This file includes a button that, when clicked, opens a new window and sends a message containing the user's name and a readiness flag.
- **index.html**: This file receives the message from the popup and displays a personalized message on the screen.

## How to Use

1. Open `start.html` in your browser.
2. Click the "Start" button. This will open a new window pointing to `index.html` (make sure the URL in the `game_url` variable is correctly set).
3. After 1 second, a message will be sent from the sender (popup window) to the receiver (parent window).
4. The message will update the content in the popup window based on the data sent from the sender.

## Key Concepts

- **`postMessage`**: Allows secure communication between windows (parent window and popup) or between different domains.
- **`window.open`**: Opens a new browser window or tab.
- **Event Handling**: The receiver listens for the `message` event and processes the incoming data.

## Security Considerations

It is essential to verify the origin of the message (using `e.origin`) to ensure that messages are only accepted from trusted domains. This is currently commented out for testing purposes, but in a production environment, this step should be enabled to prevent Cross-Site Scripting (XSS) attacks.

```javascript
if (e.origin !== "http://yourtrustedsite.com") {
    console.log('Untrusted origin:', e.origin);
    return;
}
```

## Technologies
- HTML5
- JavaScript (postMessage API)