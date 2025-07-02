# Application

[Fleet](https://www.jetbrains.com/fleet/)

## Description

Do you enjoy working with different programming languages in the same project?
Well, we’ve got you covered! With Fleet, you can start coding in the language of
your choice. Fleet is designed to automatically detect your project
configuration from the source code, maximizing the value you get from its smart
code-processing engine while minimizing the need for project configuration.

## Build notes

Latest stable Fleet release from Arch Linux.

Note:- This application requires a license, otherwise it will run in Evaluation
Mode for 30 days.

## Usage

```bash
docker run -d \
    -p 5900:5900 \
    -p 6080:6080 \
    --name=<container name> \
    --security-opt seccomp=unconfined \
    -v <path for config files>:/config \
    -v <path for data files>:/data \
    -v /etc/localtime:/etc/localtime:ro \
    -e HTTPS_CERT_PATH=<path to cert file> \
    -e HTTPS_KEY_PATH=<path to key file> \
    -e WEBPAGE_TITLE=<name shown in browser tab> \
    -e VNC_PASSWORD=<password for web ui> \
    -e ENABLE_STARTUP_SCRIPTS=<yes|no> \
    -e UMASK=<umask for created files> \
    -e WEBUI_PORT=<port> \
    -e PUID=<uid for user> \
    -e PGID=<gid for user> \
    binhex/arch-fleet
```

Please replace all user variables in the above command defined by <> with the
correct values.

## Example

```bash
docker run -d \
    -p 5900:5900 \
    -p 6080:6080 \
    --name=fleet \
    --security-opt seccomp=unconfined \
    -v /apps/docker/fleet:/config \
    -v /apps/docker/fleet/projects:/data \
    -v /etc/localtime:/etc/localtime:ro \
    -e WEBPAGE_TITLE=Fleet \
    -e VNC_PASSWORD=mypassword \
    -e ENABLE_STARTUP_SCRIPTS=yes \
    -e UMASK=000 \
    -e WEBUI_PORT=6080 \
    -e PUID=0 \
    -e PGID=0 \
    binhex/arch-fleet
```

## Access via web interface (noVNC)

`http://<host ip>:<host port>/vnc.html?resize=remote&host=<host ip>&port=<host
port>&&autoconnect=1`

e.g.:-

`http://192.168.1.10:6080/vnc.html?resize=remote&host=192.168.1.10&port=6080&&autoconnect=1`

## Access via VNC client

`<host ip>::<host port>`

e.g.:-

`192.168.1.10::5900`

## Notes

`ENABLE_STARTUP_SCRIPTS` when set to `yes` will allow a user to install
additional packages from the official Arch Repository or the Arch User
Repository (AUR) via scripts located in the folder `/config/home/scripts/`. A
sample script is located at `/config/home/scripts/example-startup-script.sh`
with comments to guide the user on script creation.

User ID (PUID) and Group ID (PGID) can be found by issuing the following command
for the user you want to run the container as:-

```bash
id <username>
```

___
If you appreciate my work, then please consider buying me a beer  :D

[![PayPal donation](https://www.paypal.com/en_US/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MM5E27UX6AUU4)

[Documentation](https://github.com/binhex/documentation) | [Support forum](https://forums.unraid.net/topic/76727-support-binhex-fleet/)
