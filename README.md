# dark_site

[Mac/Linux instructions](#mac-or-linux-instructions)

[Windows instructions](#windows-instructions)

# Mac or Linux Instructions

## Download the Tor Browser
Install the Tor Browser by downloading here: https://www.torproject.org/download/
## 1. Open up a terminal/shell and install required libraries.

__a. Install Homebrew:__

Homebrew helps you easily install software packages on your computer. For more info: (https://brew.sh/)

For Mac OSX:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

For Linux:
```sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"```

__b. Make sure you have Python installed__
You can check if you already have it by running ```python```, otherwise you can run brew install python ).
__c. Install Tor__
```
brew install tor
```

## 2. Set up your local web server 
__a. Download example code here (https://github.com/jlliu/dark_site) to your computer.__
This will download a folder called “dark_site”, containing an HTML file. Unzip the folder to somewhere you can find easily. 
__b. In the terminal, navigate to within the ```“dark_site”``` folder.__
__c. While inside that directory, start a local server by running:__
```
python -m SimpleHTTPServer 8080
```
You can choose a different port number than 8080, but you should remember it for later!

__d. Check whether your local server is running by opening your favorite web browser and going to localhost:8080. __

## 3. Configure your onion service
__a. Locate the Tor configuration file:__
```
cd /usr/local/etc/tor
```
(Note: This path might look different depending on how you install Tor).
Try inspecting the contents of the folder with the following command:
```
ls
```
This tells you the contents of the ```/tor``` folder. You should see a file called ```torrc.sample```. This is a sample Tor configuration file.
__b. Edit the torrc configuration file.__
i. Open the ```torrc.sample``` file with a text editor (here, we will use vim, a way of editing files on the command line).
```
vim torrc.sample
```
ii. Search for the section that says “This section is just for location-hidden services”. Find the following lines:
```
# HiddenServiceDir /usr/local/etc/tor/hidden_service/
# HiddenServicePort 80 127.0.0.1:80
```
iii. Remove the ```“#”``` to uncomment the lines, and modify them as follows:
```
HiddenServiceDir /usr/local/etc/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:8080
```
The path corresponding to ```HiddenServiceDir``` holds the things needed to get your hidden service working, i.e., a public key, a private key, and a hostname (your very own onion site). It should NOT be the directory where you are hosting your website files, as ```HiddenServiceDir``` contains secret information. The port number (in this case, ```8080```) on the line with ```HiddenServicePort``` should correspond with the port that you are using with your python server.

iv. Save your file. In vim, you can do this by hitting esc and then typing ```:wq```.

v. Remove the ```.sample``` extension to the file to make the configuration file effective. While in the directory where ```torrc.sample``` is located, you can rename this file with the ```mv``` command, which can move a file from an old location to a new location (as well as rename it from an original name to a new name).
```
mv torrc.sample torrc 
```
__c. Run Tor to make your settings take effect.__
Run Tor to configure your Onion service according to your ```torrc``` file. 
```
tor
```
If you encounter an error in the terminal, you may have typed something wrong in the torrc file. Anytime you make changes to the ```torrc``` file, you have to rerun this command by stopping tor using cmd+C, and rerunning ```tor```.
	
## 4. View your dark web site!
__a. To get the .onion address of your site, run the following:__
```
cat /usr/local/etc/tor/hidden_service/hostname
```
This should give you a long, gibberish address ending in .onion.

__b. Open the Tor browser, and copy and paste this address into the address bar.__

You should be able to see the website you’re hosting at that address. You can continue to make changes to your locally-hosted website and see them reflected in the Tor browser without having to re-run Tor, as long as your local server keeps running.

In the Tor browser, you may also notice that inspecting the Tor circuit reveals that your traffic goes through three unknown relays before your onion service. This is because creating an onion service is effectively using Tor’s anonymizing capabilities to mask your identity as a webhost.

# Windows Instructions

[TO DO] Fill in here. maybe we don't even need an entirely different section and can just differentiate the mac/windows instructions at the package installation step. need to confirm whether or not the terminal commands will be different.
