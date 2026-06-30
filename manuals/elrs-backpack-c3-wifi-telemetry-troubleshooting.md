# ELRS Backpack C3 Wi-Fi Telemetry Troubleshooting

ExpressLRS Backpack `1.5.7` includes CRSF telemetry over Wi-Fi UDP broadcast, which is the normal firmware path recommended in the main setup guide. A later patch for some ESP32-C3 based TX backpack targets was merged into Backpack `master`, but it is not included in `1.5.7`.

On affected targets, setting **Telemetry** to `WiFi` in Normal link mode may not start or connect Wi-Fi. The upstream PR explains that on C3 devices, not calling `SetSoftMacAddress` before entering Wi-Fi mode can cause serial TX to stop working and Wi-Fi to fail to start correctly, which can break backpack functionality.

The upstream references are:

- [ExpressLRS Backpack PR #219](https://github.com/ExpressLRS/Backpack/pull/219)
- [ExpressLRS Backpack issue #217](https://github.com/ExpressLRS/Backpack/issues/217)
- [Fix commit `2c863af`](https://github.com/ExpressLRS/Backpack/commit/2c863afb46e832290d48b1c9a95969612cb2b8d6)

## Option 1: Flash `master` with ExpressLRS Configurator

Flash the current Backpack `master` branch if you want the merged fix instead of using the temporary workaround.

1. Open **ExpressLRS Configurator**.
2. Open **Settings** and enable **Expert Mode**.
3. Select **Backpack** in the left-side menu.
4. Change **Git branches** to `master`.
5. Select your TX backpack target.
6. Set the Backpack Home Wi-Fi **SSID** and **password** to your home network or phone hotspot.
7. Flash that build to the backpack.

<p float="left">
  <img src="images/elrs-expert-mode.png" alt="ExpressLRS Configurator with Expert Mode enabled" width="35%" />
  <img src="images/elrs-master-branch.png" alt="ExpressLRS Configurator with the Backpack Git branch set to master" width="35%" />
</p>

## Option 2: Flash `master` with ExpressLRS Web Flasher

You can also use the official ExpressLRS Web Flasher:  
[https://expresslrs.github.io/web-flasher/](https://expresslrs.github.io/web-flasher/)

1. Click **Transmitter Module**.
2. Enable the **Branches** toggle.
3. Select the `master` branch.
4. Select your TX backpack target.
5. Set the Backpack Home Wi-Fi **SSID** and **password** to your home network or phone hotspot.
6. Flash the backpack.

<img src="images/elrs-web-flasher-master-branch.png" alt="ExpressLRS Web Flasher showing Transmitter Module with Branches enabled and master selected" width="60%" />

## Option 3: Use the temporary Link Mode workaround

If you want to stay on release firmware, you can trigger Wi-Fi by briefly switching the backpack into MAVLink mode. In the reported cases, MAVLink mode starts Wi-Fi immediately. After Wi-Fi is running, switching back to Normal mode keeps the connection alive for CRSF telemetry.

1. Power on the radio and make sure it is connected to the receiver or aircraft.
2. Open the **ExpressLRS** Lua script on the radio.
3. Go to **Backpack**.
4. Set **Link Mode** to `MAVLink`.
5. Set **Telemetry** to `WiFi`.
6. Wait for the backpack Wi-Fi to start or connect to the configured Home Wi-Fi.
7. Set **Link Mode** back to `Normal`.
8. Leave **Telemetry** set to `WiFi`.

This workaround needs to be repeated after power cycling the backpack. SquirrelCast currently receives CRSF telemetry only, so switch back to `Normal` before using the app.

If the workaround still does not start Wi-Fi, make sure the Backpack Home Wi-Fi **SSID** and **password** were set while flashing, and avoid special characters in the hotspot name and password.
