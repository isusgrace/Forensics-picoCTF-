Hi, Can you speak Thai ?

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ Glory of the Garden หมวด Forensics

# วิธีที่ 1

## Step 1 เปิดไฟล์

ข้อนี้จะมีไฟล์ .jpg มาให้ ให้เราทำการดาวน์โหลดและเปิดไฟล์ในที่ไหนก็ได้ ข้อนี้ไฟล์ภาพสามารถเปิดดูได้ปกติ

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/83a323ac-49fc-4dde-9d7e-9cc4ec2330a8" />

ภาพที่ 1

ผลลัพธ์จะเป็นดังภาพที่ 1

## Step 2 HEX Eeditor

เปิดเว็บไซต์นี้
```
https://hexed.it/
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5b9fd19d-e5a3-44d8-bb56-37a4ff0b3617" />

## อธิบาย

ข้อนี้ไม่มีอะไรมาก สังเกตตรง ASCII Interpretation แล้วเลื่อนลงให้สุดก็จะเจอ หรือกดตรง Search for ก็ได้ นี่เป็นเพียงแค่วิธีแรก มีวิธีที่ 2 อีก วิธีที่ 2 เราจะใช้ Kali Linux

# วิธีที่ 2

เอามาให้ดูทั้งดุ้นก่อน เดี๋ยวอธิบายแต่ละ process ให้

```
┌──(kali㉿kali)-[~/Downloads]
└─$ mkdir isusgrace05                                                    
                                                                                                                       
┌──(kali㉿kali)-[~/Downloads]
└─$ cd isusgrace05
                                                                                                                       
┌──(kali㉿kali)-[~/Downloads/isusgrace05]
└─$ wget https://challenge-files.picoctf.net/c_fickle_tempest/150b6eaad43200d3dc91f98c390e4c6168620b57d0b95a7e9d04c92910bbbe16/garden.jpg     
--2026-06-21 03:47:12--  https://challenge-files.picoctf.net/c_fickle_tempest/150b6eaad43200d3dc91f98c390e4c6168620b57d0b95a7e9d04c92910bbbe16/garden.jpg
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 18.239.134.106, 18.239.134.58, 18.239.134.85, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|18.239.134.106|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2295191 (2.2M) [application/octet-stream]
Saving to: ‘garden.jpg’

garden.jpg                    100%[================================================>]   2.19M  1.57MB/s    in 1.4s    

2026-06-21 03:47:14 (1.57 MB/s) - ‘garden.jpg’ saved [2295191/2295191]

                                                                                                                       
┌──(kali㉿kali)-[~/Downloads/isusgrace05]
└─$ file garden.jpg                                           
garden.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, baseline, precision 8, 2999x2249, components 3
                                                                                                                       
┌──(kali㉿kali)-[~/Downloads/isusgrace05]
└─$ strings garden.jpg   
JFIF
XICC_PROFILE
HLino
mntrRGB XYZ 
acspMSFT
IEC sRGB
-HP  
cprt
... (มันเยอะ ขอย่อไว้แต่เพียงเท่านี้ ซีเคร็ตอยู่ตอนท้าย)
s\]|."Ue
\qZf
Here is a flag: picoCTF{XXXXX} (ซีเคร็ตอยู่นี่ ไปทำเอาเอง)
```

## อธิบาย

## Step 1 mkdir ส่ง cd ส่ง wget

คำสั่ง mkdir ใช้สำหรับสร้างไดเรกทอรี (หรือโฟลเดอร์) ใหม่บนระบบปฏิบัติการคอมพิวเตอร์ ผ่าน Command Line โดยสามารถสร้างโฟลเดอร์เดียว สร้างหลายโฟลเดอร์พร้อมกัน สร้างโฟลเดอร์ซ้อนกันหลายชั้น และสร้างโฟลเดอร์พร้อมกำหนดสิทธิ์ได้ ในข้อนี้เราจะใช้คำสั่ง mkdir สร้างโฟลเดอร์เดียว
```
┌──(kali㉿kali)-[~/Downloads]
└─$ mkdir isusgrace05                                                    
```

คำสั่ง cd ใช้สำหรับเปลี่ยนไดเรกทอรีหรือโฟลเดอร์ปัจจุบันในเทอร์มินัล เอาแบบภาษาอังกฤษก็ Terminal
```
┌──(kali㉿kali)-[~/Downloads]
└─$ cd isusgrace05
```

คำสั่ง wget ใช้สำหรับดาวน์โหลดไฟล์ คัดลอกเว็บไซต์ และดึงข้อมูลจากอินเทอร์เน็ตผ่าน Command Line
```
┌──(kali㉿kali)-[~/Downloads/isusgrace05]
└─$ wget https://challenge-files.picoctf.net/c_fickle_tempest/150b6eaad43200d3dc91f98c390e4c6168620b57d0b95a7e9d04c92910bbbe16/garden.jpg     
--2026-06-21 03:47:12--  https://challenge-files.picoctf.net/c_fickle_tempest/150b6eaad43200d3dc91f98c390e4c6168620b57d0b95a7e9d04c92910bbbe16/garden.jpg
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 18.239.134.106, 18.239.134.58, 18.239.134.85, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|18.239.134.106|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2295191 (2.2M) [application/octet-stream]
Saving to: ‘garden.jpg’

garden.jpg                    100%[================================================>]   2.19M  1.57MB/s    in 1.4s    

2026-06-21 03:47:14 (1.57 MB/s) - ‘garden.jpg’ saved [2295191/2295191]
```

## Step 2 file

คำสั่ง file ใช้สำหรับตรวจสอบและระบุประเภทของไฟล์ โดยดูจากเนื้อหาและโครงสร้างข้อมูลภายในไฟล์นั้น ไม่ใช่ดูจากนามสกุล ซึ่งช่วยให้เราทราบว่าไฟล์นั้นคือไฟล์ประเภทใด
```
┌──(kali㉿kali)-[~/Downloads/isusgrace05]
└─$ file garden.jpg                                           
garden.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, baseline, precision 8, 2999x2249, components 3
```

## Step 3 strings

คำสั่ง strings ใช้สำหรับดึงข้อความที่มนุษย์อ่านได้ออกจากไฟล์ไบนารี
```
┌──(kali㉿kali)-[~/Downloads/isusgrace05]
└─$ strings garden.jpg   
JFIF
XICC_PROFILE
HLino
mntrRGB XYZ 
acspMSFT
IEC sRGB
-HP  
cprt
... (มันเยอะ ขอย่อไว้แต่เพียงเท่านี้ ซีเคร็ตอยู่ตอนท้าย)
s\]|."Ue
\qZf
Here is a flag: picoCTF{XXXXX} (ซีเคร็ตอยู่นี่ ไปทำเอาเอง)
```

ถ้าใช้แค่ strings เฉย ๆ มันจะยาวเลย สมมติถ้า Flag ซ่อนอยู่ส่วนอื่นก็เหนื่อยที่จะเลื่อนหา เพราะฉะนั้น ถ้าเรารู้ Format Flag ควรเพิ่ม grep ไปด้วย

คำสั่ง grep  เป็นคำสั่งสำหรับค้นหาข้อความหรือรูปแบบที่ต้องการภายในไฟล์ หรือผลลัพธ์จากคำสั่งอื่น โดยจะแสดงเฉพาะบรรทัดที่พบข้อมูลนั้นๆ ออกมา
```
┌──(kali㉿kali)-[~/Downloads/isusgrace05]
└─$ strings garden.jpg | grep "picoCTF"
Here is a flag: picoCTF{XXXXX}
```
ใช้แบบนี้จะไวกว่า

