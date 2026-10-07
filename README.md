# OTP Live Display

A single-page, animated 6-digit OTP display. It receives a code dynamically via:

- URL query param: `?otp=123456`
- `window.postMessage({ type: "otp", code: "123456" }, "*")`
- The JS global `OTP.set("123456")`
- A **live WebRTC data channel** (NAT traversal via Google STUN
  `stun:stun.l.google.com:19302`) with manual copy-paste signaling

## WebRTC flow (this page = receiver)

1. The sender (e.g. the Flutter app) creates an **offer** and a data channel.
2. Paste that offer into the page and click **Generate answer**.
3. Copy the generated **answer** back into the sender.
4. Once connected, the OTP streams in live and fills the boxes.

No signaling server is required — only Google STUN for NAT traversal.

## Hosting

The page is a static `index.html`, suitable for GitHub Pages or any static host.
