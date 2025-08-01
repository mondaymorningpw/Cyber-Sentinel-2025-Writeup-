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

# Recon:

## Hoasted Toasted:
We have discovered what we believe is a North Torbian public website and have suspicions there is a secret internal-only site hidden there as well. Figure out how to connect to the hidden site and find the flag!   
The site is at https://not-torbian.ethtrader-ai.com/  

Upon clicking the link, I encountered an SSL/TLS certificate warning. I also got a “Your connection is not private” warning which got triggered because the browser doesn’t trust the website’s security certificate. For the purpose of the CTF challenge, I know it’s safe to bypass the warning to access the site.

Once I got to the site, I inspected the website’s certificate details.   
In the browser’s address bar, click the padlock icon. 

In certificate details, I looked at the DNS Name.

I couldn’t access the site at first https://definitelynotaflag.north.torbia/

In terminal, I put the command ping not-torbian.ethtrader-ai.com to get the IP address 34.86.60.228

Add it to my hosts file  
Run Notepad as administrator  
Open the hosts file in notepad

File > Open  
In the open dialog box, C:\Windows\System32\drivers\etc\  
Press enter  
Bottom right corner, look for a dropdown menu that’s probably default set to  "Text Documents (*.txt)".   
Click on this dropdown menu and change it to "All Files (*.*)" This allows us to see the hosts file.

Select the hosts file and then open it  
Scroll down to the bottom of the file  
Add the line 34.86.60.228 definitelynotaflag.north.torbia    
Save the file

Flush DNS cache so changes immediately take effect  

Open command prompt as administrator   
Type command ipconfig /flushdns

If successful, should look something like:   
C:\WINDOWS\system32>ipconfig /flushdns

Windows IP Configuration

Successfully flushed the DNS Resolver Cache.

Close web browser  
Reopen it

Flag: C1{vH0st_S4n_M4g1c_R3ve4l3d}

Note:  
For best practice, remove the custom entry from the hosts file once it’s no longer needed.    
Run notepad as administrator  
Open hosts file  
Delete the line that was added: 34.86.60.228 definitelynotaflag.north.torbia  
Save file  
Flush DNS cache by opening command prompt as administrator and using the command ipconfig /flushdns

# Web Security:

## Secret.txt Society:
Our team suspects that a Juche Jaguar developer accidentally left something interesting behind on a public site. You’ve been tasked with examining its structure. Can you uncover what the bots were told to ignore? Start with the usual entry points a crawler might explore. One disallowed path leads to a page where someone left behind more than just code.

Access the robots.txt file at https://juche.msoidentity.com/robots.txt 

Browse to the endpoint provided in this file to gather the flag: C1{r0b0ts_arent_4lways_p0lit3}

## Field Reports Mayhem:
We've gained access to the Juche Jaguar’s Field Reports archive through an operative's use of weak credentials. Upon logging in, the operative sees their previous field reports and can file new ones. Somewhere in here, I am sure some 'leet' agent stashed the Supreme Leader's secret pizza discount code!  
Log in to the portal at: http://35.245.106.190/login.html  
Use the credentials: 1234:spudpotato  

After checking the available reports of Agent 1234, there weren't any clues to what the flag was.   
The key was in the question “some ‘leet’ agent” therefore change the agent id from 1234 to 1337  
1337 = leet  
http://35.245.106.190/dashboard.php?id=1337&code=CD56EF

Now, in one of the reports: Report GH56IJ under Agent ID: 1337

Codename: EliteSpud  
Debrief: I extracted the Supreme Leader’s secret pizza-order discount code: C1{ID0R_F13LD_R3P0RT}. The pizza delivery arrived faster than any data packet.   

The flag is found in the report: C1{ID0R_F13LD_R3P0RT}



