# PARVOX Smart Control — starter app

This is an installable Progressive Web App (PWA) source project, not a compiled Android APK.

## What it currently does
- Premium black/silver interface.
- Web Bluetooth connection to a device named `PARVOX CONTROL`.
- Sends text commands for RGB colour, brightness, LED modes and volume.
- Receives battery telemetry notifications if firmware exposes the battery characteristic.
- Audio pairing is done separately in Android Bluetooth settings using the ESP32 A2DP device name.

## Important hardware/firmware requirements
1. The ESP32-WROOM-32 must run compatible firmware supporting Bluetooth Classic A2DP and BLE GATT concurrently.
2. BLE service UUID: `12345678-1234-1234-1234-123456789000`
3. BLE write characteristic UUID: `12345678-1234-1234-1234-123456789001`
4. BLE battery notify characteristic UUID: `12345678-1234-1234-1234-123456789002`
5. Advertise the BLE controller name as `PARVOX CONTROL`. The audio A2DP name can be `PARVOX`.
6. The app sends `VOL:0` through `VOL:100`, but this only changes actual audio volume when firmware connects that command to a compatible digital audio volume controller in the audio path. TPA3110 alone cannot do this.
7. Battery notifications should be text such as `BAT:11.8;BATPCT:65`. The percentage must be calculated and calibrated for the actual 3S battery. Do not treat a voltage estimate as an accurate state-of-charge gauge.
8. LED commands: `COLOR:r,g,b`, `BRIGHT:n`, `MODE:RAINBOW`, `MODE:BREATH`, `MODE:STATIC`, `LED:OFF`.

## Run and install on Android
Web Bluetooth requires a secure context (HTTPS) and a supported browser, typically Chrome on Android.
- Host these files on an HTTPS static host.
- Open the HTTPS URL in Chrome on Android.
- Use Chrome menu > Add to Home screen / Install app.
- Pair the audio endpoint `PARVOX` separately in Android Bluetooth settings.
- Open the installed PARVOX app and connect to `PARVOX CONTROL`.

Opening `index.html` directly from local file storage will generally not allow Web Bluetooth.

## Not included
- A compiled APK.
- Matching ESP32 firmware for concurrent A2DP + BLE, battery notification and external volume-processor integration.
- Actual DSP equalization. The equalizer card is informational until compatible DSP hardware and firmware are added.

## Customisation
Edit `index.html` to change branding, colours, layout and controls. Keep the UUIDs and command strings aligned with the ESP32 firmware.
