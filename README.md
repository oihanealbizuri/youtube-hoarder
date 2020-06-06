# youtube-hoarder
Download YouTube playlist, channels and videos automatically.

## Instalation
(WARNING: service files are made for systemd)

Install service and timer files as an user (via symlinks):

    mkdir -p .config/systemd/user/
    ln -sf /path/to/youtube-hoarder.* .config/systemd/user/

## Configuration
Edit `config` file variables:

- `DOWNLOAD`: points to `youtube-hoarder/download`, where playlist and channels to be downloaded are saved.
- `MUSIC_DL_DIR` and `VIDEO_DL_DIR`: they point to download directories.

Edit `download` file, the script reads the first two columns:

1. Media type: can be `music` or `video`.
2. URL: self explanatory.
3. (optional): whatever you want, it's not read, but may be useful to know what you are downloading.

For example:

    music https://www.youtube.com/playlist?list=MyMusicPlaylist Music
    video https://www.youtube.com/user/MyChannel                My Channel

## Run the service
Enable and start `youtube-hoarder.timer` (by default, it runs `youtube-hoarder.service` once every 15 minutes):

    systemctl enable --now --user youtube-hoarder.timer
