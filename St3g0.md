Hi, Can you speak Thai ?

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ St3g0 หมวด Forensics

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
└─$ wget https://artifacts.picoctf.net/c/215/pico.flag.png
--2025-10-23 23:33:23--  https://artifacts.picoctf.net/c/215/pico.flag.png
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 54.230.42.116, 54.230.42.21, 54.230.42.13, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|54.230.42.116|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 13438 (13K) [application/octet-stream]
Saving to: ‘pico.flag.png’

pico.flag.png           100%[============================>]  13.12K  --.-KB/s    in 0s      

2025-10-23 23:33:24 (331 MB/s) - ‘pico.flag.png’ saved [13438/13438]
```

Step 2 zsteg

Zsteg คือ เครื่องมือสำหรับวิเคราะห์และตรวจจับข้อมูลที่ถูกซ่อนไว้ในไฟล์ภาพ โดยเฉพาะไฟล์ประเภท PNG และ BMP

```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ zsteg -a pico.flag.png
b1,r,lsb,xy         .. text: "~__B>wV_G@"
b1,rgb,lsb,xy       .. text: "picoCTF{7h3r3_15_n0_5p00n_96ae0ac1}$t3g0"
b1,abgr,lsb,xy      .. text: "E2A5q4E%uSA"
b2,b,lsb,xy         .. text: "AAPAAQTAAA"
b2,b,msb,xy         .. text: "HWUUUUUU"
b3,r,lsb,xy         .. file: gfxboot compiled html help file
b3p,r,lsb,xy        .. text: "Kooooooooohp"
b3p,b,lsb,xy        .. text: "OJNnNH4%"
b3p,b,msb,xy        .. text: ["R" repeated 10 times]
b3p,rgb,lsb,xy      .. text: "yz{[bB~Z{z_[zF"
b3p,bgr,lsb,xy      .. text: ";[{zCB_Z{[~z[F}_[["
b3p,abgr,lsb,xy     .. file: Hitachi SH big-endian COFF object file, no relocation info, no line number info, not stripped, 1 section, symbol offset=0x5050100, 67371264 symbols, optional header size 260, created Sun Jan  4 00:49:09 1970                                           
b4,r,lsb,xy         .. file: Targa image data (16-273) 65536 x 4097 x 1 +4352 +4369 - 1-bit alpha - right "\021\020\001\001\021\021\001\001\021\021\001"
...
```
จริง ๆ มันมีต่อยาวกว่านี้มาก ที่ฉันคัดลอกมามันคือส่วนที่น่าสนใจ โฟกัสตรงที่
```
b1,rgb,lsb,xy       .. text: "picoCTF{XXXXX}$t3g0"
```
XXXXX ไม่ใช้ flag นะ คือปิดไว้ จะได้ทำเอง

เพิ่มเติม

- ที่ใช้ zsteg เนื่องจากเรากำลังจัดการกับไฟล์ .PNG ฉันคิดว่ามันเป็นตัวเลือกที่ดีอีกหนึ่งตัวเลือก เนื่องจาก zsteg เป็นเครื่องมือที่ใช้สำหรับการตรวจจับ Steganography ในรูปภาพ PNG และ BMP + ใช้ exiftool แล้วไม่เจอสิ่งที่น่าสงสัย
