# Digital Forensic Investigation Diploma

## Module 1, Topic 6 :  Data Acquisition and Anti-Forensics (Concepts Only)

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

## Module 5: Hash Based Analysis
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

 

