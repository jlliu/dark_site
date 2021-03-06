# Set up a website on the dark web

These instructions are a part of a workshop on the dark web, Tor, and the role of art on the dark web. [See slides here](https://docs.google.com/presentation/d/15EjToNoy4DlnsTIm8vOmfok-aYSOzcrd6IY3hJGdYec/edit?usp=sharing).

# [Mac and Linux instructions](#mac-and-linux-instructions) | [Windows instructions](#windows-instructions)

	
## _Mac and Linux Instructions_ ##

### 1. Download the Tor Browser
Install the Tor Browser by downloading here: https://www.torproject.org/download/


### 2. Download a text editor ([Sublime Text](https://www.sublimetext.com/), [Atom](https://atom.io/), etc.)

### 3. Open up a terminal and install required libraries.

__a. Install Homebrew:__

Homebrew helps you easily install software packages on your computer. For more info: (https://brew.sh/)

For Mac OSX:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

For Linux:
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install.sh)"
```

__b. Make sure you have Python installed__
You can check if you already have it by running ```python```, otherwise you can run brew install python ).

__c. Install Tor__
```
brew install tor
```

### 4. Set up your local web server 

__a. Download example code here (https://github.com/jlliu/dark_site) to your computer.__

This will download a folder called `dark_site-master`, containing an HTML file. Unzip the folder to somewhere you can find easily. 

__b. In the terminal, navigate to within the ```dark_site-master``` folder.__


__c. While inside that directory, start a local server by running:__

```
python -m SimpleHTTPServer 8080
```

Depending on the `python` version you have installed, you might need to run
```
python -m http.server 8080
```
instead.

You can choose a different port number than 8080, but you should remember it for later!

__d. Check whether your local server is running by opening your favorite web browser and going to localhost:8080.__

### 5. Configure your onion service

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
#HiddenServiceDir /usr/local/var/lib/tor/hidden_service/
#HiddenServicePort 80 127.0.0.1:80
```
iii. Remove the ```“#”``` to uncomment both of these lines, and modify them as follows:
```
HiddenServiceDir /Users/YOUR_ACCOUNT_NAME/Documents/hidden_service
HiddenServicePort 80 127.0.0.1:8080
```

The path corresponding to ```HiddenServiceDir``` will hold the things needed to get your hidden service working, i.e., a public key, a private key, and a hostname (your very own onion site).

It should NOT be the directory where you are hosting your website files, as ```HiddenServiceDir``` contains secret information. The port number (in this case, ```8080```) on the line with ```HiddenServicePort``` should correspond with the port that you are using with your python server.

Above, we are saying that our ```HiddenServiceDir``` should be in a folder called ```hidden_service``` in your ```Documents``` folder. But this can be anywhere on your computer, as long as it's not your website directory! Remember to change ```YOUR_ACCOUNT_NAME``` to your computer username.

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

If done successfully, this command should automatically make a folder called ```hidden_service``` at the path you specified in the ```torrc``` file!
	
### 6. View your dark web site!
__a. To get the .onion address of your site, run the following:__
```
cat /Users/YOUR_ACCOUNT_NAME/Documents/hidden_service/hostname
```
This should give you a long, gibberish address ending in .onion.

__b. Open the Tor browser, and copy and paste this address into the address bar.__

You should be able to see the website you’re hosting at that address. You can continue to make changes to your locally-hosted website and see them reflected in the Tor browser without having to re-run Tor, as long as your local server keeps running.

In the Tor browser, you may also notice that inspecting the Tor circuit reveals that your traffic goes through three unknown relays before your onion service. This is because creating an onion service is effectively using Tor’s anonymizing capabilities to mask your identity as a webhost.

*** After your .onion site is working, please DO NOT close the terminal window where you are running Tor. It will stop your onion service, and re-running it will generate a different .onion site name for you.

Please also keep your local web server (the one you created with the command "Python -m SimpleHTTPServer..." running as well - you don't need to restart it for changes you make to the site's HTML to come into effect. ***

## _Windows Instructions_ ##

### 1. Install the Tor Browser by downloading [here](https://www.torproject.org/download/).

### 2. Download a text editor ([Sublime Text](https://www.sublimetext.com/), [Atom](https://atom.io/), etc.)

### 3. Make sure you have `python` installed
You can check if you already have it by running ```python``` in the Command Prompt, otherwise you can download it from [here](https://www.python.org/downloads).


### 4. Set up your local web server

__a. Download example code here (https://github.com/jlliu/dark_site) to your computer.__

This will download a folder called ```dark_site-master```, containing an HTML file. Unzip the folder to somewhere you can find easily. 

__b. In the Command Prompt, navigate to within the ```dark_site-master``` folder. (There may be two folders called dark_site-master nested in each other, make sure you enter the deepest one.)__

```
cd C:\Users\YOUR_ACCOUNT_NAME_HERE\Downloads\dark_site-master\dark_site-master
```
The above command assumes the folder is in your Downloads, and assumes you should look into the *second* dark_site-master folder nested in the first one. Remember to change ```YOUR_ACCOUNT_NAME``` to your computer username.

__c. While inside that directory, start a local server by running:__

```
python -m SimpleHTTPServer 8080
```

Depending on the `python` version you have installed, you might need to run
```
python -m http.server 8080
```
instead.

You can choose a different port number than 8080, but you should remember it for later!

__d. Check whether your local server is running by opening your favorite web browser and going to localhost:8080.__

### 5. Configure your onion service
__a. Locate the Tor configuration file called `torrc`.__
First, find where you downloaded the Tor Browser bundle. Once in that folder, navigate to `Browser\TorBrowser\Data\Tor\torrc`. Or just look up the `torrc` filename using the Windows search.

__b. Edit the `torrc` configuration file.__
i. Open the `torrc` file with your favorite text editor.

ii. Add the following lines at the end (and make sure to replace `YOUR_USERNAME`):
```
HiddenServiceDir C:\Users\YOUR_USERNAME\Documents\tor\hidden_service
HiddenServicePort 80 127.0.0.1:8080
```

The path corresponding to ```HiddenServiceDir``` holds the things needed to get your hidden service working, i.e., a public key, a private key, and a hostname (your very own onion site). It should NOT be the directory where you are hosting your website files, as ```HiddenServiceDir``` contains secret information. The port number (in this case, ```8080```) on the line with ```HiddenServicePort``` should correspond with the port that you are using with your python server.

iii. Save and close the `torrc` file.

iv. Create the `tor` folder inside `C:\Users\YOUR_USERNAME\Documents`, and the `hidden_service` folder inside `C:\Users\YOUR_USERNAME\Documents\tor`, if they don't already exist.

__c. Re-open the Tor browser in order for changes to take effect!__

Every time you open the Tor browser, the Tor software starts running, and will make any changes in your configuration file take effect.
	
### 4. View your dark web site!
__a. To get the .onion address of your site, open the file located at `C:\Users\YOUR_USERNAME\Documents\tor\hidden_service\hostname`.__
You can use any text editor. This should give you a long, gibberish address ending in .onion.

__b. Open the Tor browser, and copy and paste this address into the address bar.__

You should be able to see the website you’re hosting at that address. You can continue to make changes to your locally-hosted website and see them reflected in the Tor browser without having to re-run Tor, as long as your local server keeps running.

In the Tor browser, you may also notice that inspecting the Tor circuit reveals that your traffic goes through three unknown relays before your onion service. This is because creating an onion service is effectively using Tor’s anonymizing capabilities to mask your identity as a webhost.

** After your .onion site is working, please keep your local web server running (the one you created with the command `python -m SimpleHTTPServer...` running – you don't need to restart it for changes you make to the site's HTML to come into effect. **
