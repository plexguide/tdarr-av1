# tdarr-av1

### Better Guide for Tdarr AV1  
[Main Intel ARC Guide](https://github.com/plexguide/Unraid_Intel-ARC_Deployment)

**WANT TO HELP?** CLICK THE ★ (STAR) in the upper-right corner! 

---

### Quick Info
**Note:** The main guide linked above is more comprehensive. This quick write-up focuses on Windows setups with an NVIDIA RTX 4000 series GPU. It may contain extra steps or precautions, but more information is often better than missing key details.

---

### For This
You will need:
1. A Windows 10/11 machine
2. A 4000 Series RTX GPU (4050 - 4090)
3. A decent processor

---

### Quick Checks
1. Update to the latest NVIDIA drivers.
2. Shut down both Tdarr Node and Tdarr Server before starting.
3. Follow these instructions exactly. Some steps may seem redundant, but they help avoid potential issues.

---

### Prepwork
1. **Download Tdarr** and extract all files to `C:\Tdarr`.
2. **Install HandBrake GUI** version 1.7.1 or later:  
   [HandBrake 1.7.1 GUI Download](https://handbrake.fr/rotation.php?file=HandBrake-1.7.1-x86_64-Win_GUI.exe)
3. **Download HandBrakeCLI** (Command Line version) and extract it to your desktop:  
   [HandBrakeCLI Download](https://handbrake.fr/rotation.php?file=HandBrakeCLI-1.7.1-win-x86_64.zip)
4. From the CLI version, copy `HandBrakeCLI.exe` and overwrite it in these 3 locations:  
   a. `C:\Tdarr\HandBrakeCLI.exe`  
   b. `C:\Tdarr\Tdarr_Node\assets\app\HandBrakeCLI.exe`  
   c. `C:\Tdarr\Tdarr_Server\assets\app\HandBrakeCLI.exe`
5. Create a folder: `C:\cache`

---

### HandBrake GUI Setup
1. Open HandBrake.
2. Click **File > Open Source** and pick any sample video file.
3. Go to **Tools > Preferences > Video**:  
   - Check “Allow use of the Nvidia NVENC encoders”  
   - Check “Prefer use of…” (if listed)  
   - Click **< Back**
4. **Summary Tab**: Set **Format** to **MKV**.
5. **Dimensions**: Set **Resolution Limit** to **None**.
6. **Video Settings**:  
   a. Video Encoder: **AV1 10-bit (NVEnc)**  
   b. Framerate: **Same as source** & **Constant Framerate**  
   c. Encoder Preset: **Slowest** (drag slider to the right)  
   d. Quality: Try **40** (larger number = smaller file size; too large can lower quality)  
   e. Audio: Codec: **E-AC3 Passthru** (recommended, not mandatory)
7. Click **Save New Preset**:  
   a. Name it **t1**  
   b. Resolution Limit: **None**  
   c. Audio Settings:  
      i. Track Selection Behavior: **All Matching Selected Languages**  
      ii. ‘Auto Passthru’ Behavior: **Check all options**  
      iii. Fallback Encoder: **None**  
      iv. Audio Encoder: **Auto Passthru** (to keep original audio codecs intact)  
      v. Additional Tracks: **Use All Tracks as Templates**  
   Click **Save**.

---

### Testing Before Moving On
This step is optional, but recommended:

- Try encoding your sample video in HandBrake with these settings to ensure quality is acceptable and file size reductions are noticeable.
- If the result is not satisfactory, adjust the Quality number lower or higher and re-test.
- Ensure you get at least ~50% space savings on high-quality content if possible.

---

### Tdarr Basic Setup
1. Run `C:\Tdarr\Tdarr_Node\Tdarr_Node_Tray.exe`.
2. Run `C:\Tdarr\Tdarr_Server\Tdarr_Server_Tray.exe`.
3. Open your browser and go to: `http://localhost:8096`.
4. In Tdarr, on the main page, scroll down and **check “Auto accept successful transcodes.”**
5. Scroll up to “Node priority…” and select your node (a random name).
6. Set **Transcode CPU:** `0` and **TGPU:** `1`. (You can increase this later once everything works.)
7. Health Check: Set CPU to `2` and GPU to `0`.
8. Click **[OPTIONS]** (top of the node settings), scroll down through the config, and ensure:  
   - Hardware Type: **NVENC** (or a suitable hardware option)  
   - Check “Allow GPU workers to do CPU tasks.”  
   Close this window by clicking the X in the upper right.

---

### Tdarr Library Setup
1. At the top of Tdarr, click **Library**.
2. Click **Library+** to create a new library.
3. **Source**: Enable folder watch and select your media directory (e.g., `z:\tv`).
4. **Transcode cache**: Set to `C:\cache`.
5. **Filters**: Add `AV1` to “Codecs to Skip” (if you only want to convert non-AV1 files).
6. **Transcode Options**:
   - Remove or disable all existing options except “New File Size Check.”
   - Go to **Community** and search for **075**. Drag over “Community: Video Transcode Customisable.”
   - Select the “Video Transcode Customisable” tab:
     a. Codecs to exclude: `av1` (or `av1,hevc` if you also want to skip HEVC)  
     b. transcode_arguments: `--preset-import-gui -Z "t1"`  
        (Use the preset name you saved in HandBrake. If you pick a different name, match it here.)
     c. output_container: `.mkv`  
     d. Enable “New container check.”  
     e. Set upperBound to `99` and lowerBound to `5`.
7. Click the big green **Options** button and start a new scan.

**Note:** If you create a new HandBrake preset while Tdarr is running, you must restart Tdarr Node and Server to load the new preset.

---

### Final Notes
1. Return to the Tdarr home page. You should see files being transcoded if all is configured correctly.
2. If nothing happens, re-check preset names, paths, and arguments. A system reboot may help.
3. Sort your queue by whatever metric you prefer at the bottom of the Tdarr page.
4. Good luck! Feel free to share your experiences or improvements.

