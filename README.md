# Cyber-Sentinel-2025-Writeup-

# Introduction:
I participated in my first Capture-the-Flag (CTF) event in June 2025. The Cyber Sentinel Skills Challenge, hosted by Correlation One and sponsored by the U.S. The Department of Defense, includes a series of real-world challenges across various cybersecurity categories. Categories include forensics, malware/reverse engineering, networking & reconnaissance, open-source intelligence gathering (OSINT), and web security.

# Forensics:

## Behind the Beat:
Agents intercepted an audio file named message.mp3. It plays a single tone, but we have intel that a flag might be tucked away in the metadata fields of the file. Can you inspect the file and uncover the flag?
Download ffprobe to explore the metadata of the audio file. 

Go to terminal:  
Check if ffprobe is properly installed,   
Run command: ffprobe -version  
Locate and go to the directory of ffprobe and message.mp3  
Run command: ffprobe message.mp3  

Flag is hidden in the metadata: C1{metadata_tells_more}

## Hidden in Plain Sight:
Analysts recovered a suspicious image from a threat actor’s social media account. At first glance, it looks like an innocent selfie - but insider reports suggest that a flag might be hiding in the image metadata. Can you extract it?

Download exiftool to review the metadata of the selfie.  
Go to terminal:  
Check if exiftool is properly installed, run command: exiftool -ver  
Locate and go to the directory of exiftool and selfie.png  
Run command: exiftool selfie.png  

Flag is hidden in the metadata: C1{smile_youre_flagged}

