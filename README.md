# MARAC_API_Workshop
These are the resources used in the "There's An API for that!" workshops sponsored by the Mid-Atlantic Regional Archives Conference in 2017. Note that these are the scripts used in the workshop itself. For additional scripts and resources referenced in the workshop, navigate to the [_additional resources_](../master//additional%20resources) subfolder, above.

These scripts and this documentation, combined with the workshop itself, are meant to encourage and empower users to run Python scripts at their home institutions. The following details are meant to be understood in order.


### How do I use these?

First, a necessary disclaimer: **We highly recommend AGAINST making any changes or using any of these scripts against your working, or Production, instance of ArchivesSpace and/or with the only copy of existing Production data.** If you do not have a Development version of AS, you can contact us or show the vagrant you used in class as an example of how one might be set up for you. Note that GET scripts are not that risky, so if you cannot or will not have a Dev instance of AS, you can still try GETs as your familiarize yourself with our scripts. If fear of making mistakes is holding you back, and rightly so, you should investigate options for running a Dev or Virtual Machine (VM) of AS. If your institution decides to ramp up its use of APIs, a testing environment is a necessity.

Second, remember the vagrant box that you were provided in the course of the workshop. That box, now stored locally on the laptop you brought to the workshop, is our gift to you. We encourage truly novice users who may be wary to try anything on real data to play in the vagrant virtual environment first. No matter what you do there you cannot break anything, and if you mess up your data, just blast away the vagrant box using the instructions provided in the workshop slides and then `vagrant up` again!

There's very little data in the default box, but once you have it up and running you can:
+ manually enter data just like you would in AS
+ import your own collections via EAD
+ more advanced users can use our GET scripts to pull down resource records from their own institutional instance of AS and POST them to the vagrant (remember that the vagrant endpoint will begin with http://localhost:8089)


### How do I _run_ these?
This is a subtly different question from the above. This section gives practical advice for how to run these scripts, though it still raises more questions than answers. The first thing you need to know is what operating system (OS) you are using to execute these scripts.  The Mac (or Linux, for that matter) terminal is a command line interface that allows for nearly full control of the Unix-based Mac (or Linux) operating system; conversely, the Windows command prompt (that thing you get when you type "Run > cmd.exe") is essentially just an extension of the old text-based MS DOS operating system and is more limited in what it can do natively.  To help even the playing field a bit, we recommend using CygWin, an application that allows you to utilize a Unix-like terminal on a Windows machine.

* *All users*

   Directories really matter. Whatever directory you download a script to is where a) you need to run that script _from_, b) where that script is going to look for other scripts or files if it's a script that needs other resources (like the barcodes script), and c) put the output files, if the script is creating outputs. So if you download a script and leave it in your Downloads folder, all your resulting output files will also write to that folder. Also, you'll need to navigate to where your scripts are from within the command line/terminal, which is a barrier to novice users. Google "how to change directories in [the command line (Windows)] or [terminal (Mac users)] for advice on how to navigate to your script directory if you need to.

* *Windows users*

   Windows users who attended the workshop will recall that we took steps to install _cygwin_, which is a "Linux-like environment for Windows making it possible to port software running on POSIX systems (such as Linux, BSD, and Unix systems) to Windows." Cygwin allows Windows to communicate with Linux-like applications. Please see our presentation slides to walk yourself through installing cygwin and the packages required to run our scripts. Keep the cygwin installer around, it comes in handy (see immediately below).

   Pro-tip: If you ever run a script and cygwin says something along the lines of "pip: command not found" it means you're missing a package (in that example, the missing package is called pip). Try Googling the error message and you will almost certainly find other people with the same problem; use their answers to determine what package you need to install, and then re-run the cgywin installer. When you get to the Install Packages screen, there is where to look for packages. This isn't a easy pro-tip, just an insight on how these programs work. Attendees will also remember that we cloned the fuzzy wuzzy GitHub repo; this is another way of installing necessary packages.

* *Mac users*

   There is a reason why developers love Macs! You don't need a Unix emulator like Cygwin, but, you may not have all the necessary packages installed. Mac users will remember opening the terminal and having to check for XCode (which we checked with `gcc --version`), installing [Homebrew](https://brew.sh), installing Python with `brew install python` and then checking it installed correctly with `python --version`, installing the requests library (`pip install requests`), and cloning the [fuzzy wuzzy](https://github.com/seatgeek/fuzzywuzzy) library. So while the terminal is generally easier to use, remember that you may encounter other scripts that don't run: you're probably missing packages such as those above. Our best advice is to Google the exact error message that pops up (if one does), and chances are you'll find the solution online. Remember to use our slides as a guide to prepping your workstation if you'd like to run our scripts on a different Mac than the one you used in the workshop.

   Pro-tip:  Mac's *do* come with Python installed by default, however we've gone to the effort of walking you through the creation of a development environment on your Mac laptop during this workshop so that we might (hopefully) avoid some potential "gotchas."  Long story short, if you feel like living (only slightly) dangerously, you can bypass these setup steps and see how far you get with the Python natively installed on your computer.  For more really helpful (if somewhat more than beginner-level) advice, see [The Hitchhiker's Guide to Python](http://python-guide-pt-br.readthedocs.io/en/latest/starting/install/osx/).

More FYIs to read  

   1. You'll always need at least two things to run one of our scripts: _the script itself_ and _the secrets.py file_, and they must both be in the same directory.
   2. A brief description of what each script does follows this long introduction. You used each of these scripts in the workshop itself, and so these descriptions will be familiar. These scripts, as opposed to the ones offered in the [_additional resources_](../master//additional%20resources) subfolder, above, are highly specific to the workshop, but if you're interested in learning Python, it may help to look at a script you've already used.


## Authenticating with [secrets.py](../master/secrets.py)
Note: You're only downloading/editing [secrets.py](../master/secrets.py); secrets._pyc_ is created automatically and you do not need to download or edit it.

Several of our scripts used for interacting with the ArchivesSpace API call a separate secrets.py that should be in the following format:

```
backendurl='YOURBACKENDURL'
user='YOURUSER'
password='YOURPASSWORD'
```
This example mimics an institution's instance of AS and a personal username:
```
backendurl='archivesspace.fakelibrary.edu:8089'
user='archivist21'
password='guest1234'
```
For the vagrant:
```
backendurl='localhost:8089'
user='admin'
password='admin'
```
Once you download, remember to change this secrets file as needed (i.e. you can't leave it set to the vagrant default and then try to connect to your instance of AS).


## [proPublica.py](../master/proPublica.py)
This script creates and saves a separate file called _proPublicaRecord.json_ containing the results of a proPublica search for "animal."

You can run this script by typing `python proPublica.py` in cygwin/the Mac terminal. Remember that you need to be running cygwin/the Mac terminal from the directory where the script is saved, and an output file named _proPublicaRecord.json_ will appear in the same directory.


## [postContainerProfiles.py](../master/postContainerProfiles.py)
This script sources from [containerProfiles.json](../master/containerProfiles.json) to post container profiles into ArchivesSpace. Both files must be downloaded to the same directory for this script to run. You can edit [containerProfiles.json](../master/containerProfiles.json) if you'd like to try posting in different profiles.

You can run this script by typing `python postContainerProfiles.py` in cygwin/the Mac terminal. Remember that you need to be running cygwin/the Mac terminal from the directory where the script, the source .json, and [secrets.py](../master/secrets.py) are all saved.

## [postBarcodes.py](../master/postBarcodes.py)
This script sources from [barcodes.csv](../master/barcodes.csv) to post barcodes into ArchivesSpace. Both files must be downloaded to the same directory for this script to run. You can edit [barcodes.csv](../master/barcodes.csv) if you'd like to try posting in different barcodes.

You can run this script by typing `python postBarcodes.py` in cygwin/the Mac terminal. Remember that you need to be running cygwin/the Mac terminal from the directory where the script, the source .csv, and [secrets.py](../master/secrets.py) are all saved.

## [asLinkProfiles.py](../master/asLinkProfiles.py)
This script assigns a single container profile to all the containers in a collection. This can be done in the actual AS interface, but serves as a good example of a more complex script. The first few actions of the script would be a good starting point for any API action that requires identifying all the containers associated with a single collection.

You can run this script by typing `python asLinkProfiles.py` in cygwin/the Mac terminal. Remember that you need to be running cygwin/the Mac terminal from the directory where the script and [secrets.py](../master/secrets.py) are both saved. This script first prompts the user for a resource number, goes and fetches all the containers associated with that resource, then prompts the user for a container profile number, and then creates the link between each container and that profile. Note that there must already be container profiles in AS for this script to work.

## [viafReconciliationCorporate.py](../master/viafReconciliationCorporate.py)
This script looks for a CSV named _organizations.csv_ and then uses VIAF's "corporateNames" index and retrieves VIAF, Library of Congress, and International Standard Name Identifier (ISNI) URIs for each potential match. These results are written to a new file named _viafCorporateResults.csv_. Credit for this script goes to our friend and colleague [Eric Hanson](https://github.com/ehanson8 "Eric's GitHub").

The format of the  _organizations.csv_ should look like this:

| name          |
| ------------- |
| Apple Inc.    |
| New York Public Library   |
| Library of Congress|


You can run this script by typing `python viafReconciliationPeople.py` in cygwin/the Mac terminal. Remember that you need to be running cygwin/the Mac terminal from the directory where the script and your _organizations.csv_ is saved. An output file named _viafCorporateResults.csv_ will appear in the same directory, which you can post to ASpace using [postVIAFOrganizations.py](../master/postVIAFOrganizations.py).


## [postVIAFOrganizations.py](../master/postVIAFOrganizations.py)
This script looks for the CSV called _viafCorporateResults.csv_ created by running [viafReconciliationCorporate.py](../master/viafReconciliationCorporate.py), converts those reults to JSON on the fly, and then posts the resulting corporate agent records to ArchivesSpace as new records (note: this script does not edit _pre-existing_ agent records, though that is possible with a script that first GETs the agents you have, runs them through the VIAF reconciliation, and then posts them back [saying all that isn't helpful if you don't have a script that does so, but that's how you start to game out what you need]).

You can run this script by typing `python postVIAFOrganizations.py` in cygwin/the Mac terminal. Remember that you need to be running cygwin/the Mac terminal from the directory where the script and your _viafCorporateResults.csv_ is saved.
