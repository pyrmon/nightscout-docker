# nightscout-docker
Comprehensive Docker Setup for Nightscout CGM Monitor on Raspberry Pi 4 or any Linux Computer/Server

## Credit
I have gotten both the Dockerfile and the docker-compose.yml from liske/cgm-remote-monitor-docker, thank you!

## Backstory
My girlfriend is a type 1 diabetic and so I got into CGM Monitoring.
I wanted to create a guide of how I host my own Nightscout server under my own domain.
It is very easy and everybody that owns a Linux Server (for example a Raspberry Pi 4).
I will first explain how to setup Nightscout and later also how to setup Nginx so you can host Nightscout securely. If you don't own a domain you can use a free one. I will create another Readme later on how to do that. If you have any questions feel free to just write an e-mail to florian@schickel.me and I can try my best to help you.

## Requirements for this to work

* Any sort of Linux Computer/Server, have tested it both on ARM processors and AMD processors
* Docker and Docker-Compose installed (google it if you don't know how to do that)
* Administrative access to your router

## Setup Nightscout

* I have included the Dockerfile that I used, but it is for refrence only
* First Clone this repository to your server and go into the folder
```sh
git clone https://github.com/florianschi909/nightscout-docker && cd nightscout-docker
```
* Edit the docker-compose-amd.yml file
    * Change the API_SECRET value to a password with the min length of 12, I don't know if all special characters are okay
    * Change the BASE_URL to the webadress you want to access Nightscout from later on 
        * if you don't know this yet then wait for my instructions (which I will write later) where I tell you how you can get a free domain
    * If you don't use mg/dl then you can change DISPLAY_UNITS value to mmol
```Dockerfile
      # admin secret
      - API_SECRET=xxxxxxxxxxxx
      # the URL to this Nightscout instance
      - BASE_URL=https://ns.xxxxx.com
      ...
      # use SI units by default
      - DISPLAY_UNITS=mg/dl
```
* This is it. Now follow this command and your Nightscout is running on the webadress http://localhost:1337/
```sh
docker-compose up -d
```

## Setup Nginx

* This will only be the explanation on how to get Nginx running
* How the ssl certificate creation and proxy hosts work I will explain in a later commit
* Just enter these commands and it will setup Nginx Proxy Mangager on http://localhost:81
```sh
cd nginx
docker-compose -f docker-compose-nginx.yml up -d
```
* After this you can sign in as admin@example.com with the password changeme
