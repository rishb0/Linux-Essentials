w get command.md 
Mastering the wget Command

Effortlessly Download Files from the Internet!

The wget command is a powerful and flexible command-line utility for downloading files from the web. It supports HTTP, HTTPS, and FTP protocols and is available on Linux, Unix-like systems, and Windows.


---

✨ Basic Syntax

wget [options] [URL]


---

🔥 Common Uses of wget

1️⃣ Download a Single File

wget https://example.com/file.zip

✅ Fetches file.zip from the specified URL.


---

2️⃣ Save File with a Different Name

wget -O newname.zip https://example.com/file.zip

✅ Downloads and saves it as newname.zip.


---

3️⃣ Resume an Interrupted Download

wget -c https://example.com/largefile.iso

✅ Continues an incomplete download without starting over.


---

4️⃣ Download Multiple Files from a List

wget -i filelist.txt

✅ Reads a list of URLs from filelist.txt and downloads them all.


---

5️⃣ Download a Website Recursively

wget -r https://example.com/

✅ Saves an entire website for offline use.


---

6️⃣ Limit Download Speed

wget --limit-rate=200k https://example.com/file.zip

✅ Restricts speed to 200 KB/s, useful for bandwidth control.


---

7️⃣ Download in the Background

wget -b https://example.com/largefile.iso

✅ Runs the download in the background while you continue working.


---

8️⃣ Download with Authentication

wget --user=username --password=password https://example.com/securefile.zip

✅ Downloads from password-protected sites.


---

9️⃣ Mirror an Entire Website

wget --mirror -p --convert-links -P ./localdir https://example.com/

✅ Creates a fully browsable local copy of a website.


---

🔟 Set a Custom User-Agent

wget --user-agent="Mozilla/5.0" https://example.com/file.zip

✅ Helps bypass wget restrictions on certain websites.


---

🛠 Checking Installed Version

wget --version

✅ Displays the installed wget version and details.

🔹 Now you're all set to harness the full power of wget! 🚀
