# Digital Forensic Investigation Diploma

## Module 1: Forensic Investigation Fundamental, Topic 6 :  Data Acquisition and Anti-Forensics (Concepts Only)

### Practice Exercise: Logical Imaging Using FTK Imager (Free Edition)  
**Objective**: Create and verify a logical image of selected folders from a live system while preserving file system metadata, then evaluate what is gained and lost compared with physical imaging.  
**Free tool**: FTK Imager (free edition)  
**Scenario**: You have authorisation to collect user documents and relevant application data from a workstation that must remain powered on. Full physical imaging is not permitted due to time, availability, or policy constraints.  

**Task**  
Install and run FTK Imager with administrative privileges.  
Go to File → Add Evidence Item and choose either:   
👉Logical Drive (captures a mounted volume’s files and metadata), or  
👉Contents of a Folder (more selective, reduces scope).  
Select a target scope, for example:  
👉C:\Users\Documents and Desktop  
👉A browser profile folder (only if permitted in your exercise setup)  
👉A test folder you create for this exercise  
Start the acquisition and export to an evidence container (commonly AD1) or a structured output directory, depending on your selected option.  
Enable creation of cryptographic hashes (use SHA-256 if available; otherwise MD5/SHA-1 as supported) and save the hash report.  
Use FTK Imager’s Verify function to confirm the exported image matches the recorded hash values.  
Document the live capture conditions: system time, logged-in user, and any relevant open applications.  

**what to check**  
👉Confirm the output includes allocated files and folder structure, but not unallocated or slack space.  
👉Note how well metadata is preserved (MAC times, ACLs, and any other attributes the tool and file system support).  
👉Compare speed and output size with what you would expect from a physical image.  
👉If you included an open file (for example, a text document left open), note whether it was captured and whether any timestamps changed.  

**Short Reflection Questions**    
👉What evidence would you lose by choosing logical imaging rather than physical imaging?    
👉Why can logical imaging be helpful when a volume is unlocked (including encrypted or virtualised storage)?    
👉What steps reduce the risks of live acquisition (scope control, minimal interaction, and thorough notes)?   

## Module 5: Hash Based Analysis, Topic: File & Content Recovery
### Creating Hashes with DigitalVolcano Hash ToolInstall and open the DigitalVolcano Hash Tool.
Create a new folder called Hash_Practice on your desktop.  
Add three different files into Hash_Practice (for example, a .docx, a .jpg, and a .zip).  
In the Hash Tool, add/import the three files (drag and drop into the window if supported).  
Select at least two hash algorithms (for example MD5 and SHA-256).  
Generate hashes for all three files.  
Copy the results into a simple log (file name, hash type, hash value).  
Pick one file and rename it (for example photo.jpg to photo_renamed.jpg).  
Hash the renamed file again using the same algorithm(s).  
Confirm the hash value is identical to the original (because the content has not changed).  
Open the same file and change one small piece of content (for example, add one letter to a text file, or edit one pixel in an image). Save it.  
Hash the edited file again using the same algorithm(s).  
Confirm the hash value is completely different from the original (because the content changed).  
Make a duplicate copy of one of the original files (copy–paste it in the folder).  
Hash both the original and the duplicate.  
Confirm the hashes match exactly, showing how hashes can be used to identify duplicates.  
Write a short conclusion in your notes explaining how this supports: integrity checking, identification against known-hash lists, and deduplication.  


## Module 5: Hash Based Analysis, Topic: System & User Artefacts
### Practical Exercise: USB History from the SYSTEM Hive Using USB Detective (usbdetective.com)  
Download USB Detective from usbdetective.com and open the application.  
Create a working folder called USB_Practical and place your evidence items there (at minimum, the Windows SYSTEM registry hive, and ideally a few LNK files or Jump Lists for correlation).  
In USB Detective, use the option to load a registry hive (or load SYSTEM hive) and select the SYSTEM hive from your dataset.   
Confirm the tool parses the hive successfully and shows a list of USB/storage artefacts.  
In USB Detective, locate the section for USB storage devices (USBSTOR) and identify at least two devices.  
For each device, record the make/model, serial number, and any connection/last seen timestamps shown by USB Detective.  
In USB Detective, locate the section for Mounted Devices (MountedDevices / volume mappings).  
Note any volume identifiers (Volume GUIDs) and the drive letter mappings where available.  
Correlate what you recorded by matching the USB device details (from the USBSTOR view in USB Detective) to the volume mappings (from the Mounted Devices view in USB Detective).  
Create a short table in your notes with columns: Device Make/Model, Serial, Volume GUID, Drive Letter, Last Seen.  
If you have LNK files or Jump Lists, open them in your preferred artefact viewer and look for targets referencing the relevant drive letter (for example, E:\) or a Volume GUID path.  
Match those references back to the device you identified in USB Detective, and note the file path(s) that suggest access from removable media.  
Write a brief finding statement (3–5 sentences) that answers: which USB device was connected, when it was last connected (as shown in USB Detective), what volume/drive letter it mapped to, and which shortcut or Jump List entry supports file access from that removable device.  

## Practivce Excercise
Download Eric Zimmerman’s Prefetch Parser (PECmd) from ericzimmerman.github.io and extract it to a working folder called Prefetch_Practical.  
Create a subfolder called PF_Files and place a set of Windows Prefetch files (*.pf) into it (from a forensic image or provided dataset).  
Open Command Prompt and navigate to the Prefetch_Practical folder.  
Run PECmd against the folder of Prefetch files (for example, pointing the tool at PF_Files).  
Review the output generated by PECmd and locate the following fields for at least three executables:  
o Executable name  
o First run time  
o Last run time  
o Run count  
o Referenced files and DLLs.  
6. Identify one executable with multiple run counts and note the most recent last run time  
7. Identify one executable with a single run count and record its first run time.  
8. Locate the Prefetch version number reported by the tool and confirm it aligns with a Windows 7–10 system (for example, versions in the 23–30 range).  
9. Using a provided Amcache artefact (or extracted Amcache output), look up the same executable name and record its first-seen or last-modified time.  
10. Compare the Amcache timestamp with the Prefetch last run time and note whether they support the same execution window.  
11. If a Security Event Log extract is available, locate Event ID 4688 entries for the same executable.    
12. Compare the process creation time in Event 4688 with the Prefetch last run time.  
13. Write a short summary explaining how Prefetch confirms execution, why some executions may not generate Prefetch files (for example, network or removable media), and how correlating Prefetch with Amcache and Event 4688 strengthens execution attribution.  

### Analysing Chromium-Family Browser Datastores with NirSoft BrowsingHistoryView  
Download BrowsingHistoryView from nirsoft.net and open the tool.  
If prompted, run the tool with appropriate permissions and select Load history from the current system or Load history from a custom folder (for provided evidence).  
Configure BrowsingHistoryView to include Chromium-based browsers (such as Chrome and Microsoft Edge) in the data source options.  
Refresh or load the data so the browsing records are displayed in the main results pane.  
Identify key fields shown by the tool, including URL, Title, Visit Time, Visit Count, Visit Type, and Web Browser.  
Sort the results by Web Browser to isolate Chrome or Edge records.  
Sort by Visit Time and confirm that timestamps are displayed in human-readable UTC (or note the local time offset applied by the tool).  
Select several entries and record their visit times, noting how time normalisation supports cross-artefact correlation.  
Examine the Visit Type or Transition column and identify examples of typed URLs versus referral-based visits.  
Use the Properties view for a selected entry to review additional metadata such as referrer or visit source (if available).  
If download history is present, filter or sort for download-related entries and record the source URL and local target path.  
Note any available indicators relating to download status, warnings, or interruptions, depending on what the tool exposes.  
Export a subset of results (for example, Chrome visits from a single day) to CSV.  
Review the exported data and identify which fields could be correlated with other artefacts (such as Prefetch, DNS cache, or file system timestamps).  
Write a short summary explaining how NirSoft BrowsingHistoryView abstracts underlying SQLite databases, why timestamp conversion is essential, and how visit source and download metadata support browsing and activity reconstruction.  















