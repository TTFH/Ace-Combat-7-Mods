# Ace Combat 7 Mods  
  
## How to extract .PAK files  
Open the folder `Ace Combat 7 Skies Unknown\Game\Content\Paks\`  
Inside you'll find 12 files with names matching the next regex\*: `pakchunk\d-WindowsNoEditor(_0_P)?.pak`  
<sup>\*Q: What's a regex? A: It means the file names will be similar to that.</sup>  
The files that end with `_0_P` are used for DLCs, while the rest are for the base game.  
pakchunk0 is used for the weapons stats and pakchunk5 is used for skins, you can find the content of all the paks in the file `AC7FilesTree.txt` in this repository.  
To extract the files open `QuickBMS`  
Select the script `aes_script.bms`  
Select the pak file to extract, for example: `pakchunk0-WindowsNoEditor_0_P.pak`  
Select the folder to where extract the files, for example create a new one named `PAK00\`  
The file is encrypted using AES, but luckily for us, we know the decryption key.  
Press '0' to select the decryption key: `https://ace7.acecombat.jp/specia` from the list or type it, then press ENTER.  
Type ENTER to close the windows after the files are extracted.  
  
Open one of the extracted files with a text editor or a hex editor.  
For example open `Nimbus\Content\Blueprint\Weapons\Player\Base\plwp_admm_x0.uasset` with Notepad++  
The files starts with `AC7` (0x41434537 in HEX) and it's totally unreadable, this means the file is encrypted AGAIN!  
It's ~~almost~~ impossible to decrypt the files, since the algorithm is not public.  
  
## How to get the decrypted files  
- The files on PS4 are not encrypted, so if you have the game on a PS4 it should be as easy as opening the internal storage and copying the files.  
- Or someone ~~illegally~~ shared the files with you.  
  
### How to unzip files on Google Drive  
Let's say you have the files in Google Drive but you can't download them because your internet is really slow and the files are bigger than 3GiB.  
You can ask a friend to download the files for you and send them back in a pendrive or using IPoAC, you know, putting the files on a SD card and send it back to you on a homing pigeon, wait... that doesn't sound to realistic for ya? here is another way:  
  
Let's say you have a DLC.7z file containing all the DLC files (\*\_0\_P.pak) but you only want to download only one of them.  
1- Add a shortcut to your Drive (right click on the file and select that option)  
2- Add Google Colaboratory to your Drive (open the Google Workspace Marketplace and install Colaboratory)  
3- Create a ipynb script file (right click -> More -> Google Colaboratory)  
4- Mount your drive to the virtual machine, just type the next code and press Enter:  
```py  
from google.colab import drive  
drive.mount('/gdrive')  
```  
5- Change the directory to your mounted Drive  
`cd /gdrive/AC7_Decrypted`  
6- Extract the files, after extracting delete the files you don't need to reduce the used space on Drive  
`!7za x DLC.7z`  
7- Compress the file you want to reduce the size  
`!7za a -t7z PAK00.7z pakchunk0-ps4_0_p.pak`  
8- Donwload the compressed file  
  
Example file sizes:  
DLC.7z: 3.34 GiB  
pakchunk0-ps4_0_p.pak: 3.41 GiB  
PAK00.7z: 895.3 MiB  
  
Extract the 7z file with 7zip and then extract the pak file like above, this time you may not need to enter the AES key.  
  
## How to edit weapons stats  
The files containing the weapons stats are located in `Nimbus\Content\Blueprint\Weapons\Player\Base\`  
Let's select for example plwp_admm_x0.uasset and plwp_admm_x0.uexp (you need both uasset and uexp files) to edit the stats of the ADMM  
Copy those files to the `UnrealPak\` folder  
Open UAssetGUI and select version 4.18 on the top right corner  
Open plwp_admm_x0.uasset from the `UnrealPak\` folder  
Click on View -> Expand All  
Inside `Export Data / Export \* (Default__\*) / 1 (\*)` it's posible to edit values like Damage, LoadTime, LockonRange, etc.  
Save the file after editing it  
Backup files (.bak) are created, you can remove them  
  
## How to repack mods  
Edit `config.txt` to list the files and the paths, the path must start with `../../../Nimbus/`  
For example:  
```  
plwp_admm_x0.uasset ../../../Nimbus/Content/Blueprint/Weapons/Player/Base/plwp_admm_x0.uasset  
plwp_admm_x0.uexp ../../../Nimbus/Content/Blueprint/Weapons/Player/Base/plwp_admm_x0.uexp  
```  
You can use \* as a wildcard for filenames or extensions  
For example:  
```  
plwp_admm_x0.*  
*.uasset  
*.*  
```  
To pack the files execute the next command:  
`UnrealPak yourmod_P.pak -create=config.txt -compress`  
IMPORTANT: your mod must end with \_P if it edit DLC files  
  
## How to install Mods:  
1) Go to `Ace Combat 7 Skies Unknown\Game\Content\Paks\`  
2) Create a folder named `~mods` if it doesn't exists  
3) Copy `yourmod_P.pak` to that folder  
