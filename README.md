# SandstormModsDownloader
# Original Bonelabs version by My-Bone-work
# https://github.com/My-bones-work/BoneLabModsDownloader
# Updated for Insurgency Sandstorm 1.21 by Joanna Wick
# Version: 0.1
# Date: 2026-06-12

A simple PowerShell script to automatically download all the mods you subscribed to on mod.io.

You will need to have let Sandstorm do an initial download of all mods before using this script.
The script cannot update the state.json file used by the game for giving mod information in the game
and this is why you have to let the game perform the initial downloads.

## Usage

1. Log in to https://mod.io
2. Go to "My account"
3. On the left side of the screen, click on `🔑 ACCESS`
4. Generate API access and OAuth access keys if you don't have them yet (you'll also have to first accept the terms and conditions)
5. Generate an OAuth access *token*. The token should have Read or Read+Write access. You should name it Sandstorm.
6. Download the zip file and extract it anywhere.
7. Right-click the `Download_Sandstorm_Mods.ps1` file and select "Run with PowerShell". It should ask you some things about platform 
   and install location and then your OAuth key

If you have done the setup once then it'll just read the settings from the configuration file it generated and everything 
should happen automatically. If you want to redo the setup, delete or rename `config.json` and it should show the prompts again.

Do not delete the token.cfg file as it contains the token you need to use this script.  If you do delete the file you
will need to go back to mod.io and create a NEW token.  Mod.io does not allow you to retrieve an old token after you create.
A new token will always have to be created if you lose the one you were using.

When you run it a window should open showing where your mod.io mod directory is located and asking if you would like to download
and extract the files there overwriting the existing files.  If you just want to test to make sure it is downloading the right
files just enter N(o) and a GUI will open letting you select a location.

If you re-run the script at a later date, it will check your subscriptions for updates and it'll only download mods from new 
subscriptions or mods which have been updated.

If you receive a Warning List of files this just indicates 7-Zip found some unexpected things and the archive should have
extracted without issue.

If you receive an Error List of files you should scroll back up through Powershell to find those files to get more
detailed information about the error.  You can also see if the files were extracted or not.

Common 7-Zip Unzipping Errors

Data Error / CRC Error: Meaning: The data inside the Zip archive is corrupted, meaning the compressed data does not match the 
file's original Cyclic Redundancy Check (CRC) value.

Can not open file as archive :Meaning: 7-Zip fails to recognize the file structure or format. This happens if the file download is 
incomplete, if the file extension is incorrect (e.g., trying to open a .gz file that is actually an XML document), or if the file 
was password-protected by a format 7-Zip doesn't fully support.

Headers Error: The header section of the archive—which contains critical metadata and structural information—is damaged.

Can not open output file / Access is denied: 7-Zip cannot create or write the destination file on your computer because of a 
Lack of administrator privileges on the destination folder.

Not enough space on disk: The destination drive doesn't have enough free storage to hold the unzipped files.

The most common errors will be CRC_Error or Lack of Drive Space.  I have found a couple of mod files that give CRC_Errors
and it looks like they were compressed and a bad CRC was created by whatever program was used to create the zip.

Change Log
==========

0.1 (2026-06-12) Initial Release

    1. Token variable moved to a token.cfg file so you will not need to get a new token if you delete the config.json and haven't
       saved the old token id.
    2. Added getting the mod directory from the %localappdata%\mod.io\globalsettings.json
    3. Added a GUI selector for location if you want the mod files unpacked to a different location for testing.
    4. A directory will now be created in the mod.io/mods directory using the mod_id for the download and unpack
       the mod files there.
    5. Removed Android platform support
    6. config.json now contains the mod.io mod_id number and last update time for each mod for faster lookup of the latest update.
    7. Mod.io json files have changed since the BoneLabModDownloader was created and it has been updated to work with the current system.
    8. Dropped the internal Powershell Extractor for Zip files as it was limited and would fail if the file was larger than 4GB or
       if there were file crc errors that didn't corrupt the archive.
    9. Added error reporting and a lot more information as mod file are being downloaded and extracted.
    10. If the numeric directory a mod is stored (ex: directory 123456 located in mod.io/254/mods/) has been deleted it will trigger 
       an automatic download and update when script has been executed.
    11. Editing state.json to reflect updated mod download

To Do
=====

    1. Create GUI to allow selecting of multiple mods that should be deleted
