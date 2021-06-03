# CSGO-OBS-fix-2020 (still working 05/2021)

## How and why this works
inside win-capture.dll is a function call to "get_programdatapath"

``get_programdata_path(path, L"obs-studio-hook\\");``

**which calls:**

```
SHGetFolderPathW(NULL, CSIDL_COMMON_APPDATA, NULL, \
				 SHGFP_TYPE_CURRENT, path);
where "CSIDL_COMMON_APPDATA" is defined as 0x23
```

**luckily right after that, we find:**

```
CSIDL_WINDOWS 0x24
```

**We just byte patched 0x23 to 0x24**
*upon starting obs, it should create a folder inside of the windows folder called obs-studio-hook and move the graphics-hook32.dll (and others) automatically.
The reason why the graphics-hook32.dll is also modified is, cuz for some reason the create_device function from the dxd11 dll crashes the game under trusted launch*

## Fix it! NOW! 
1. Download both files

2. win-capture.dll goes into:
C:\Program Files\obs-studio\obs-plugins\64bit\win-capture.dll

3. graphics-hook32.dll goes into:
C:\Program Files\obs-studio\data\obs-plugins\win-capture\graphics-hook32.dll


----  ----  ----  ----  ----  ----  ----    ----  ----  ----  ----  ----  ----  ----


> Streamlabs OBS: do exactly the same and replace these to files in the following paths:

C:\Program Files\Streamlabs OBS\resources\app.asar.unpacked\node_modules\obs-studio-node\obs-plugins\64bit  

and 

C:\Program Files\Streamlabs OBS\resources\app.asar.unpacked\node_modules\obs-studio-node\data\obs-plugins\win-capture
