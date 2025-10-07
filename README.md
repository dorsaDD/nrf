# Wearable MVP (nRF52840DK + nRF Connect SDK / Zephyr)

This is a minimal skeleton for your internship project. It compiles on **nRF52840DK (PCA10056)** using **nRF Connect SDK** (Zephyr).

## Features
- Threaded architecture: radio, sensor, and timer threads print lifecycle messages.
- Timer thread simulates periodic physiological sampling (currently every 10s).
- BLE advertising with device name `Wearable` (no GATT yet).
- Power-friendly structure (no busy loops; threads sleep).

## Prerequisites
- Install **nRF Connect SDK** (recommended v2.6.x or later) via *nRF Connect for Desktop → Toolchain Manager* or CLI.
- Have a nRF52840DK connected over USB.

## Build & Flash
```bash
# From your NCS workspace root (where 'west' works)
west build -b nrf52840dk/nrf52840 wearable_mvp/app -p
west flash
```

Open a serial console to view logs, or use RTT after you enable it later.

## Project Layout
```
wearable_mvp/
├─ app/
│  ├─ CMakeLists.txt
│  ├─ prj.conf
│  ├─ boards/
│  │  └─ nrf52840dk_nrf52840.overlay
│  └─ src/
│     ├─ main.c
│     ├─ threads.c
│     ├─ radio.c
│     └─ power.c
└─ README.md
```

## Next Steps
- Replace timer period with `K_HOURS(1)` after testing.
- Add accelerometer GPIO interrupt and I2C driver bring-up.
- Create a custom GATT service or use NUS for data uplink.
- Tighten power: disable UART console, use RTT, and device runtime PM.
