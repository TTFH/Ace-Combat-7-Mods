# Ace Combat 7 Mods

# How to create Mods:
1) Extract game files  
Open quickbms_4GB.exe  
Choose file unreal_tournament_4.bms  
Go to "Ace Combat 7 Skies Unknown\Game\Content\Paks\"  
Choose a .pak file containing the resources you want to modificate (skins are in pakchunk5-WindowsNoEditor.pak)  
Choose a folder to unpack  

2) Modificate the files  
If you want remplace the skin 01 for the skin 02 in the Su-30SM (because you don't have the skin 02 unlocked)  
Copy the file su30sm\01\su30sm_01_D.ubulk (00 is the skin 01, 01 is the skin 02, 02 is the skin 03 and so on)  
On the path Nimbus\Content\Vehicles\Aircraft\su30sm\00\su30sm_00_D.ubulk  

3) Repack the files  
Execute python3 u4pak.py pack skinpack.pak Nimbus

# How to install Mods:
1) Go to "Ace Combat 7 Skies Unknown\Game\Content\Paks\"
2) Create a folder named "~mods" without quotes
3) Copy skinpack.pak to that folder
