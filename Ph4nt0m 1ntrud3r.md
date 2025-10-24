Hi, Can you speak Thai ?

Yes, I can speak Thai.

มา วันนี้เราจะมาทำข้อ Ph4nt0m 1ntrud3r หมวด Forensics

Step 1 เปิดไฟล์ใน wireshark

ในข้อนี้จะมีไฟล์มาให้ Type of file คือ PCAP File (.pcap) 

เราจะเปิดไฟล์นี้ใน wireshark ไปที่ Open with แล้วเลือก wireshark

Step 2 Time

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/87d482f1-c6ba-4122-b5b5-33f2983d8869" />

ภาพที่ 1

<img width="974" height="566" alt="ไฮไลท์สีเหลือง" src="https://github.com/user-attachments/assets/b1696027-da46-4845-917f-5741c8b75934" />

ภาพที่ 2

ฉันลองดูแต่ละแพ็กเกจ สังเกตที่ Data payload จะมีข้อความที่ดูเหมือนถูกเข้ารหัสด้วย Base64 ดังภาพที่ 2 (ไฮไลท์) แต่ Len ของบางแพ็กเกจไม่เหมือนกัน ฉันจึงคลิกที่ Time ดังภาพที่ 1 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fbf9e5cd-ae88-4852-9729-fd4038538108" />

ภาพที่ 3

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cefd9209-1235-4c0e-888a-854fef3d4a38" />

ภาพที่ 4

สังเกตแพ็กเกจแรกที่มี Len=12 ดังภาพที่ 3 ฉันจำได้ว่ารูปแบบของ flag คือ "cGljb0NURg==" ในกรณีที่ถูกเข้ารหัสด้วย Base64 แสดงว่า flag ถูกแยกชิ้นส่วน และชิ้นส่วนของ flag แต่ละชิ้นส่วนอยู่ในแพ็กเกจที่มี Len=12 ให้เราทำการ copy โดยการคลิกขวา แล้วเลือก "...as ASCII Text" เอาเฉพาะส่วนที่ถูกเข้ารหัสด้วย Base4 ดังภาพที่ 2 คัดลอกมาทุกแพ็กเกจที่มี Len=12 โดยเรียงจากบนลงล่าง และคัดลอก "fQ==" ที่อยู่ในแพ็กเกจสุดท้ายที่มี Len=4 มาด้วย เพราะนั่นคือวงเล็บปีกกาปิด

<img width="1920" height="1080" alt="ชิ้น" src="https://github.com/user-attachments/assets/2c750fa7-5c0d-4723-bc5f-8e997b3e2ea5" />

ภาพที่ 5

นำไปถอดรหัสด้วย Base64 โดยใช้ CyberChef จะได้ flag ดังภาพที่ 5 

ปิด flag ไว้ จะได้ทำเอง
