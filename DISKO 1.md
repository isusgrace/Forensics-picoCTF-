Hi, Can you speak Thai ?

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ DISKO 1 หมวด Forensics 

# Step 1 สร้าง Directory และนำเข้าไฟล์

ใช้คำสั่ง mkdir ใช้สำหรับสร้างไดเรกทอรีหรือโฟลเดอร์ใหม่บนระบบไฟล์
```
mkdir <new directory>
```
ตามด้วย คำสั่ง cd ใช้สำหรับเปลี่ยนไดเรกทอรีหรือโฟลเดอร์ปัจจุบันในเทอร์มินัล
```
cd <new directory>
```
ตามด้วย คำสั่ง wget ใช้สำหรับดาวน์โหลดไฟล์จากอินเทอร์เน็ตโดยตรงผ่านบรรทัดคำสั่ง
```
┌──(kali㉿kali)-[~/Downloads]
└─$ mkdir isusgrace02                                                  
                                                                                                               
┌──(kali㉿kali)-[~/Downloads]
└─$ cd isusgrace02
                                                                                                               
┌──(kali㉿kali)-[~/Downloads/isusgrace02]
└─$ wget https://artifacts.picoctf.net/c/536/disko-1.dd.gz
--2026-03-26 02:02:24--  https://artifacts.picoctf.net/c/536/disko-1.dd.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 54.230.41.34, 54.230.41.22, 54.230.41.96, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|54.230.41.34|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 20484476 (20M) [application/octet-stream]
Saving to: ‘disko-1.dd.gz’

disko-1.dd.gz               100%[==========================================>]  19.54M  7.50MB/s    in 2.6s    

2026-03-26 02:02:28 (7.50 MB/s) - ‘disko-1.dd.gz’ saved [20484476/20484476]
```

# Step 2 gunzip and file

คำสั่ง gunzip เราจะใช้สำหรับคลายบีบอัดไฟล์ที่ถูกบีบอัดด้วยโปรแกรม gzip ให้กลับมาเป็นไฟล์ต้นฉบับ
```
┌──(kali㉿kali)-[~/Downloads/isusgrace02]
└─$ gunzip disko-1.dd.gz
```

คำสั่ง file เราจะใช้สำหรับตรวจสอบและระบุประเภทของไฟล์ โดยวิเคราะห์เนื้อหาภายในไฟล์นั้นๆ ไม่ใช่แค่ดูจากนามสกุล
```                                                                                                               
┌──(kali㉿kali)-[~/Downloads/isusgrace02]
└─$ file disko-1.dd       
disko-1.dd: DOS/MBR boot sector, code offset 0x58+2, OEM-ID "mkfs.fat", Media descriptor 0xf8, sectors/track 32, heads 8, sectors 102400 (volumes > 32 MB), FAT (32 bit), sectors/FAT 788, serial number 0x241a4420, unlabeled
```

# Step 3 strings

คำสั่ง strings เราจะใช้สำหรับค้นหาและแสดงข้อความที่พิมพ์ได้จากในไฟล์ โดยจะแสดงลำดับอักขระที่พิมพ์ได้ 4 ตัวขึ้นไป

คำสั่ง grep ใช้สำหรับค้นหาและกรองข้อความภายในไฟล์หรือผลลัพธ์จากคำสั่งอื่น โดยจะแสดงบรรทัดที่มีข้อความที่ตรงกับรูปแบบที่เรากำหนด
```
┌──(kali㉿kali)-[~/Downloads/isusgrace02]
└─$ strings disko-1.dd | grep "picoCTF"
picoCTF{XXXXX}
```
XXXXX ไม่ใช่ flag นะ คือปิดไว้ จะได้ทำเอง
