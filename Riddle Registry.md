Hi, Can you speak Thai ? 

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ Riddle Registry หมวด Forensics

Step 1 สร้าง Directory และนำเข้าไฟล์

ใช้คำสั่ง mkdir ใช้สำหรับสร้างไดเรกทอรี (หรือโฟลเดอร์) ใหม่บนระบบไฟล์
```
mkdir <new directory>
```
ตามด้วย คำสั่ง cd ใช้สำหรับเปลี่ยนไดเรกทอรีหรือโฟลเดอร์ปัจจุบันในเทอร์มินัล
```
cd <new directory>
```
ตามด้วย คำสั่ง wget ใช้สำหรับดาวน์โหลดไฟล์จากอินเทอร์เน็ตโดยตรงผ่านบรรทัดคำสั่ง
```
┌──(kali㉿kali)-[~]
└─$ mkdir isusgrace02   
                                                                                             
┌──(kali㉿kali)-[~]
└─$ cd isusgrace02
                                                                                             
┌──(kali㉿kali)-[~/isusgrace02]
└─$ wget https://challenge-files.picoctf.net/c_saffron_estate/8273e5c46d44ea7def776d9b93d8b29ffd0388423443149d1313aeb13f8add39/confidential.pdf
--2025-10-17 08:44:52--  https://challenge-files.picoctf.net/c_saffron_estate/8273e5c46d44ea7def776d9b93d8b29ffd0388423443149d1313aeb13f8add39/confidential.pdf
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 18.239.134.58, 18.239.134.126, 18.239.134.85, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|18.239.134.58|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 182705 (178K) [application/octet-stream]
Saving to: ‘confidential.pdf’

confidential.pdf        100%[============================>] 178.42K   405KB/s    in 0.4s    

2025-10-17 08:44:53 (405 KB/s) - ‘confidential.pdf’ saved [182705/182705]
```

Step 2 exiftool

ใช้คำสั่ง exiftool เราจะใช้มันสำหรับอ่านข้อมูลเมตา
```
┌──(kali㉿kali)-[~/isusgrace02]
└─$ exiftool confidential.pdf                      
ExifTool Version Number         : 13.10
File Name                       : confidential.pdf
Directory                       : .
File Size                       : 183 kB
File Modification Date/Time     : 2025:09:29 17:29:23-04:00
File Access Date/Time           : 2025:10:17 08:44:53-04:00
File Inode Change Date/Time     : 2025:10:17 08:44:53-04:00
File Permissions                : -rw-rw-r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Page Count                      : 1
Producer                        : PyPDF2
Author                          : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=
```
สังเกตตรง Author ลักษณะแบบนี้ต้องถอดรหัสด้วย Base64 โดยการเข้า CyberChef
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f2974a97-c8b4-4b24-b6b0-51b8a860710d" />
หรือใช้คำสั่ง echo บน kali linux
```
echo "cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=" | base64 -d
```
จะได้
```
┌──(kali㉿kali)-[~/isusgrace02]
└─$ echo "cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=" | base64 -d
picoCTF{XXXXX}
```
XXXXX ไม่ใช่ flag นะ คือปิดไว้ จะได้ทำเอง

เพิ่มเติม
- สังเกตส่วนหนึ่งของโจทย์ที่บอกว่า "and uncover the flag within the metadata." นั่นทำให้เรารู้ว่าต้องใช้ exiftool
```
echo -n "ข้อความของคุณ" | base64
```
คำสั่งนี้ใช้สำหรับเข้ารหัสข้อความด้วย Base64
```
echo "ข้อความของคุณ" | base64 -d
```
คำสั่งนี้ใช้สำหรับถอดรหัสข้อความที่ถูกเข้ารหัสด้วย Base64
