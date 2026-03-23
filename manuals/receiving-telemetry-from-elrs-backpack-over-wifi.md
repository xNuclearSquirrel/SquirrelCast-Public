# Receiving Telemetry From the ELRS Backpack Over Wi-Fi

To use ELRS telemetry with SquirrelCast, first make sure the ELRS backpack is enabled on your TX module.

For the initial backpack setup, follow the official ExpressLRS guide:  
[Flashing via WiFi](https://www.expresslrs.org/hardware/backpack/backpack-tx-setup/#flashing-via-wifi)

It is recommended to set the Backpack Home Wi-Fi SSID and password to match your phone hotspot. This makes it easier for the backpack to connect automatically later.

SquirrelCast currently receives **CRSF telemetry over Wi-Fi UDP broadcast** from the TX backpack. The phone and the backpack need to be on the same Wi-Fi network.

## Flash the master branch

At the time of writing, this feature is available on the `master` branch and is not yet part of the stable Backpack release used for this guide. To use it now, flash the newest `master` build to the TX backpack.

1. Open **ExpressLRS Configurator**.
2. Open **Settings** and enable **Expert Mode**.
3. Select **Backpack** in the left-side menu.
4. Change **Git branches** to `master`.
5. Flash that build to the backpack.

<p float="left">
  <img src="images/elrs-expert-mode.png" alt="ExpressLRS Configurator with Expert Mode enabled" width="35%" />
  <img src="images/elrs-master-branch.png" alt="ExpressLRS Configurator with the Backpack Git branch set to master" width="35%" />
</p>

As an alternative, you can also use the official ExpressLRS Web Flasher:  
[https://expresslrs.github.io/web-flasher/](https://expresslrs.github.io/web-flasher/)

In the Web Flasher:
1. Click **Transmitter Module**.
2. Select your TX backpack target.
3. Enable the **Branches** toggle.
4. Select the `master` branch.
5. Flash the backpack.

<img src="images/elrs-web-flasher-master-branch.png" alt="ExpressLRS Web Flasher showing Transmitter Module with Branches enabled and master selected" width="60%" />

> **Note:** This page should be updated once a Backpack release includes this change.

## Current protocol support

MAVLink support has not been added to SquirrelCast yet, but it is planned. For now, telemetry over Wi-Fi works only when your radio link is using the **CRSF** protocol.
