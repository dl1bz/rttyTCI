# rttyTCI - RTTY application using TCI Audio for macOS

<img src="https://github.com/dl1bz/rttyTCI/blob/master/stuff/rttyTCI_screenshot.png" width="1024px" />

rttyTCI is a RTTY (Radio Teletype) application for use in hamradio. Only TCI Audio streaming is supported, means a working TCI server is required. Classical analogue audio input and output via soundcard interfaces isn't and won't be supported.

### What is TCI ?

TCI - Transceiver Control Interface was mainly developed by Expert Electronics for a simple and still advanced connection between the ExpertSDR2/3 and third-party software. TCI has all required control commands similar to the CAT system, but even more, it can transfer IQ-streams from the ExpertSDR2/3 to clients (third-party software such as signal Skimmers, etc.) via the local network and the Internet, CW macros, and Audio In/Out streams for digital modes. TCI is the universal multi-client interface (you can connect it to radio Loggers, Skimmers, PAs, antenna switches, etc. at the same time). It was developed as an open protocol to use with multi-band transceivers, which support one, two, or multiple receivers/transmitters. This is a game-changer for the SDR radio! It is an open-source protocol, we've discussed using it with hardware and accessory developers. For example, a Band Pass Filters unit with a LAN interface can get information about radio frequency via LAN and can switch filters, the same applies to antenna switches and PAs, and so on. Several software developers are already working on the implementation of TCI in their software, we'll get TCI into all HAM software.

In the meantime a lot of other SDR host applications, like Thetis and my [deskHPSDR](https://github.com/dl1bz/deskhpsdr), provide a TCI Server too.

### Requirements

* ARM based Mac (M-series) running macOS 26.x "Tahoe"
* working TCI Server with TCI audio streaming support, follow the TCI 2.0 standard
* Hamradio transceiver equipment for receiving and sending RTTY signals
* optional: logging application with support for FlexRadio/ADIF logdata transfer via UDP

### Using rttyTCI

rttyTCI is current in development state "early development", far away from "release" or "production release", so issues are possible.

* receive and decoding RTTY signals work
* encoding and transmit RTTY signals work
* macro support and text templates included
* options for adjust RTTY operation available
* send log data to a supported hamradio log application work (format FlexRadio/ADIF via UDP)

I run rttyTCI in RTTY operation successful with my deskHPSDR by using mode DIGL and 2210Hz Offset via TCI audio streaming and TCI CAT. SDR device was a Brick2 SDR transceiver, connected via Ethernet by running OpenHPSDR protocol P2. I made about 10 real QSOs in mode RTTY for tesing, all was working like expected.

TCI Audio stream need the following parameter, equal to other apps like JTDX, MSHV or WSJT-X:

Sample Format:  float32 (no other sample_formats supported)
Channels:       1 / mono
Sample Rate:    48000 Hz (no other sample_rates supported)
Block Size:     512 Samples

Recommended app setup running RTTY in hamradio with rttyTCI:

* tick ON: "Strict", SQL 60
* Fill: LTRS (send diddles if idle)
* Stop: 1.5 (1.5 stop bits)
* TX: 0 (0db attenuation for send samples to TCI server)
* BPF: OFF
* Shape: Ramp 5
* tick ON: UOS and Start CR/LF

Use DIGL for RTTY, pay attention to set an offset (recommended 2210Hz for DIGL or 1500Hz for DIGU), otherwise you maybe have a "zero-beat" problem, if MARK is exact
at the carrier frequency, because classical RTTY is FSK keying and not SSB like. But here we are using AFSK. In SSB the carrier is always suppressed - in the case if MARK is exact at this carrier supression point you will hear NOTHING. deskHPSDR support such an offset, go to RX Menu and press OFFSET RTTY, as far as I know ExpertSDR2/3 have such an offset too.

### Documentation

No app documentation available yet, sorry. Maybe later...

### App Bundle Notarization

I don't have a paid Apple Developer Account and I don't plan to get one. That is why I unfortunately cannot officially notarize and digitally sign this app. Apple created this barrier, not I. If you don't accept this, go away and ignore this app.
Otherwise, use `xattr -r -d com.apple.quarantine /Applications/RTTY-TCI.app` to allow my app to start on your Mac.

### Licensing terms and conditions

rttyTCI is published as freeware, but not as Open Source. That means, Source code will not be available.

This rttyTCI app don't use any kind of foreign code or code parts, all program code was developed by myself.

You can use this app without any additional costs. This program is distributed in the hope that it will be useful, but  WITHOUT ANY WARRANTY; without even the implied warranty of  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

There are no rights or obligations to get any kind of user support for rttyTCI from me, I publish only the app bundle "as it is". Exclusion of any Guarantee and any Warrenty. All what you do with this app is at your very own risk.

This app was made without any commercial background or relationship. It's for use in Hamradio only for receive and transmit signals in classical RTTY mode 170 Hz shift and 45.45 baud.

73 Heiko, DL1BZ
