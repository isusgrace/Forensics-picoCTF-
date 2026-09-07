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

# Step 3
