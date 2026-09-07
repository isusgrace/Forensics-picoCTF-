Hi, Can you speak Thai ?

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ Corrupted file หมวด Forensics

# Step 1 สำรวจไฟล์

ข้อนี้จะให้ไฟล์เรามา 1 ไฟล์ เราจะคำสั่ง file ในการดูชนิดของไฟล์

```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ file file                                                              
file: data
```

data...ไม่สามารถระบุชนิดหรือรูปแบบของไฟล์ได้อย่างชัดเจน เจอแบบนี้ก็เริ่ดเลยเตง งั้นมาลอง strings กัน

```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ strings file.jpg
JFIF
 $.' ",#
(7),01444
'9=82<.342
!22222222222222222222222222222222222222222222222222
$3br
%&'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
        #3R
&'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
<Sqaa{w&
neS=
T ^f
(ajI
toQ\
so%z
TM\R
F5XV4Gee
}OSW
1$G[_
{mb:
yFm*
&'2!
pPrKd
e3#4
J(qOt
_]\]@
7cps
udU`{u
#O,*
nyg,
I+JM
```

อ้าว คุณพรี่บอกเป็นไฟล์ JPEG

# Step 2 xxd

จาก Step 1 เราจะมาดู Hexdump ต่อ มันจะต้องมีจะเอยจะใดจะอี้จะอ้ายอะไรบางอย่างซ่อนอยู่
```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ head -c 20 file | xxd    
00000000: 5c78 ffe0 0010 4a46 4946 0001 0100 0001  \x....JFIF......
00000010: 0001 0000
```

ชัดเจน ผู้ต้องหาคือ 5c78 ffe0 ถ้าเป็นไฟล์ JPEG จะต้องเป็น FF D8 FF E0 หรือ FF D8 FF E1 ในส่วนของรายละเอียด เดี๋ยวอธิบายเพิ่ม

ในเมื่อเรารู้แล้ว ว่าตรงนี้ผิด เราสามารถแก้ไขได้ โดยใช้ Hex Editor หรือจะสร้างโค้ด Python มาแก้ก็ได้ แต่ส่วนตัวจะใช้ Hex Editor

<img width="1920" height="1031" alt="image" src="https://github.com/user-attachments/assets/17097453-f9bd-41d0-b572-48c29fe7721f" />

ภาพที่ 1

แก้ไขตามภาพเลย จากนั้นเราจะกด Save as หลังจากกดแล้ว เราได้เปลี่ยนชื่อไฟล์เป็น fff.jpg

# Step 3 eog

เราจะทำการดาวน์โหลดและย้ายไฟล์มายังโฟลเดอร์ที่เราใช้

```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ mv ~/Downloads/fff.jpg /home/kali/Downloads/isusgrace03
```

มาดูตรง Hexdump กันอีกรอบ 

```
┌──(kali㉿kali)-[~/Downloads/isusgrace03]
└─$ head -c 20 fff.jpg | xxd
00000000: ffd8 ffe0 0010 4a46 4946 0001 0100 0001  ......JFIF......
00000010: 0001 0000                                ....
```

โอเค ตอนนี้ทุกอย่างปกติแล้ว ท้ายไฟล์ก็ปิดด้วย FF D9

มาเปิดภาพดูกัน คำตอบจะอยู่ในนั้น

<img width="800" height="500" alt="fff" src="https://github.com/user-attachments/assets/d3a2ffac-f6dc-40c9-bf04-3667948c02c0" />

จริง ๆ ไม่ต้องย้ายไฟล์และดู Hexdump ก็ได้ แก้เสร็จก็เปิดไฟล์ดูได้เลย

# เพิ่มเติม

- FF D8 FF E0: เป็นไฟล์ JPEG ที่ใช้มาตรฐาน JFIF (JPEG File Interchange Format) ซึ่งมักพบในรูปภาพทั่วไปที่เซฟมาจากอินเทอร์เน็ต รูปภาพที่ถูกบีบอัด หรือรูปที่บันทึกจากโปรแกรมแต่งภาพ

ตัวอย่าง

<img width="1920" height="973" alt="image" src="https://github.com/user-attachments/assets/149b4a57-3fb6-4c01-95b7-22d165ee6fae" />

<img width="1920" height="692" alt="image" src="https://github.com/user-attachments/assets/c9d299fc-42d7-4b4e-9cf4-efff2ee64a4c" />

- FF D8 FF E1: เป็นไฟล์ JPEG ที่มีข้อมูล Exif (Exchangeable Image File Format) อยู่ภายใน ซึ่งส่วนใหญ่เป็นรูปภาพที่ถ่ายมาจากกล้องถ่ายรูปหรือสมาร์ตโฟน โดยจะเก็บข้อมูลจำพวก วันเวลาที่ถ่าย, รุ่นกล้อง, และพิกัด GPS

ตัวอย่าง

<img width="1920" height="941" alt="image" src="https://github.com/user-attachments/assets/2550c40b-04dc-43e1-99d3-aa922ef8b451" />

<img width="1920" height="949" alt="image" src="https://github.com/user-attachments/assets/7587b59a-7be4-40f4-979d-9a949b3c1ad4" />

<img width="1920" height="975" alt="image" src="https://github.com/user-attachments/assets/6bfeda45-ea19-4b8c-a8fa-8d68df2fa652" />

ในข้อความสีม่วงจะมีข้อมูลส่วนตัวของภาพและอุปกรณ์ที่ใช้ในการถ่าย จึงปิดไว้ ถ้าอยากเห็นภาพมากขึ้น แนะนำว่าให้นำภาพที่ตัวเองถ่ายในอุปกรณ์ใดกได้ เช่น โทรศัพท์ ไปเข้า EXIFTool

```
https://exif.tools/
```

