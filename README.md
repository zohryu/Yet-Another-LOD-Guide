# Yet-Another-LOD-Guide
Yet another guide to help with Grass Caching and LOD Generation


||SKYRIM SE LOD GENERATION||


Disclaimer :
This guide is for my own personal usage originally, so please follow the settings with a grain of salt.

FOR LATER REFERENCE (these settings are to greatly, GREATLY increase generated LOD distance in-game, but the performance impact is extremely sizeable; please test it out AFTER all LOD process is completed).

↓ ↓ ↓  EXPERIMENTAL ↓ ↓ ↓ 

SkyrimPrefs.ini

[TerrainManager]

bShowLODInEditor=1

fBlockLevel0Distance=20000.0000

fBlockLevel1Distance=42000.0000

fBlockMaximumDistance=120000.0000

fSplitDistanceMult=0.7500

fTreeLoadDistance=25600.0000

to

[TerrainManager]

bShowLODInEditor=1

fBlockLevel0Distance=95000.0000

fBlockLevel1Distance=140000.0000

fBlockMaximumDistance=500000.0000

fSplitDistanceMult=4.0

fTreeLoadDistance=25600.0000

Skyrim.ini

uGridsToLoad=5

to

uGridsToLoad=7


^^^ EXPERIMENTAL ^^^

Step 1
Deactivation :

1. Disable all mods that should be turned off for LOD generation (these mods usually have a mention in their mod descriptions).
	This is particularly sensitive because it requires memory of which mods mentioned this, I can't help much.

2. Verify that ENB Complex Grass mods are disabled.

3. Ensure that all previous LOD outputs are disabled.

4. Make sure all Fog mods are disabled.

5. Verify that the following mods are disabled :
	
Mists of Tamriel

Blubbo Riften Outer Trees Visible

All Blubbo City Trees

All Flat World Map Framework + Maps

Water For ENB Vominheim

Lux Water for ENB Patch

All Nature of the Wildlands Patches



The above list is not exhaustive.
Read the mod descriptions!



Step 2
The Pre-Process for xLODGen :

1. Ensure that the textures you want to use are overriding everything else.
	This means that landscapes, architecture, etc MUST be properly overridden.
	This will allow proper grass meshing with proper landscape textures.

		If you are a Majestic Mountains user, this is the load order to follow :
			Majestic Mountains
			Majestic Mountains Double-Sided Patch
			Skyrim - A Mountainous Experience
			Majestic Mountains - More Accurate Collision
			Majestic Mountains - More Accurate Collision - AME Patch 
	
2. Turn on SSETerrainTamriel.esm

3. Ensure xLODGen settings are appropriate (Refer to STEP guide https://stepmodifications.org/wiki/SkyrimSE:2.1.0#DynDOLOD).

4. Run xLODGen and distribute the output to a new empty mod in MO2, then activate it.

5. Disable SSETerrainTamriel.esm



Step 3
The Grass Cache

PLEASE PLEASE PLEASE READ THIS

https://github.com/The-Animonculory/Modding-Resources/blob/main/Grass%20Lods.md#fixing-grass-data-w-grass-cache-fixes

You MUST read this guide, step-by-step, slowly, as you progress through the steps of this sister guide.
I've written this guide in tandem with it to help users (like myself) who have difficulty following the Github guide.

PREAMBLE : 

    	Ensure all .ini configurations for No Grass In Objects is correct at various steps
	
	Ensure all necessary pre-requisite mods are downloaded (from the Github guide first section).
	
	Ensure you have run the xEdit script to filter the appropriate grass-filled worldspaces to add to the GrassControl.Config.txt (Github guide second section)


1. Enable the grass mods you wish to use.

2. Load up your entire load order in xEdit.

3. Filter for GRASS records, send all records to a new .esp and name the .esp GRASS_BOUNDS_DATA.esp (refer to the Github guide third section).

4. Open GRASS_BOUNDS_DATA.esp in the Creation Kit, highlight all grass records from the left panel Object window (you can't miss it), right click and recalculate bounds.

5. Click on Data, Save, and exit.

6. Enable the following grass mods :

	The actual grass mods that you tested prior to this and will use (stacked in override order).
  
		Landscape Fixes For Grass Mods
	
		No Grassias - A Universal Grass Fix For Grass Mods
	
		Complimentary Grass Fixes
	
		No Grass in Caves

7. Ensure Grass Control & No Grass in Objects is turned on and properly configured (Refer to GitHub guide).

8. Ensure GRASS_BOUNDS_DATA.esp is enabled and below all grass related mods.

9. Ensure that Grass Cache Fixes is disabled at this point.

10. Ensure xLODGen output is enabled.

11. Disable ENB / ReShade, disable all direct texture replacers, set game resolution to 800x600 in SSE Display Tweaks.

12. Launch the PreCache Grass plugin from MO2, and wait a long time.

13. Once the output is complete, copy the .cgid grass files from the "overwrite" folder.

14. Move the .cgid files into a new mod called "GRASS LOD (.cgid)".

15. Activate the mod.

[IMPORTANT]

1. Make a copy of your grass cache and place it somewhere safe.

2. Create a new mod called "GRASS CACHE FIXES LOD (.gid)" and copy your grass cache (from "GRASS LOD (.cgid)") into there. Make sure that the data matches in both this mod and your Grass Cache mod.

3. Activate "Grass Cache Fixes" in your MO2 left pane.

4. Open the CGF mod and copy the 1_rename_cgid_to_gid.bat file into your Grass Data mod, placing it in the grass folder amongst the .cgid files.

5. Double click to run the bat file. Once it has finished, verify that all the files are .gid and not .cgid.


Step 4 [READ VERY CAREFULLY]
The Grass Cache Fixes

Step 1: Backup your grass cache.
In case you screw up, you don't want to have to redo your grass cache, as that's painful.

Step 2: Change the file extension of your grass cache from cgid to gid.
Copy the 1_rename_cgid_to_gid.bat file into your "grass" folder. Double-click to execute the batch file. This will rename all files in the directory containing the *.cgid file extension to *.gid.

Step 3: If using DynDOLOD (you should be!), set GrassGID=gid in DynDOLOD_SSE.ini
Navigate to DynDOLOD\Edit Scripts\DynDOLOD\DynDOLOD_SSE.ini and open with a text editor. Change the GrassGID setting to GrassGID=gid.

Step 4:
The Grass Cache Finals

You will now have several grass related output mods in your LOD section.
The original .cgid grass cache files in a mod called "GRASS LOD (.cgid)".
Another mod called "GRASS CACHE FIXES LOD (.gid)".

After having processed step 4, you will activate, in this order :

	Grass Control & No Grass In Objects
	GRASS_BOUNDS_DATA
	Grass Cache Fixes
	GRASS LOD (.cgid)
	GRASS CACHE FIXES LOD (.gid) [This one will go after all LOD related mods]

Step 6: Uncomment lines in the included INI file (Grass Cache Fixes.ini) to allow the game to natively load the grass cache gid files.
Uncomment bAllowCreateGrass, bAllowLoadGrass, bEnableGrassFade, and fGrassFadeRange settings by removing the semicolon in front.

Step 7: Set fGrassStartFadeDistance in your SkyrimPrefs.ini to 6144.
Ensuring that fGrassStartFadeDistance=6144 and fGrassFadeRange=14128 will make grass extend all the way to the maximum distance for uGridsToLoad=5.

Step 8: Test in game.
If you see grass in loaded cells and in LOD, you have done everything correctly. If you do not see grass in loaded cells, you do not have the grass cache properly installed. If you see grass in loaded cells but not in LOD, DynDOLOD did not detect the grass cache, probably because you missed step 3.



Step 6
TexGen and actual Grass LODS

1. Enable ENB Complex Grass mods for the mods you have selected.
	
2. Launch TexGen, making sure any troublesome mods are disabled beforehand.

3. Don't forget to disable the mods that SHOULD NOT be enabled.
    For mods that return errors, try error checking them xEdit, or cleaning them with the QuickAutoClean setting for xEdit.
    Otherwise, disable them (not recommended, but sometimes it "just works").

4. You can only use Mode 1 for Grass LOD generation, since this method cannot be used to extend the grass distance beyond the uGridsToLoad distance. Mode 2 will display a gap between the loaded grass and the LOD. DynDOLOD uses the gid grass cache files to generated grass LOD in object level 4 bto meshes.

5. With ENB Complex grass, HD Grass can be selected in TexGen.

	This part is difficult and annoying, but you may have to tweak brightness outputs for grass and trees.
  I can't help with this. It's trial and error unfortunately, and it depends on your ENB.

6. Run the TexGen process, then copy the output to a new empty mod called "TEXGEN OUTPUT" in MO2.

7. Activate the mod.



Step 7
Dyndolod

1. Ensure any mods that are giving errors with Dyndolod are either cleaned, error-checked, or disabled.

	The only water mods that should be enable are :
	
		Water for ENB (or whatever water mod you use)
		
		Water Effects Brightness and Reflection Fix
		
		FYX - Water Splash - Bright Water for ENB - WEBaRF (LOD)
		
		Majestic Mountains LOD pack MUST overwrite DynDOLOD Resources SE
		

2. Launch Dyndolod.

3. Enable all relevant settings in advanced mode.

	Tweaking the LOD brightness might be another annoyance.

4. Set the appropriate visual settings for LOD4, LOD8, LOD16, LOD32 for Mountains and Waterfalls.
  (Currently testing with setting Lod0 USE AT YOUR OWN CAUTION)
  
  FOR GREAT LOD SETTINGS, PLEASE READ THIS SECTION OF THE STEP GUIDE (https://stepmodifications.org/wiki/SkyrimSE:2.1.0#DynDOLOD)

5. Run Dyndolod.

6. Copy Dyndolod output into a new mod called "DYNDOLOD OUTPUT", and activate it.

7. Re-enable all disabled mods.

8. Put Dyndolod.ESM near the bottom of your .ESMs (which are at the top), put Dyndolod.esp + Occlusion.esp near the bottom but BEFORE Flat World Map Framework + Maps.

8. Run all synthesis patches.
