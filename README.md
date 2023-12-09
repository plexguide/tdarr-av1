# tdarr-av1

### Quick Info
This write is to help you get going. There may be mistakes or I am taking extra steps, but more knowledge is better than nothing.
<br><br>

### For This
For this quick guide you will need:
1. Windows 10/11 Machine
2. A 4000 Series RTX GPU (4050 - 4090)
3. A decent processor
<br><br>

### Quick Checks
1. Make sure to update to the latest version of the Nvidea Drivers
2. Make sure Tdarr Node and Server are shutdown
3. Follow the instructions exact. Again, may be extra steps but it prevents the... well G... I forgot to do this.
<br><br>

### Prepwork
1. Download Tdarr and unextract all the files to C:\Tdarr 
2. Download and install the GUI version of Handbrake (has to be 1.71 or above): [https://handbrake.fr/rotation.php?file=HandBrake-1.7.1-x86_64-Win_GUI.exe](https://handbrake.fr/rotation.php?file=HandBrake-1.7.1-x86_64-Win_GUI.exe) 
3. This is the Command Line for Handbrake. Download this and extract to your desktop via: [https://handbrake.fr/downloads2.php](https://handbrake.fr/rotation.php?file=HandBrakeCLI-1.7.1-win-x86_64.zip)
4. From the CLI version of handbrake (HandBrakeCLI.exe), overwrite the 3 from three different locations (do not be special, just do it):
   a. C:\Tdarr\HandBrakeCLI.exe
   b. C:\Tdarr\Tdarr_Node\assets\app\HandBrakeCLI.exe
   c. C:\Tdarr\Tdarr_Server\assets\app\HandBrakeCLI.exe
5. Create a folder called: C:\cache
<br><br>

### HandBrake GUI
1. Open up Handbrake
2. Click file and select ANY VIDEO you have laying around. Can be anything, just have to pick something.
3. Click [Tools] > [Preferences] > [Video] > Checkmark - Allow use of the Nvidia NVENC Encoders AND-AND the Prefer use of .. > Click [< Back]
4. Summary Mini Tab > Format [MKV]
5. Dimensions > Resolution Limit [None]
6. Video
   a. Video Encoder > AV1 10-bit (NVEnc)
   b. Framerate > Same as source & Constant Framerate
   c. Encoder Option > Encoder Present: Slowest (slide right)
   d. Quality > Mine is at 40 (the smaller the number, the bigger the file... which is bad)
   e. Audio > Codec (E-AC) Passthru [This may not be required, just a habit]
7. Save New Preset Button
   a. Name: t1
   b. Resolution Limit: [None]
   c. Audio:
     <br>i. Track Selection Behavior: [All Matching Selected Languages]
     <br>ii. 'Auto Passthru' Behavior: [Check All of them, yes all of them]
     <br>iii. Fallback Encoder: [None]
     <br>iv. Audio encoder settings for each chosen track: Codec > [Auto Passthru] ... goof this and all your videos may turn into MP3 codecs.
     <br>v. For Additioinal Tracks: Use All Tracks as Templates
     <br>vi. Click Save
<br><br>
### Testing Before Moving On

This can all be skipped, but you can see the results before executing all of this. Has nothing to do with Tdarr. See Browser at the bottom, that's where your TEST file will save to!

Remember how I said to select a video, you can actually hit the start encode button and let it run and you can check the quality and tweak how you like. You can change the quality number to see where you want it.

TIP 1: Test a really highend file.
TIP 2: Watch it on a 4k monitor, the results.
TIP 3: Don't get to hell bent on the #'s, if it looks really good and the file is smaller, your good.
TIP 4: Check the original file size and the new file size. If your new file is bigger... well your quality # is too small, if even... too small. You should at least have a 50% reduction.
<br><br>
### 


