# QOCAST

**Browser-controlled QO-100 DATV transmit and receive console for Windows**, by HB9IIU.

QOCAST sends DVB-S2 video to the QO-100 satellite with an ADALM-Pluto
(PlutoDVB2 firmware by F5OEO), and shows what comes back with a MiniTiouner or
PicoTuner. You control everything from one page in your browser; the received
picture plays in its own small window, the **QOCAST Player**.

![QOCAST main page](images/screenshot.png)

## What's new in 0.3.2

- **Pluto frequency correction:** after each transmission via QO-100, QOCAST
  compares your signal with the beacon and corrects your Pluto's frequency, so
  it transmits right on your slot (a Pluto is often 10-50 kHz off at 2.4 GHz).
- **The LNB is followed automatically** on the beacon; every correction is
  announced on the page.
- **Your own signal is found by itself** after PTT, no more clicking.
- The received station on two lines next to "Configure signal" (with the
  provider name), and a tidier header.

## What's new in 0.3

- **LNB calibration:** the Setup page shows your LNB's real oscillator
  frequency. **Recalibrate** locks on the QO-100 beacon five times and corrects
  it, in about 30 seconds.
- **Local mode:** try the whole chain without the satellite. The receiver
  listens to your Pluto directly on 2.4 GHz (small antenna on the tuner, LNB
  power off), and the spectrum shows your signal simulated at your slot, as
  high as your TX power.
- **Sound meter** on the camera picture: one small bar showing the sound as it
  is sent.
- **Sound offset** for the camera (Setup): if your sound comes after the
  picture, enter how much, and it is corrected for every viewer.
- **Signal health warns** when the picture falls behind (a growing delay) or
  the stream has no sound.
- **More reliable reception of your own signal** when you press PTT.
- **tx_log.csv:** one line per transmission with your own signal as received
  (frequency error, MER, Pluto temperature), to see whether your Pluto's
  frequency error is reproducible.

## What's new in 0.2: no more video in the browser

In 0.1, received video was shown inside the web page: OpenTuner received the
signal, QOCAST converted it to a format browsers can play, and the page played
it. It worked, but it was never good enough for DATV. The picture lagged
seconds behind, stalled, and every change of station or resolution meant
starting over. Browser video players are made for internet streaming, with
large buffers. A live picture from the satellite needs the opposite.

So 0.2 drops that idea completely:

- **New: the QOCAST Player.** A small window that plays the tuner's stream
  directly with VLC: picture and sound, no conversion and no browser in
  between. The picture appears about a second after tuning. QOCAST starts it,
  it finds your MiniTiouner or PicoTuner by itself, and it closes at Quit.
  Right-click the picture for mute, volume and "always on top".
- **OpenTuner is no longer needed.** It is not in the package any more, and
  QOCAST closes an OpenTuner that is still running, so it can't keep the tuner
  busy. The Player uses OpenTuner's proven tuner code (thanks, Tom ZR6TG).
- **Receive from the main page.** The separate RX page is gone. Click a signal
  on the BATC spectrum to receive it: a green band marks it, with the station's
  callsign once locked. A line next to "Configure signal" shows lock, MER,
  D margin and MODCOD. At start, the receiver is on the QO-100 beacon.
- **TX monitor (was "On-air monitor").** While you stream, it shows a small,
  live **TX preview** of the encoded picture you actually send to the Pluto,
  already before PTT. Below it, your signal received back through QO-100, with
  MER and D margin.
- **Smaller download:** about 130 MB instead of more than 300 MB.

Also new: a built-in BATC wideband chat, a camera preview that recovers by
itself when the webcam gives no picture, a microphone compressor for the
camera, and clearer messages in the log. The full list is on the
**[Releases](../../releases)** page.

## What makes QOCAST different

Like other DATV tools, QOCAST starts from a table of encoder settings for each
symbol rate and FEC (picture size, bitrates, audio). But a fixed table only fits
"average" pictures: a detailed film or a busy camera scene can need more than
the profile carries, and the stream overflows - viewers see glitches.

So QOCAST **tests what you actually send**, and adapts the settings to it:

- **Films:** at the first Start with a profile, QOCAST finds the three hardest
  30-second parts of the film, encodes them with the exact transmit command, and
  steps down only as far as needed (NVENC multipass, then a smaller picture, then
  fewer frames per second) until the stream has no overflows and keeps spare room.
  If there is room left over, the video gets more bitrate. The result is saved
  next to the film: the next Start is immediate.
- **Camera, Moblin and OBS:** a 20-second test, per profile, with your own scene
  (your room, your light, your phone in your hand), then the same check.
- **Testcards:** the moving ones (SBB clock, station card with marquee) are
  shipped with settings already tested for every profile.
- **On air:** QOCAST keeps watching. If a film still overflows, it is checked
  again, more carefully, at its next Start; for live sources the page says so.

Also built in:

- **Signal health at a glance:** one line tells you if your stream is good, too
  full or has errors, with a live bitrate bar (video, audio, overhead, spare) and
  TR 101 290 checks behind it.
- **See yourself come back:** while you stream, the QOCAST Player is tuned to
  your downlink, so you see your own picture received back through QO-100.
- **Start, then PTT:** the stream starts muted; the Pluto only transmits when
  you press PTT.
- **Moblin and OBS stay connected:** connect them once; start and stop the
  transmission as often as you like without touching the phone or OBS.
- **Use it from any device:** open `http://qocast.local:8080` on a tablet,
  phone or another PC on your home network.
- **Nothing to install or configure:** unzip and start. The QOCAST Player
  starts with QOCAST, finds your tuner by itself and closes at Quit.

## Download

Get the latest `QOCast-Portable-x64.zip` from the **[Releases](../../releases)** page.
No installation: unzip it to a writable folder and run `CLICK-HERE-TO-START.cmd`.

## Features

- **Sources:** testcards with melody (SBB clock, station card with marquee,
  classic test card), webcam with microphone, iPhone camera with Moblin, OBS,
  video files
- **Settings that fit:** every film, camera, Moblin or OBS source is checked
  once per profile, so the stream fits the QO-100 bitrate without overflows
- **BATC wideband spectrum:** click a free (green) slot to choose your
  frequency, click a signal to receive it
- **QOCAST Player:** the received picture and sound in their own window
- **Start, then PTT:** the stream runs muted until you press PTT
- **TX monitor:** live preview of what you send, and your signal received back
- **Local Pluto RX spectrum:** see your own carrier
- **LNB calibration** on the QO-100 beacon, and a **Local mode** to test
  without the satellite
- **Overlays** on camera and Moblin: callsign, locator, UTC time, scrolling text
- **Signal health:** status in words, live bitrate bar, TR 101 290 checks
- **BATC wideband chat** built in
- **Help page:** step-by-step setup of Moblin and OBS, receiving a station

## Requirements

- Windows 10 or 11, 64-bit
- An **NVIDIA graphics card** (the video is encoded with NVENC, H.265)
- **ADALM-Pluto** with the **PlutoDVB2 firmware** (F5OEO), connected by USB
- Optional, for receiving: a **MiniTiouner** or **PicoTuner** with its USB
  driver installed in Windows, and an LNB for the QO-100 downlink

## Starting and quitting

1. Run `CLICK-HERE-TO-START.cmd` (or `QOCast.exe`). The page opens in your browser at
   http://localhost:8080, and the QOCAST Player window opens on the QO-100
   beacon.
2. Set your callsign and locator on the **Setup** page.
3. To end: the **Quit** button at the top of the page.

Other devices on your network can use `http://qocast.local:8080` (or
`http://<this-PC-address>:8080`). There is no password: anyone on your home
network can open it.

## Included third-party software

QOCAST ships with FFmpeg (LGPL 2.1, with the Fraunhofer FDK AAC encoder),
TSDuck, the Varela Round font, and the QOCAST Player. The Player contains
tuner code from OpenTuner by Tom ZR6TG and is therefore GPLv3; it plays video
with LibVLC by VideoLAN (LGPL 2.1). The licences are in the `licenses` folder.

Source code of the QOCAST Player:
**[github.com/HB9IIU/QOCAST-OpenTuner](https://github.com/HB9IIU/QOCAST-OpenTuner)**

## Credits

- **Evariste F5OEO** for the PlutoDVB2 firmware
- **Tom ZR6TG** for OpenTuner, whose tuner code the QOCAST Player uses
- **VideoLAN** for VLC
- **F1EJP** for DATV-Easy, the reference for the encoder settings
- **BATC** for the QO-100 wideband spectrum monitor and chat
- **AMSAT-DL** and everyone who keeps QO-100 running

73 from HB9IIU!
