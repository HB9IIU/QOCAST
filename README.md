# QOCAST

**Browser-controlled QO-100 DATV transmit and receive console for Windows**, by HB9IIU.

QOCAST sends DVB-S2 video to the QO-100 satellite with an ADALM-Pluto
(PlutoDVB2 firmware by F5OEO), and shows what comes back with a MiniTiouner or
PicoTuner - all from one page in your browser.

## Download

Get the latest `QOCast-Portable-x64.zip` from the **[Releases](../../releases)** page.
No installation: unzip it to a writable folder and run `START-QOCAST.cmd`.

## Features

- **Sources:** testcards with melody (SBB clock, station card with marquee,
  classic test card), webcam with microphone, iPhone camera with Moblin, OBS,
  video files
- **Settings that fit:** every film, camera, Moblin or OBS source is checked
  once per profile, so the stream fits the QO-100 bitrate without overflows
- **BATC wideband spectrum:** click a free (green) slot to choose your frequency
- **Start, then PTT:** the stream runs muted until you press PTT
- **Local Pluto RX spectrum:** see your own carrier
- **On-air monitor:** your own picture received back through QO-100
- **RX page:** watch QO-100 in the browser, click a signal to tune
- **Overlays** on camera and Moblin: callsign, locator, UTC time, scrolling text
- **Stream analysis:** live TR 101 290 checks and bitrate breakdown

## Requirements

- Windows 10 or 11, 64-bit
- An **NVIDIA graphics card** (the video is encoded with NVENC, H.265)
- **ADALM-Pluto** with the **PlutoDVB2 firmware** (F5OEO), connected by USB
- Optional, for receiving: a **MiniTiouner** or **PicoTuner** with its FTDI
  driver installed in Windows, and an LNB for the QO-100 downlink

## Starting and quitting

1. Run `START-QOCAST.cmd` (or `QOCast.exe`). The page opens in your browser at
   http://localhost:8080. OpenTuner starts minimized and connects your tuner by
   itself.
2. Set your callsign and locator on the **Setup** page.
3. To end: the **Quit** button at the top of the page.

Other devices on your network can use `http://<this-PC-address>:8080`.

## Included third-party software

QOCAST ships with FFmpeg, TSDuck, the Varela Round font and the HB9IIU QOCAST
OpenTuner (based on OpenTuner by Tom ZR6TG, GPLv3). Their licences are in the
`licenses` folder.

## Credits

- **Evariste F5OEO** for the PlutoDVB2 firmware
- **Tom ZR6TG** for OpenTuner
- **F1EJP** for DATV-Easy, the reference for the encoder settings
- **BATC** for the QO-100 wideband spectrum monitor
- **AMSAT-DL** and everyone who keeps QO-100 running

73 from HB9IIU!
