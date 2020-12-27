---
layout: post
title: PHP Code Injection
description: bWAPP Tutorials
image: assets/images/PHPCodeInjection/bwapp.jpg
---

# bWAPP Tutorials - PHP Code Injection

**PHP Code Injection** เป็นช่องโหว่ที่อนุญาตให้ Client ส่ง Code หรือคำสั่ง PHP ในรูปของ Query string ได้

---

#### RIPS Scan
ทดสอบนำไฟล์ **phpi.php** ไป scan หาข่องโหว่โดยใช้เครื่องมือ **RIPS** ผลลัพธ์จากการ scan จะพบว่ามีช่องโหว่ในเรื่องของ **Code Execution** ในบรรทัดที่ 90 ของไฟล์
![]({{site.baseurl}}/assets/images/PHPCodeInjection/1-1.png){:width="1100px" style="float: center"}

#### วิธีการทดสอบช่องโหว่ PHP Code Injection ใน bWAPP
(จากตัวอย่าง ip ที่ใช้ในการทดสอบจะเป็น 192.168.126.129 เนื่องจากทำการทดสอบใน VMware)

1. เข้าไปที่ url http://192.168.126.129/bWAPP/phpi.php
![]({{site.baseurl}}/assets/images/PHPCodeInjection/1.png){:width="1100px" style="float: center"}

2. คลิกที่คำว่า **message** ระบบจะแสดงผลคำว่า **test** ออกมาที่บรรทัดล่าง ดังรูปตัวอย่างด้านล่าง
![]({{site.baseurl}}/assets/images/PHPCodeInjection/2.png){:width="1100px" style="float: center"}

3. ทดสอบโดยการ Injection ผ่านทาง Query string จะเห็นว่าสามารถส่งคำสั่ง PHP เข้าไปได้ ในที่นี้ทดสอบด้วยคำสั่ง phpinfo โดยการเพิ่ม **;phpinfo()** ต่อท้าย url 
![]({{site.baseurl}}/assets/images/PHPCodeInjection/4.png){:width="1100px" style="float: center"}

#### วิธีการปิดช่องโหว่ PHP Code Injection
1. จากตัวอย่างไฟล์ phpi.php
![]({{site.baseurl}}/assets/images/PHPCodeInjection/f_1.png){:width="1100px" style="float: center"}

2. ทำการแก้ไขคำสั่งบรรทัดที่ 90 โดยใช้ function **htmlspecialchars()** ของภาษา PHP ในการช่วยแปลงอักขระพิเศษให้ในอยู่ในรูปแบบของ HTML string แล้ว Save เป็นไฟล์ใหม่ชื่อ phpi_fix.php เพื่อทดสอบบน Server
![]({{site.baseurl}}/assets/images/PHPCodeInjection/f_2.png){:width="1100px" style="float: center"}

3. ทดสอบ Scan ไฟล์ phpi_fix.php ด้วย RIPS อีกครั้ง จะพบว่าช่องโหว่ **Code Execution** ได้หายไปแล้ว
![]({{site.baseurl}}/assets/images/PHPCodeInjection/1-2.png){:width="1100px" style="float: center"}

4. ทดสอบ Injection ที่หน้าเว็บ จะพบว่าคำสั่ง PHP ที่ส่งเข้าไปจะถูกแปลงเป็นข้อความธรรมดา
![]({{site.baseurl}}/assets/images/PHPCodeInjection/5.png){:width="1100px" style="float: center"}

---
#### Members
- Athiporn Phumnicom
- Phureephat Sottiratanapan
