Hi, Can you speak Thai ?

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ CanYouSee หมวด Forensics

Step 1 สร้าง Directory และนำเข้าไฟล์

```
mkdir <new directory>
```
ใช้คำสั่ง mkdir ใช้สำหรับสร้างไดเรกทอรี (หรือโฟลเดอร์) ใหม่บนระบบไฟล์
```
cd <new directory>
```
ตามด้วย คำสั่ง cd ใช้สำหรับเปลี่ยนไดเรกทอรีหรือโฟลเดอร์ปัจจุบันในเทอร์มินัล
```
wget <URL>
```
ตามด้วย คำสั่ง wget ใช้สำหรับดาวน์โหลดไฟล์จากอินเทอร์เน็ตโดยตรงผ่านบรรทัดคำสั่ง

```
┌──(kali㉿kali)-[~/Downloads]
└─$ mkdir isusgrace03

┌──(kali㉿kali)-[~/Downloads]
└─$ cd isusgrace03

┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ wget https://artifacts.picoctf.net/c_titan/131/unknown.zip
--2025-10-24 01:37:34--  https://artifacts.picoctf.net/c_titan/131/unknown.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 54.230.42.21, 54.230.42.116, 54.230.42.41, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|54.230.42.21|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2252296 (2.1M) [application/octet-stream]
Saving to: ‘unknown.zip’

unknown.zip             100%[============================>]   2.15M  1.55MB/s    in 1.4s    

2025-10-24 01:37:37 (1.55 MB/s) - ‘unknown.zip’ saved [2252296/2252296]
```

Step 2 unzip
```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ unzip unknown.zip          
Archive:  unknown.zip
  inflating: ukn_reality.jpg
```
คำสั่ง unzip ใช้สำหรับแตกไฟล์ที่ถูกบีบอัดในรูปแบบ .zip เพื่อดึงไฟล์และโฟลเดอร์ทั้งหมดออกมาจากไฟล์เก็บถาวรนั้น (ไฟล์ที่เราเลือกจะแตก)

Step 3 exiftool
```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ exiftool ukn_reality.jpg
ExifTool Version Number         : 13.10
File Name                       : ukn_reality.jpg
Directory                       : .
File Size                       : 2.3 MB
File Modification Date/Time     : 2024:03:11 20:05:57-04:00
File Access Date/Time           : 2024:03:11 20:05:57-04:00
File Inode Change Date/Time     : 2025:10:24 01:37:47-04:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
XMP Toolkit                     : Image::ExifTool 11.88
Attribution URL                 : cGljb0NURntNRTc0RDQ3QV9ISUREM05fZDhjMzgxZmR9Cg==
Image Width                     : 4308
Image Height                    : 2875
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 4308x2875
Megapixels                      : 12.4
```
คำสั่ง exiftool เราจะใช้มันสำหรับอ่านข้อมูลเมตา

ใช้สำหรับอ่าน, เขียน และแก้ไขข้อมูลเมตาที่ฝังอยู่ในไฟล์ เช่น รูปภาพ วิดีโอ และเสียง โดยข้อมูลเหล่านี้ได้แก่ วันที่ถ่าย, การตั้งค่ากล้อง, ตำแหน่ง GPS และข้อมูลอื่นๆ

สังเกตตรง Attribution URL ลักษณะแบบนี้ถูกเข้ารหัสด้วย Base64

<img width="1920" height="1080" alt="canseeyouu" src="https://github.com/user-attachments/assets/236860e5-17be-4a10-a6af-fa21fd5dda82" />

เราสามารถถอดรหัสได้ โดยการใช้ CyberChef
```
echo "cGljb0NURntNRTc0RDQ3QV9ISUREM05fZDhjMzgxZmR9Cg==" | base64 -d
```
หรือใช้คำสั่ง echo บน kali linux
```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ echo "cGljb0NURntNRTc0RDQ3QV9ISUREM05fZDhjMzgxZmR9Cg==" | base64 -d
picoCTF{XXXXX}
```

XXXXX ไม่ใช้ flag นะ คือปิดไว้ จะได้ทำเอง

เพิ่มเติม

- สังเกต Hints ที่บอกว่า "How can you view the information about the picture?" นั่นทำให้เรารู้ว่าต้องใช้ exiftool เพราะ exiftool จะแสดงข้อมูลเมตาทั้งหมดในไฟล์ เมื่อเราใช้มัน
