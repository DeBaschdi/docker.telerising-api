# docker.telerising-api
A docker container for running telerising API

### Prerequisites
You will need to have `docker` installed on your system and the user you want to run it needs to be in the `docker` group.

> **Note:** The image is a multi-arch build providing variants for amd64, arm32v7 and arm64v8 - the correct variant for your Architecture needs to be tagged eg :amd64 :arm32v7 :arm64v8


## Technical info for Docker
To learn how to manually start the container or about available parameters (you might need for your GUI used) see the following example:

```
docker run \
  -d \
  -e USER_ID="99" \
  -e GROUP_ID="100" \
  -e TIMEZONE="Europe/Berlin" \
  -e UPDATE="yes" \
  -e PROVIDER="zattoo.com" \
  -e LOGIN="firstname.lastname@example.com" \
  -e PASSWORD="mypassword123" \
  -e SERVER="fr5-0" \
  -e NETWORK_DEVICE="eth0" \
  -e FFMPEG_HOST_LOCATION="\/usr\/bin\/ffmpeg" \
  -p 8180:8180 \
  -v {TELERISING_STORAGE}:/telerising \
  --name=telerising-api \
  --restart unless-stopped \
  --tmpfs /tmp \
  --tmpfs /var/log \
  --net="bridge" \
  takealug/telerising-api:tag
```

The available parameters in detail:

| Parameter | Optional | Values/Type | Default | Description |
| ---- | --- | --- | --- | --- |
| `USER_ID` | yes | [integer] | 99 | UID to run telerising as |
| `GROUP_ID` | yes | [integer] | 100 | GID to run telerising as |
| `TIMEZONE` | yes | [string] | Europe/Berlin | Timezone for the container |
| `PROVIDER` | no | [string] | zattoo.com | The Provider / Reseller u USE |
| `UPDATE` | yes | yes/no | yes | Updates Telerising Script inside This Container each restart |
| `LOGIN` | no | [string] | firstname.lastname@example.com | Your Provider Account NAME |
| `PASSWORD` | no | [string] | mypassword123 | Your Account Password |
| `SERVER` | yes | [string] | fr5-0 | The Server u want to use |
| `NETWORK_DEVICE` | yes | [string] | eth0 | The Device listen to on (nedded for Host-Mode) |
| `FFMPEG_HOST_LOCATION` | yes | [string] | /usr/bin/ffmpeg | The Path to ffmpeg on your Host |
| `-p` | yes | [integer] | 8180 | Listenport |
| `--net` | yes | bridge/host | bridge | The Network Mode to run The Container in|

> **Note:** If you plan to use VLC / tvheadend ect outside of your Docker network (e.g. 172.17.0.X) to use, you should run the container in --net = "host" and you must also enter the correct -e NETWORK_DEVICE = "XXX" of your host system.

Frequently used volumes:
 
| Volume | Optional | Description |
| ---- | --- | --- |
| `TELERISING_STORAGE` | no | The directory to persist telerising to |


When passing volumes please replace the name including the surrounding curly brackets with existing absolute paths with correct permissions.

## Support my work
If you like my Work, please [![Paypal Donation Page](https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif)](https://paypal.me/DeBaschdi) - thank you! :-)
