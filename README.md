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

# Malware/Reverse Engineering:

## Hardcoded Lies:
The malware sample doesn’t appear to print anything useful. But our threat intel team believes it holds a hardcoded configuration string. Can you pull on some strings to retrieve it?

Using hard coded strings may reveal information about the binary. We need to search for these 'strings' inside of the binary to find the flag.

Flag is hidden in the text: C1{h4rdc0ded_but_0verlooked}

## Encoded Evidence:
We've intercepted a suspicious script file. It appears to be a placeholder for some kind of malware delivery mechanism, but the actual payload seems to be hosted somewhere else. Analysts believe a flag is hidden by this script. Can you locate and decode it?

Try opening this file with Notepad or VS Code to inspect the contents first. When reviewing the information, note that there is a URL to Pastebin - this URL hosts some Base64 encoded information.

I needed to open a VBScript script file but I was getting a security warning. 
Since the script is for CTF and learning, there’s no actual malware. 
To bypass it, I had to view the code in Notepad so it would not trigger the execution warning.

Use CyberChef to decode Base64 string to get the flag: C1{n0_d3bug_n0_p4yn}

# Networking:

## Packet Whisperer:
Our blue team intercepted a network capture file. It contains unencrypted HTTP traffic. While skimming through it, analysts believe someone accidentally exposed their login credentials in plain text. Review the PCAP to find the password that the user logged in with.

Use Wireshark to open this PCAP file. 

Once open, right click the HTTP streams. Choose Follow > TCP Stream to view information sent across the wire.

Upon closer look, we see password=C1%7Bmaybe_TLS_would_be_nice%7D

The password is URL encoded, when decoded we get the flag: C1{maybe_TLS_would_be_nice}

# OSINT:

## Cafe Confidential:
Two photos were posted minutes apart by someone of interest. One shows them enjoying a slice of cake in a boutique café; the other captures a well-known landmark in the background. We believe both photos were taken on the same outing. Can you determine exactly which café they visited, and where is it?

Flag format is: C1{Cafe Name_Street Name}  
For example, Tom's Cafe located at 31 Mitchell Rd, Boston, MA would be C1{Tom's_Mitchell}.

Used Google’s “Search by Image” mode to find where the pictures were taken.  
Additional use of online maps to determine if locations are closely related.   
Based on the image of the Matilda cake and the Harrods location, and confirmed with search results, the cafe is Parker's, located at Jumeirah Lowndes Hotel, 21 Lowndes St, London SW1X 9ES, United Kingdom.

The flag is: C1{Parker's_Lowndes}

## Problems in North TORbia:
We were given a ransom note but none of our files were encrypted. Regardless, could you run it back and see what information could be gleaned from it?

Upon opening the note, the key line to look at in the text is:  
SEND PAYMENT TO:  
http://jjpwn5u6ozdmxjurfitt42hns3qovikeyhocx5b2byoxgupnuzd2vkid.onion/

The URL is a .onion address.  
Download the Tor Browser to visit the onion address.

Control + U to view the source code.

Flag is hidden in the source code: C1{h1dd3n_f13lds_0f_0n10ns}

