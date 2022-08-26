# vinylemulator for RC522

Emulate the tactile experience of a vinyl collection through your Sonos system, but with a back end run by Spotify.

There is a step-by-step tutorial on how to set this up from first principles on a Raspberry Pi here: https://www.hackster.io/mark-hank/sonos-spotify-vinyl-emulator-ssve-3be63d

Update: confirmed works with Sonos S2 released 8 June 2020

This forked version of the vinylemulator is modified to use the RC522 RFID reader/writer. Learn how to connect and configure it here: https://pimylifeup.com/raspberry-pi-rfid-rc522/

Description
---------------------------

Start playing a Spotify album or playlist through Sonos when you place a physical object on an NFC reader connected to a Raspberry Pi.

You can attach these tiny NFC tags to any physical object you want: I like polaroid-style prints of album covers and tape cassettes for playlists/mixtapes, but you do you; send me a photo if you're baller enough to print album art on 12-inch square aluminium plates and tag it to that.

Background
---------------------------

Originally forked from <a href="https://github.com/pucbaldwin/musicbox">musicbox project</a> which was itself a fork from <a href="https://github.com/shawnrk/songblocks">songblocks project</a>. I have rewritten and simplified this a lot, however, so this version looks very different to those two.

All the actual back end work of this is done by the <a href="https://github.com/jishi/node-sonos-http-api/">node-sonos-http-api</a> which will need to be installed and set up in order to work.

This is not the first project to link NFC to Sonos / Spotify, but I couldn't find one that did both in the way I wanted. Unlike other projects of this type - which take a NFC tag id and cross reference that against a database on the Raspberry Pi to find the music URI - this project actually stores the album details directly on the NFC tag. This has a few advantages:

First, you can have a very large collection which will continue to exist independent of digital storage on the Raspberry Pi. Even if you manage to wipe the database on your Pi, your collection will live forever (just like real vinyl);

Second, these NFC tags aren't tied to the particular Raspberry Pi. This means that the tags are portable to other Raspberry Pis running the same scripts. So take your favourite jazz album from your city pad up to the country house to listen to in the study when it's Laphroig time, or take a rare deep cut you've stumbled across to a friend's house for a listening party. Other use cases are available for those who aren't millionaires.

It also means that other applications can read the tags - I am working on an implementation for Android phones which don't rely on Pi for the NFC, for instance.

It's all coded in Python. Kind of.

Usage
---------------------------

This currently accesses three any of three different services depending on the content of the NFC tag presented. The relevant service is determined by the start of the text passed by the NFC tag.

| Service name     | Behaviour       |
| ---------------- | --------------- |
| spotify: | Plays a spotify album, track or playlist URI |
| tunein: | Plays a radio station identified by a tunein ID number |
| bbcsounds: | Plays a BBC radio station identified by stream name as detailed in node-sonos-http-api readme |
| apple: | Plays a Apple Music album, track or playlist URI |
| amazonmusic: | Plays a Amazon Music album, track or playlist URI |
| room: | Changes the room in which the script plays|
| command: | Executes a command in the current room; can accept any command as defined in node-sonos-http-api |
| favorite: | Plays a Sonos favorite identified by its name |

Examples of what can be passed:

```sh

      spotify:track:4LI1ykYGFCcXPWkrpcU7hn
      spotify:album:4hW2wvP51Myt7UIVTgSp4f
      spotify:user:spotify:playlist:32O0SSXDNWDrMievPkV0Im

      tunein/play/44491
      
      favourite/BBC_Radio_2

      bbcsounds:bbc_radio_two

      command:playpause
      command:mute
      command:next
      command:volume/50
      command:volume/+10
      command:shuffle/on
```

Setup instructions
---------------------------

Follow all the instructions on [this page](https://pimylifeup.com/raspberry-pi-rfid-rc522/) to ensure you have a working RC522 before setting up this project, then follow the original instructions below: 

> I made a full tutorial, starting from absolute first principles, here:
https://www.hackster.io/mark-hank/sonos-spotify-vinyl-emulator-ssve-3be63d

