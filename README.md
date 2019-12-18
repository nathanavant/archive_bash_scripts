SCRIPTS

 

These are simple scripts that I wrote in order to automate common tasks. 

 

In order to use them, you need to cut and paste the text into a plain text file labeled scriptname or scriptname.sh (the extension is optional) and place them in the folder /usr/local/bin on your machine. (This folder may have to be created).

 

This is a hidden folder, but you can easily access it in the Mac OS Finder by selecting Go→Go to Folder in the Finder menu bar and typing /usr/local/bin into the search box. 

 

Once you’ve dropped the file into that folder, you have to make it executable to turn it into a command. Open a terminal window and type

 

cd /usr/local/bin

 

This will navigate you to the folder you just dropped the script into. Now type

 

chmod +x script.sh

 

Where the italics is the filename of the script. 

 

Now you will be able to run the command from any location in the terminal by entering just the scriptname.

 

Dirlist

 

When you run this script in a folder, it will automatically generate the standard Smithsonian Channel numbered show folders. It saves a bit of time and makes sure you name them accurately. In order for this script to work, you must create a folder called “files” in usr/local/bin that contains a dirlist.txt file with the current folder structure written out as a list.

 

https://lh6.googleusercontent.com/915nVwWoYbdaZsA2UtWGMwfMv6rUqqAh69i4BxrmcLzAM5OvKohsHCqiIZb8ei9Q6EqWyxqO5uiQl-X_4clsZYUzTxM0-dShQBItq8l0j1df44WGwSZ8S_FaeHzgC1UQxZfbgCqB

 

As the official folder structure changes this text file must be kept up to date.

 

The Script

 

#!/bin/bash

 

#dirlist - creates standard SN folder structure

 

cat /usr/local/bin/files/dirlist.txt | xargs mkdir

 

Barcodes

 

This script looks for a text file called barcodes.txt and uses it to create a series of folders inside the current directory. I use this to quickly make all the barcoded folders I will need for a processing project.

 

First, you have to create the text file with the list of folder names (each on their own line, just as in the dirlist example above). I make these by copying the entire barcode column from the Master Inventory List spreadsheet and pasting it into a document in nano, a command line text editor. You can also use TextEdit for this.

 

Once the text file is in place with all barcodes listed, I navigate to the folder in the Terminal and run the script. The folders are created and the text file is deleted.

 

The Script

 

#!/bin/bash

 

#barcodes - makes all the folders from a txt file

 

cat barcodes.txt | xargs mkdir

rm barcodes.txt

 

Checksums

 

When you run this script in a folder, it will calculate md5 checksums for every file in a directory, and then place that information into a handy csv spreadsheet file called file_inventory.csv

 

Installing rhash

 

This script requires a command line applications called rhash to run. Rhash is capable of recursively looping through a directory and calculating md5 checksums for all files with one command. 

 

In order to install rhash, you first have to install an application called homebrew. Homebrew is an open source application that uses public repositories to grab and install applications in a very user-friendly way. It works just like apt-get on a Linux system, if you are familiar with that. Paste this command into a terminal window and hit enter, and Homebrew will install.

 

ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null

 

If the screen prompts you to enter a password, enter your Mac's user password to continue. Just type your password and press ENTER/RETURN key, the text is hidden as you type it. 

 

When the process finishes and you have a blank prompt again, install rhash by typing:

 

brew install rhash

 

When this process finishes, rhash is installed and you will be able to use this script. 

 

How to Use the Script

 

Navigate to the directory that contains the files you want to create checksums for and run the script by typing its filename.

 

The command may take a while to execute, depending on the number of files in the folder and their sizes. Don’t close the Terminal window until it gives you a fresh prompt, which means it is finished. The file_inventory.csv file should now have been added to your directory with a list of all files and their checksums.

 

The script

 

#!/bin/bash

 

#checksums - creates CSV file with filenames and MD5 checksums for all files in directory

DIR=.

 

rhash -r --md5 -p "%f, %m \n" "$DIR" >> file_inventory.csv
