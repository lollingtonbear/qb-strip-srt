Script Name    :  qb-strip-srt
Orginal Author :  Andy Sibthorp
Latest Author  :  Andy Sibthorp
Version        :  1.0
Date           :  19/03/2024

Dependencies:
  qbittorrent-nox
  mkvtoolnix-cli
  mkvtoolnix-gui

Description:
  This bash script uses mkvmerge to remove unwanted subtitles (SRT) from specifed mkv file. It then deletes the original mkv file and moves it to the specified target dir.
  This designed to work with radarr and sonarr and qbittorrent

Instructions:

1. Prep the script
   Copy this script to a useful location (e.g. /usr/local/bin) and make it executable with chmod.
   Edit the varibles in the "Definitions and Settings" section to align with your own qbittorrent configuration.
   Edit the language settings if you prefer a non-English set of subtitles.
   Create the new target and logs directies. This script will try to do to for your if they don't exist, so it is assumed the script has permissions to do this.


2. Configure qbittorrent:
   You will need to configure qbittorrent to run this script after a torrent has finised downloading.
   In the qbittorrent web client goto Options > Downloads, then scroll down to the "Run external program" section
   Tick "Run external program on torrent finished"
   Enter the following in to the box below that tick box:
      /<path to the script>/qb-strip-srt "%R"


3. Configure radarr and sonarr
   You will need to configure sonar and radarr to look in the correct place the downloads
   Open the radarr web interface and navigate to Settings > Download client
   Add a new Remote Path Mapping that contains the download location Configured in qbittorrent and the location you want the script to place the files after being processed.
   See here for guide: https://wiki.servarr.com/radarr/settings#remote-path-mappings
