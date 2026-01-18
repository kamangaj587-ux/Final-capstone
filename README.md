# Final-capstone
🛡️ Challenge 1: SQL Injection

Goal: Find a flag file using SQL injection.

Steps:
1. Identify the vulnerable input field — usually a login form or search box.
2. Test for SQL injection:
   - Try ' OR '1'='1 or admin'-- in the input field.
3. Use SQLMap for automation:
   `bash
   sqlmap -u "http://target-site.com/page.php?id=1" --dbs
   `
   - Replace the URL with the actual vulnerable endpoint.
4. Extract tables and data:
   `bash
   sqlmap -u "http://target-site.com/page.php?id=1" --dump
   `
5. Look for flag values — often stored in a table named flags, ctf, or secrets.

---

🌐 Challenge 2: Web Server Vulnerabilities

Goal: Investigate directories and find a flag file.

Steps:
1. Use Dirb or Gobuster to brute-force hidden directories:
   `bash
   dirb http://target-site.com/
   `
   or
   `bash
   gobuster dir -u http://target-site.com -w /usr/share/wordlists/dirb/common.txt
   `
2. Explore discovered directories — look for files like flag.txt, secret.php, or hidden/flag.html.
3. Use Burp Suite or browser to manually inspect and download the flag file.

---

📁 Challenge 3: Exploit Open Samba Shares

Goal: Access a flag file via open SMB shares.

Steps:
1. Scan for SMB shares:
   `bash
   smbclient -L //target-ip/ -N
   `
2. Connect to a share:
   `bash
   smbclient //target-ip/share-name -N
   `
3. Navigate and download:
   `bash
   get flag.txt
   `
   - Look inside folders like public, shared, or ctf.

---

📡 Challenge 4: Analyze Wireshark Capture

Goal: Find the location of a file containing flag info in a .pcap file.

Steps:
1. Open the .pcap file in Wireshark.
2. Use filters:
   - http or ftp to find file transfers.
   - tcp.stream eq 0 to follow conversations.
3. Follow TCP stream:
   - Right-click → Follow → TCP Stream.
   - Look for file paths or actual flag values in plain text.
4. Export or extract the file:
   - If a file was transferred, use “Export Objects” → “HTTP” or “FTP”.

---

✅ Final Step: Reporting Flags

Once you’ve captured all four flags, document them clearly:
- Flag 1: FLAG{sqlinjectionsuccess}
- Flag 2: FLAG{webdirectoryfound}
- Flag 3: FLAG{sambaaccessgranted}
- Flag 4: FLAG{packetanalysiscomplete
