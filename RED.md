Hi, Can you speak Thai ?

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ RED หมวด Forensics 

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
└─$ mkdir isusgrace03   
                                                                                             
┌──(kali㉿kali)-[~]
└─$ cd isusgrace03
                                                                                             
┌──(kali㉿kali)-[~/isusgrace03]
└─$ wget https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png
--2025-10-20 10:16:57--  https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 18.239.134.85, 18.239.134.106, 18.239.134.126, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|18.239.134.85|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 796 [application/octet-stream]
Saving to: ‘red.png’

red.png                 100%[============================>]     796  --.-KB/s    in 0s      

2025-10-20 10:16:59 (38.7 MB/s) - ‘red.png’ saved [796/796]
```

Step 2 zsteg
Zsteg คือ เครื่องมือสำหรับวิเคราะห์และตรวจจับข้อมูลที่ถูกซ่อนไว้ในไฟล์ภาพ โดยเฉพาะไฟล์ประเภท PNG และ BMP
```
┌──(kali㉿kali)-[~/isusgrace03]
└─$ zsteg -a red.png
meta Poem           .. text: "Crimson heart, vibrant and bold,\nHearts flutter at your sight.\nEvenings glow softly red,\nCherries burst with sweet life.\nKisses linger with your warmth.\nLove deep as merlot.\nScarlet leaves falling softly,\nBold in every stroke."
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="
b1,rgba,msb,xy      .. file: OpenPGP Public Key
b2,g,lsb,xy         .. text: "ET@UETPETUUT@TUUTD@PDUDDDPE"
b2,rgb,lsb,xy       .. file: OpenPGP Secret Key
b2,bgr,msb,xy       .. file: OpenPGP Public Key
b2,rgba,lsb,xy      .. file: OpenPGP Secret Key
b2,rgba,msb,xy      .. text: "CIkiiiII"
b2,abgr,lsb,xy      .. file: OpenPGP Secret Key
b2,abgr,msb,xy      .. text: "iiiaakikk"
b3,rgba,msb,xy      .. text: "#wb#wp#7p"
b3,abgr,msb,xy      .. text: "7r'wb#7p"
b3p,r,msb,xy        .. text: "{[{_[_[_{_["
b3p,g,lsb,xy        .. text: "%!%! !%!%%%!"
b3p,rgb,lsb,xy      .. file: OpenPGP Secret Key
b3p,bgr,msb,xy      .. text: "ddd``dddd"
b3p,abgr,lsb,xy     .. file: OpenPGP Secret Key
b4,b,lsb,xy         .. file: 0421 Alliant compact executable not stripped
b5p,b,lsb,xy        .. file: PDP-11 separate I&D executable not stripped - version 9
b6,rgb,msb,xy       .. file: Applesoft BASIC program data, first line number 126
b6p,b,lsb,xy        .. file: PDP-11 old overlay
b7,g,lsb,xy         .. file: Targa image data - RLE 33088 x 2 x 8 +8192 - right " @\200\002\004"                                                                                          
b8,r,msb,xy         .. file: RDI Acoustic Doppler Current Profiler (ADCP)
b8,g,lsb,xy         .. file: Targa image data - Map 257 x 257 x 1 +1 "\001\001\001\001\001"
b8,b,lsb,xy         .. file: PDP-11 UNIX/RT ldp
b8,rgb,lsb,xy       .. file: Targa image data - Map (254-65025) 510 x 65281 x 1 +65024 +257 "\376\001\001\377"                                                                            
b8,bgr,lsb,xy       .. file: PDP-11 UNIX/RT ldp
b8,rgba,lsb,xy      .. file: MySQL table definition file Version 1, MySQL version 16908286
b8,abgr,lsb,xy      .. file: MySQL table definition file Version 1, MySQL version 16908030
b1,bgr,msb,xy,prime .. file: OpenPGP Public Key
...
```
จริง ๆ มันมีต่อยาวกว่านี้มาก ที่ฉันคัดลอกมามันคือส่วนที่น่าสนใจ โฟกัสตรงที่
```
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="
```
มันคือ flag ที่ถูกเข้ารหัสด้วย Base64 โดยมันถูกวางติดกันยาว ๆ ในการถอดรหัสเราสามารถเข้า CyberChef 
<img width="1920" height="1080" alt="ลบแล้ว" src="https://github.com/user-attachments/assets/d0d7472c-3968-4fea-b407-5a249043f964" />
หรือใช้คำสั่ง echo บน kali linux
```
echo "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==" | base64 -d
```
จะได้
```
┌──(kali㉿kali)-[~/isusgrace03]
└─$ echo "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==" | base64 -d
picoCTF{XXXXX}picoCTF{XXXXX}picoCTF{XXXXX}picoCTF{XXXXX}
```
จากนั้นคัดลอกมาแค่ 1 ข้อความ เพื่อส่ง flag ใน picoCTF

XXXXX ไม่ใช้ flag นะ คือปิดไว้ จะได้ทำเอง

เพิ่มเติม
- ที่ใช้ zsteg เนื่องจากเรากำลังจัดการกับไฟล์ .PNG ฉันคิดว่ามันเป็นตัวเลือกที่ดีอีกหนึ่งตัวเลือก เนื่องจาก zsteg เป็นเครื่องมือที่ใช้สำหรับการตรวจจับ Steganography ในรูปภาพ PNG และ BMP + ใช้ exiftool แล้วไม่เจอสิ่งที่น่าสงสัย
```
echo -n "ข้อความของคุณ" | base64
```
คำสั่งนี้ใช้สำหรับเข้ารหัสข้อความด้วย Base64
```
echo "ข้อความของคุณ" | base64 -d
```
คำสั่งนี้ใช้สำหรับถอดรหัสข้อความที่ถูกเข้ารหัสด้วย Base64
