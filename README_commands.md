SOME USEFUL COMMANDS

 

Unlock Folders/Files

 

sudo chflags -R nouchg

 

OR

 

sudo chmod -R 777

 

Add a space after the command, then drag the file or folder to the Terminal window after the command, press enter. May prompt for a password; your computer password is all that is needed. Might not unlock folders and files on the XSAN, but will unlock on own computer, attached hard drives, Cache-A, and the Library computer in the Core.

 

Delete a file

 

rm

 

Add a space after the command, then drag the file or [empty] folder to the Terminal window after the command, press enter. NOTE: Files are immediately deleted cannot be recovered when deleted this way. Use with care.

 

Delete a Folder and all files in it

 

rm -R

 

Add a space after the command, then drag the folder to the Terminal window after the command, press enter. NOTE: Files & folders are immediately deleted cannot be recovered when deleted this way. Use with care.

 

Make Directories from a list of names listed in a text file

 

cat dirlist.txt | xargs mkdir

 

Make  empty files (e.g., something.txt) from a list of names listed in a text file

 

cat dirlist.txt | xargs touch

 

(where "dirlist.txt" is a text file with a bunch of file names separated by spaces. Names themselves shouldn't have spaces in them, if they do, enclose them in " " --e.g., file 1 would create two files: file and 1;  but "file 1" would create one file called file 1)

 

Index a tar file created with Keka and dumps stdout into a txt file

 

tar -tf [file].tar > [file]-tarindex.txt

example:

tar -tf GFX_PROJECT.tar > GFX_PROJECT-tarindex.txt

 

Generate a mediainfo report in the command line

 

mediainfo [path/to/file]

 

Count files in a directory tree

 

find FOLDERNAME -type f | wc -l

 

