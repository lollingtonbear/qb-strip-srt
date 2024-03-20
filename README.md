Script Name    :  qb-strip-srt

Orginal Author :  Lollington_Bear

Version        :  1.0

Date           :  19/03/2024

Background:

The Plex app my Samsung TV struggles to play mkv files if they contain a lot of language tracks for subtitles and audio. The player either locks up or the video playback is badly artifacted. Apparantly this is a common issue with Samsung TV Plex app.

To solve this problem you can use mkvmerge to create a new mkv file with only the tracks you want in it, then Plex app on the Samsung TV play the video without issue.

I wanted to automate this process so it happens before radarr / sonarr pick up the file, so I wrote a basic script that does it for you. I've also included the setup steps for it up.

Requires:
1. qbittorrent-nox  (Or anyother torrent client that supports running a script when a download is completed)
2. mkvtoolnix-cli
3. mkvtoolnix-gui

Description:

This bash script uses mkvmerge to remove unwanted subtitles (SRT) from specifed mkv file. It then deletes the original mkv file and moves it to the specified target dir. This is intended to work with radarr and sonarr and qbittorrent

Instructions:

Prep the script
1. Copy this script to a useful location (e.g. /usr/local/bin) and make it executable with chmod.
2. Edit the varibles in the "Definitions and Settings" section to align with your own qbittorrent configuration.
3. Edit the language settings if you prefer a non-English set of subtitles.
4. Create the new target and logs directies. This script will try to do to for your if they don't exist, so it is assumed the script has permissions to do this.

Configure qbittorrent:
1. You will need to configure qbittorrent to run this script after a torrent has finised downloading.
2. In the qbittorrent web client goto Options > Downloads, then scroll down to the "Run external program" section
3. Tick "Run external program on torrent finished"
4. Enter the following in to the box below that tick box:

        /<path to the script>/qb-strip-srt "%R"

Configure radarr and sonarr
1. You will need to configure sonar and radarr to look in the correct place the downloads
2. Open the radarr web interface and navigate to Settings > Download client
3. Add a new Remote Path Mapping that contains the download location Configured in qbittorrent and the location you want the script to place the files after being processed.
4. See here for guide: https://wiki.servarr.com/radarr/settings#remote-path-mappings
