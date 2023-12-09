# tdarr-av1

### Quick Info
This write is to help you get going. There may be mistakes or I am taking extra steps, but more knowledge is better than nothing.
<br><br>

### For This
For this quick guide you will need:
1. Windows 10/11 Machine
2. A 4000 Series RTX GPU (4050 - 4090)
3. A decent processor

### Prepwork
1. Download Tdarr and unextract the file to C:\Tdarr 
2. Download and install the GUI handbrake like normal via: [https://handbrake.fr/rotation.php?file=HandBrake-1.7.1-x86_64-Win_GUI.exe](https://handbrake.fr/rotation.php?file=HandBrake-1.7.1-x86_64-Win_GUI.exe) >>> It needs to be 1.71+
3. This is the Command Line for Handbrake. Download this and extract to your desktop via: [https://handbrake.fr/downloads2.php](https://handbrake.fr/rotation.php?file=HandBrakeCLI-1.7.1-win-x86_64.zip)



Special Note 1: Enable automatic login on your PC. This is useful for recovery in the event of a system crash. If you're familiar with older programs like Plexguide, you'll recognize the superiority of Linux and Docker. Essentially, configure your machine to automatically resume operations after a reboot.

Read this: https://answers.microsoft.com/en-us/windows/forum/all/how-to-login-automatically-to-windows-11/c0e9301e-392e-445a-a5cb-f44d00289715.

Special Note 2: Some folks might scoff at AV1, dismissing it as overhyped, irrelevant, or not the way forward. But here's the deal: I've seen AV1 compress a 5GB file down to a mere 1.5GB with hardly any quality compromise. And no, you don't need to break the bank with a $1600 4090. If you hear the "not every device can play it" argument, remember that a plethora of devices, including Plex and JellyFin, support AV1. Most users already own AV1-compatible devices. For the few who don't? A simple solution: upgrade to a new Android box or Apple TV. Why should you invest more in storage when they can't spring for a basic device? Using Plex with an Intel processor or ARC GPU? Good news: they handle AV1 like champs. And a pro tip for your pals: enable maximum bandwidth mode to avoid transcoding and enjoy direct streaming.

PART I: Installing & Configuring Handbrake

a. When working with HandBrake, ensure you're using version 1.61 or later, and it should be the GUI version for the context of these instructions.

b. Upon launching HandBrake, select any video. This step is essential to create a profile.

c. Update the format to MKV.

d. For the video settings, remove the default resolution cap, which is set at 1080p. If overlooked, your 4K content will be downscaled to 1080p. Additionally, there's a default CF value set at 22. I've adjusted mine to 28. Remember: a higher value results in smaller file size but potentially reduced quality. The advantage of a test video is that you can preview the output before integrating with tdarr. Adjust and review until satisfied.

NOTE: Also change the format of the video to Intel 10 BIT AV1 something... you'll see it.

e. In the audio settings, switch it to 'pass through'.

f. Proceed to create a profile or its equivalent. Among the available options, ensure the resolution limit is set to 'none'.

g. In the audio section, select all audio formats. There's an option labeled 'first language'—change this to 'all'. Additionally, there's an audio setting (possibly labeled EC3 by default); modify this to 'AUTO pass through'. Failing to do so might lead to unintended audio conversions (or mp3 quality... you do not want that.

PART II: Tdarr

a. Deploy the Tdarr Server.

b. First click Libraries, then create a library. From there, ensure you to cick transcode options.

c. Disable the default: Migz-Transcode Using CPU && FFMPEG.

d. Add a plugin, click [Community] and type 075.

e. Implement the 075 custom configuration by clicking on it. Simply follow these steps and append the transcode argument: --preset-import-gui -Z "t4" and make sure to add codecs_to_exclude... put av1. The output container should be .mkv

NOTE: Remember, "t4" is a placeholder for the profile name you saved in HandBrake. It can be any name you've chosen. Ensure that the name is accurately placed between the quotation marks. For instance, if your profile is named "cat01", the argument should be: --preset-import-gui -Z "cat01".

f. Below your library name now, you should see an options button. Click Scan Fresh.

g. Deploy your Tdarr node and click the Tdarr tab.

h. From there, you should see some random node name. Click it.

* Set Transcode: CPU 0 - GPU 1
* Set Healthcheck: CPU 3 - GPU 1

Then click options above it, scroll downward and there is a hidden area under all that text. Make sure to check... allows GPU works to do CPU tasks.

i. That should be it. You should start seeing your stuff transcoding. Please submit changes to help fix this quick guide up. I'll run through it again for more cleanup and detail.


