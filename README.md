# openalpr-pi

Uses ansible to install openalpr (https://github.com/openalpr/openalpr) on a raspberry pi. Once complete, openalprd will run and analyze a mjpeg stream from the raspberry pi camera, and put the result on a beanstalk queue, as described on https://github.com/openalpr/openalpr/wiki/OpenALPR-Daemon-%28alprd%29. 

## What this ansible playbook will do

* Resize partition to utilize full size of sd card
* Install required libraries
* Install mjpeg-streamer https://github.com/jacksonliam/mjpg-streamer
* Compile openalpr (and opencv and other required libraries)
* Start mjpeg-stream and openalprd on boot

## What you need

* Raspberry Pi with camera module
* SD Card with Raspbian

## What you must do

* Connect rPi to network

* Export your key to rPi 

```
ssh pi@<rPi ip address> 'mkdir .ssh'
cat ~/.ssh/id_rsa.pub | ssh pi@<rPi ip address> 'cat >> .ssh/authorized_key'
```

* Edit the file "production", and modify it with correct ip address to your rPi. 

* Copy provisioning/roles/wlan/vars/main.yml.example to provisioning/roles/wlan/vars/main.yml, and enter your wifi credentials (or delete the "wlan" line in playbook.yml if you don't want wlan). 

* Run the playbook:

```
ansible-playbook -i production playbook.yml
```

The whole process takes some 8 hours on rPi2.
