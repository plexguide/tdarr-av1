# tdarr-av1

## BEAR with Me. I'm typing this just as a quick guide at 11:47PM/2347EST (so I'm tired).

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
   <br>a. C:\Tdarr\HandBrakeCLI.exe
   <br>b. C:\Tdarr\Tdarr_Node\assets\app\HandBrakeCLI.exe
   <br>c. C:\Tdarr\Tdarr_Server\assets\app\HandBrakeCLI.exe
5. Create a folder called: C:\cache
<br><br>

### HandBrake GUI
1. Open up Handbrake
2. Click file and select ANY VIDEO you have laying around. Can be anything, just have to pick something.
3. Click [Tools] > [Preferences] > [Video] > Checkmark - Allow use of the Nvidia NVENC Encoders AND-AND the Prefer use of .. > Click [< Back]
4. Summary Mini Tab > Format [MKV]
5. Dimensions > Resolution Limit [None]
6. Video
    <br>a. Video Encoder > AV1 10-bit (NVEnc)
    <br>b. Framerate > Same as source & Constant Framerate
    <br>c. Encoder Option > Encoder Present: Slowest (slide right)
    <br>d. Quality > Mine is at 40 (the smaller the number, the bigger the file... which is bad)
    <br>e. Audio > Codec (E-AC) Passthru [This may not be required, just a habit]
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

 <br>TIP 1: Test a really highend file.
 <br>TIP 2: Watch it on a 4k monitor, the results.
 <br>TIP 3: Don't get to hell bent on the #'s, if it looks really good and the file is smaller, your good.
 <br>TIP 4: Check the original file size and the new file size. If your new file is bigger... well your quality # is too small, if even... too small. You should at least have a 50% reduction.
<br><br>
### Tdarr Basic Setup
1. Click C:\Tdarr\Tdarr_Node\Tdarr_Node_Tray.exe
2. Click C:\Tdarr\Tdarr_Server\Tdarr_Server_Tray.exe
3. Access Tdarr via your browser - http://localhost:8096
4. On the main tab, scroll down and CHECK - Auto accept successful transcodes
5. Scrollback up to Node priority... click the node... some random name...
6. Transcode CPU: 0 ... TGPU: 1 (you can increase this, but do this after it all works)
7. Health Check: 2 ... GPU: 0
8. Look above and you will see [OPTIONS]... click and scroll down past the all the config stuff.
9. Make sure [NVENC] or [Any...] is select for the type of hardware and scroll down a tiny bit more.
10. Check... Allow GPU workers to do CPU tasks and then click the X in the upper right.
<br><br>
### Tdarr Library
1. At the very top, click Library (and yes you can create multiple ones later, but do this first and make sure it works!)
2. Click Library+ and then look at the mini tabs below.
3. [Source]: Turn on folder watch and SELECT WHERE YOUR MEDIA IS AT. Mine for example is z:/tv
4. [Transcode cache] - C:/cache
5. [Filters] Codes to Skip: AV1 (note you can put AV1,HEVC if you want to leave your x265 files alone)
6. [Transcode Options]: Disable all of them or delete them all... EXCEPT New File Size Check!
   <br>a. Click Community & Type 075 in the search and drag over ---- Community:Video Transcode Customisable
   <br>b. Click the Video Transcode Customisable Tab and options should come up.
   <br>c. codecs to exclude: av1 (or av1,hevc if you want to leave your x265 files alone)
   <br>d. transcode_arguements: --preset-import-gui -Z "t1"
   <br><br>
   NOTE: Pay attention to the t1. This is the name you created in handbrake. If you called it something else because you were special to start with, change it to THAT! If you create a new profile while tdarr SERVER,NODE is running... you must restart them again. If not, it's going to give you the finger!
   <br><br>e. output_container: .mkv
   <br>f. Click new container check.
   <br>g. Change upperbound to 99 and lowerBound to 5
   <br>h. Click the big green options button and click NEW FRESH SCAN, whatever the wording is!

### Final Notes
1. If you click your home page again, you should see stuff transcoding... if not... it's because you may have named something incorrectly.
2. I recommend to REBOOT the system if it doesn't work the first time... it's happened to me!
3. G to the very bottom and click SORT QUEUE BY: whatever you want
4. Good luck. If you push a change or do something in reddit, i'll update this
   
   


