Hi, Can you speak Thai ? 

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ Riddle Registry หมวด Forensics

# Step 1 สร้าง Directory และนำเข้าไฟล์

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
└─$ wget https://challenge-files.picoctf.net/c_amiable_citadel/929daf6ef01bba32b165e0a7c649ff4c953f2af21c28b024e8af5276b7716de5/logs.txt
--2026-03-17 03:02:09--  https://challenge-files.picoctf.net/c_amiable_citadel/929daf6ef01bba32b165e0a7c649ff4c953f2af21c28b024e8af5276b7716de5/logs.txt
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 18.239.134.85, 18.239.134.106, 18.239.134.126, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|18.239.134.85|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1592256 (1.5M) [application/octet-stream]
Saving to: ‘logs.txt’

logs.txt                    100%[==========================================>]   1.52M  1.03MB/s    in 1.5s    

2026-03-17 03:02:12 (1.03 MB/s) - ‘logs.txt’ saved [1592256/1592256]
```

# Step 2

คำสั่ง cat ใช้สำหรับอ่านเนื้อหาไฟล์, แสดงผลไฟล์บนหน้าจอ terminal, รวมไฟล์หลายไฟล์เข้าด้วยกัน, และสร้างไฟล์ใหม่ ในข้อนี้เราจะใช้ตรวจสอบเนื้อหาไฟล์
```
┌──(kali㉿kali)-[~/isusgrace02]
└─$ cat logs.txt | base64 --decode > picture.png
```
คำสั่ง ls ใช้แสดงรายการไฟล์และไดเร็กทอรีที่มีอยู่ในไดเร็กทอรีปัจจุบัน
```                                                                                                               
┌──(kali㉿kali)-[~/isusgrace02]
└─$ ls
logs.txt  picture.png
```
eog เราจะใช้เปิดดูรูปภาพ
```                                                                                                               
┌──(kali㉿kali)-[~/isusgrace02]
└─$ eog picture.png
```

<img width="896" height="1152" alt="picture" src="https://github.com/user-attachments/assets/3d02395e-eabf-4924-bb57-668b286f01ed" />

ภาพที่ 1

เอาเลข hex ที่อยู่ในภาพมาเข้า Cyberchef 

<img width="1920" height="915" alt="image" src="https://github.com/user-attachments/assets/cb52ddc1-079c-498c-8df8-b6adc9825cce" />

หรือใช้คำสั่ง echo บน kali linux ก็ได้
```
echo "7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F65633139383466637D" | xxd -r -p
```
จะได้
```
┌──(kali㉿kali)-[~/isusgrace02]
└─$ echo "7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F65633139383466637D" | xxd -r -p
picoCTF{XXXXX}
```
XXXXX ไม่ใช่ flag นะ คือปิดไว้ จะได้ทำเอง


## เพิ่มเติม
- ที่รู้ว่าข้อนี้ต้องแปลงเป็น PNG เพราะฉันได้เอาเนื้อหาในไฟล์ TXT ไปถอดรหัสด้วย Base64 ใน Cyberchef
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b83d4655-f9d8-401c-b8bf-f86c90224092" />

- คำสั่ง cat ใช้สำหรับแสดงและอ่านเนื้อหาไฟล์บนหน้าจอ Terminal, รวมไฟล์หลายไฟล์เข้าด้วยกัน, และสร้างไฟล์ใหม่

แสดงเนื้อหาไฟล์: ดูเนื้อหาทั้งหมดภายในไฟล์ข้อความ เช่น cat isusgrace.txt

รวมไฟล์: นำเนื้อหาจากหลายไฟล์มารวมกันแล้วสร้างไฟล์ใหม่ เช่น cat isusgrace01.txt isusgrace02.txt > isusgracemix.txt

สร้างไฟล์ใหม่: cat > isusgrace.txt จากนั้นพิมพ์เนื้อหาลงในไฟล์ใหม่ แล้ว กด Ctrl+D เพื่อบันทึกและจบการทำงาน
