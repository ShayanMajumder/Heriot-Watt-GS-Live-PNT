# Heriot-Watt GS — live PNT

Live view of a ground-station receiver for the **Anthorn eLoran** transmitter (100 kHz, GRI 6731) and the
**MSF** time signal (60 kHz), compared against GPS.

**Live page:** https://shayanmajumder.github.io/Heriot-Watt-GS-Live-PNT/

What the page shows:

- eLoran, MSF and GPS time side by side (UTC)
- the eLoran signal over one GRI (master and secondary pulse groups) and its SNR
- the MSF time code as it arrives, second by second, with the decoded date and time
- messages from the eLoran data channel (Eurofix: UTC time, GPS corrections, station data)
- eLoran − GPS over the last hour, with the fixed delay removed
- Anthorn and the ground station on a map

## How it works

The receiver (a USRP B210 with a GPS-disciplined oscillator and an LF up-converter) runs on a computer at the
ground station. Once a second it publishes a JSON snapshot to the public MQTT broker `broker.hivemq.com` over
secure WebSockets. This page is static: it subscribes to that broker in your browser and draws the snapshots.
No server is involved here, and nothing connects to the ground station.

When the receiver is not running, the page says so and shows the time of the last update.

Data published to a public broker can be read, and written, by anyone. The page treats every value as
untrusted: it is displayed as text, never run.

Options in the address: `?theme=light` or `?theme=dark`, and `?broker=wss://…&topic=…` to read another feed.

Map: [Natural Earth](https://www.naturalearthdata.com/) (public domain).
MQTT client: [MQTT.js](https://github.com/mqttjs/MQTT.js) 5.10.1, loaded from jsDelivr with an integrity check.
