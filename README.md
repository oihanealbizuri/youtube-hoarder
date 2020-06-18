# youtube-hoarder
Download YouTube playlist, channels and videos automatically.

## Instalation
(WARNING: service files are made for systemd)

Install `youtube-dl`:

- Using `pip` (for a user): `pip --user install youtube-dl`
- Using `pip` (globally, with sudo): `sudo pip install youtube-dl`
- Arch Linux: `pacman -S youtube-dl`
- Ubuntu: `apt-get install youtube-dl`

Clone repository:

   git clone https://github.com/owentrigueros/youtube-hoarder.git

Install service and timer files as an user (via symlinks):

    mkdir -p /home/kepa/.config/systemd/user/
    ln -sf /full/path/to/youtube-hoarder/youtube-hoarder.* /home/kepa/.config/systemd/user/

## Configuration
Edit `youtube-hoarder.service` file `ExecStart` command to match the cloned repo path:

   `ExecStart=/path/to/youtube-hoarder/youtube-hoarder /path/to/youtube-hoarder/config`

Edit `config` file variables:

- `DOWNLOAD`: points to `youtube-hoarder/download`, where playlist and channels to be downloaded are set.
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
