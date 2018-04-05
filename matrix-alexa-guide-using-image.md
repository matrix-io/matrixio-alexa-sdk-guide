# Alexa SDK Guide with MATRIX Creator/Voice (using pre-buit Image version)

With this image you can be up and running in just 10 minutes. The image has all packages needed already installed and part of the SDK pre-built. Steps are:

### 1. Download and Flash the Image 
If you need help with this check out [this]( https://www.raspberrypi.org/documentation/installation/installing-images/README.md) guide from Raspberry Pi.

* Image zip file: https://storage.googleapis.com/matrix-creator-testing-images/matrix-alexa-sdk-guide-040318.img.zip
* Image md5sum file:  https://storage.googleapis.com/matrix-creator-testing-images/matrix-alexa-sdk-guide-040318.img.zip.md5


### 2. Fill Authentication Info and Get Auth Token

SSH into the Raspberry Pi once bootd. This image is using Raspbian Lite version, therefore no visual interface is available. You will have to either connect a HDMI monitor and a keyboard or SSH into the Raspbery Pi. 
If you decide to use SHH, the this image's hostname is `alexa-rpi`, so after connecting the Raspberry to a network and booting it up (using a ehternet cable for example) you could try to SSH using just:
`sudo ssh pi@alexa-rpi.local`
For additional help on how to SSH check [here](https://www.raspberrypi.org/documentation/remote-access/ssh/).

Once succesfully ssh, open the `confing.txt` file in a editor and fill the `Client ID`, `Product ID` and `Client Secret` from the registration steps.

Now you need to get the Authentication Token. Run the authentication script:
`bash ./startauth.sh`

Open a browser and navigate to `http://localhost:3000`. Log in with your Amazon credentials and follow the instructions provided. A tip here is you are using SSH, you can use the terminal browser **links** from another terminal to authenticate. 

From the second SSH terminal type:
 `links http://localhost:3000`
Use ENTER to confirm and arrows keys to navigate. After finished use `q` to close the browser. More help about **links** browser [here](http://links.twibright.com/user_en.html).

### 3. Build the SDK

This should take few minutes. Run and follow directions:
`bash ./setup.sh ./config.txt`

Now you are ready to run Alexa app.

### 4. Run Alexa!
```
bash ./startsample.sh
```

The output should be similar to [example-output.txt](https://github.com/matrix-io/matrixio-alexa-sdk-guide/blob/master/example-output.txt).