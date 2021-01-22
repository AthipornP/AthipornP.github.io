---
layout: post
title: Improve Network Performance
description: 
image: assets/images/MaxUserPort/netstat.png
---

## Improve Network Performance
สำหรับสาย Dev ที่มีการพัฒนา Web application ใช้งาน Internet Information Services (IIS) เป็น Web Server ในระบบปฏิบัติการ Windows 8 และ Windows 2012 นะครับ  
ตอนรันทดสอบในเครื่องทดสอบหรือเครื่องตัวเองก็อาจจะไม่พบปัญหา แต่เมื่อ Publish ขึ้น Production อาจะเจอ Error ***SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted*** และตามด้วย IP:Port ที่เราเรียกใช้งาน
<br>
![]({{site.baseurl}}/assets/images/MaxUserPort/Screenshot 2021-01-22 142920.jpg){:width="1100px" style="float: center"}

กรณีนี้อาจเกิดจาก Port ฝั่ง Outbound บนเครื่อง Server เต็มเมื่อมีการ Request จาก Client เป็นจำนวนมาก<br>สามารถดู Dynamic port ได้โดยใช้ Command
>netsh int ipv4 show dynamicport tcp

![]({{site.baseurl}}/assets/images/MaxUserPort/Screenshot 2021-01-22 142920.png){:width="1100px" style="float: center"}

ส่วนมากจะเป็นกับ Windows 8 และ Windows Server 2012 ซึ่งมีค่า Default ดังนี้
- MaxUserPort = 1024 - 5000
- TcpTimedWaitDelay = 4 นาที

#### MaxUserPort
เป็นค่าที่ใช้ในการระบุจำนวน port สูงสุดที่มีการ Request จาก Application และเชื่อมต่อเข้ามายังฝั่ง Server โดยปกติจะมีค่าอยู่ระหว่าง 1024 ถึง 5000
สามารถเปลี่ยนค่าได้ ดังนี้
1. เปิด **command prompt** แล้วรันคำสั่ง **regedit**
2. ไปที่ **HKEY_LOCAL_MACHINE\SYSTEM\ CurrentControlSet\Services\TCPIP\Parameters**
3. สร้างคีย์เป็น **REG_DWORD** และตั้งชื่อว่า **MaxUserPort**
4. ระบุค่าเป็น **Decimal 32768** (สูงสุดที่ 65534)

#### TcpTimedWaitDelay
เป็นค่าที่ใช้ในการระบุระยะเวลาในการ Release หรือ Terminate port เมื่อไม่มีการใช้งานแล้ว โดยปกติค่านี้จะอยู่ที่ 4 นาที
สามารถเปลี่ยนค่าได้ ดังนี้
1. เปิด **command prompt** แล้วรันคำสั่ง **regedit**
2. ไปที่ **HKEY_LOCAL_MACHINE\SYSTEM\ CurrentControlSet\Services\TCPIP\Parameters**
3. สร้างคีย์เป็น **REG_DWORD** และตั้งชื่อว่า **TcpTimedWaitDelay**
4. ระบุค่าเป็น **Decimal 30** (มีหน่วยเป็นวินาที)


---
Reference:
- [Settings that can be Modified to Improve Network Performance](https://docs.microsoft.com/en-us/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)
- [Configuring MaxUserPort  (Maximum user ports)](https://www.ibm.com/support/knowledgecenter/SSRTHY_8.5.0/com.ibm.installingirm.doc/rminst0230.htm)