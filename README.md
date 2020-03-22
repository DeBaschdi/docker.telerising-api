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
  -e YOUTH_PROTECTION_PIN="1234" \
  -e SERVER="fr5-0" \
  -e SSL_MODE="0" \
  -e NETWORK_DEVICE="eth0" \
  -e FFMPEG_HOST_LOCATION="/usr/bin/ffmpeg" \
  -e PLATFORM="hls5" \
  -e BW="8000" \
  -e PROFILE="1" \
  -e AUDIO2="false" \
  -e DOLBY="false" \
  -e IGNORE_MAXRATE="false" \
  -e FFMPEG_LOGLEVEL="fatal" \
  -e ONDEMAND="false" \
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
| `YOUTH_PROTECTION_PIN` | yes | [string] | 123 | Your Youth Protection Pin to unlock FSK Content |
| `SERVER` | yes | [string] | fr5-0 | The Server u want to use |
| `SSL_MODE` | yes | 0/1 | 0 | Enable / Disable SSL Verify with Provider |
| `FFMPEG_HOST_LOCATION` | yes | [string] | /usr/bin/ffmpeg | The Path to ffmpeg on your TVH/FFMPEG-Client |
| `-p` | yes | [integer] | 8180 | Listenport |
| `ONDEMAND` | yes | true/false | false | Enable Video on Demand |

Default Client Settings, can be overwritten by Querystrings:

| Parameter | Optional | Values/Type | Default | Description |
| ---- | --- | --- | --- | --- |
| `PLATFORM` | yes | hls/hls5 | hls5 | hls - for: VLC, IPTV Simple, hls5 - for: ffmpeg, tvHeadend |
| `BW` | yes | 8000/4999/5000/3000/2999/1500 | 8000 | Streamquality |
| `PROFILE` | yes | 1/2/3/4 | 1 | Use 2 Audio Streams |
| `AUDIO2` | yes | true/false | false | use 2nd audio stream (HLS5 only) |
| `DOLBY` | yes | true/false | false | use 1st Audio Stream ,- Dolby audio (HLS5 only) |
| `IGNORE_MAXRATE` | yes | true/false | false | The stream quality check can be disabled by using the `IGNORE_MAXRATE` value (set to "true") |
| `FFMPEG_LOGLEVEL` | yes | [string] | fatal |  The ffmpeg loglevel can be changed by using the "loglevel" value. |

Network Settings:

| Parameter | Optional | Values/Type | Default | Description |
| ---- | --- | --- | --- | --- |
| `NETWORK_DEVICE` | no | [string] | eth0 | The Device listen to on (nedded for Host-Mode) |
| `ADDRESS` | yes | [string] | --- | If you Setup an IP ADDRESS or Hostname like 192.168.0.1 or example.com, Telerising is is listen to that Setting, `NETWORK_DEVICE` will be Ignored |
| `--net` | yes | bridge/host | bridge | The Network Mode to run The Container in|

> **Note:** If you plan to use VLC / tvheadend ect outside of your Docker network (e.g. 172.17.0.X) to use, you should run the container in --net = "host" and you must also enter the correct -e NETWORK_DEVICE = "XXX" of your host system.

Frequently used volumes:
 
| Volume | Optional | Description |
| ---- | --- | --- |
| `TELERISING_STORAGE` | no | The directory to persist telerising to |


When passing volumes please replace the name including the surrounding curly brackets with existing absolute paths with correct permissions.

## Support my work
If you like my Work, please [![Paypal Donation Page](https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif)](https://paypal.me/DeBaschdi) - thank you! :-)

## Unraid Template
> **Note:** An Template for Unraid can be found here : https://raw.githubusercontent.com/DeBaschdi/docker.telerising-api/master/Templates/Unraid/my-Telerising-API.xml
> Please safe it to into \flash\config\plugins\dockerMan\templates-user, after that you can use this Template in Unraids Webui. Docker > Add Container > Select Template and choose Telerising-API

<img src="https://raw.githubusercontent.com/DeBaschdi/docker.telerising-api/master/Templates/Unraid/Screenshot.png" height="325" width="265">
