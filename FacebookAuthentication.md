# Two-Factor Authentication บน Facebook
---
ในปัจจุบันเกิดความไม่ปลอดภัยจากการเข้าสู่ระบบโดยไม่ได้รับอนุญาต ทำให้เกิดความเสียหายเป็นอย่างมาก ยิ่งถ้าเป็น Page ของลูกค้าที่เราดูแล ยิ่งส่งผลกระทบหนัก สาเหตุส่วนใหญ่เกิดจากการโดน Phishing หรือการที่มีผู้ไม่ประสงค์ดี สร้างเว็บปลอมขึ้นมา เพื่อหลอกให้เรากรอกข้อมูลลงไป

การตั้งค่าแบบ ***Two-Factor Authentication*** ก็จะช่วยให้บัญชีของเรามีความปลอดภัยมากยิ่งขึ้น

***Two-Factor Authentication*** คือ การยืนยันตัวตนเพื่อเข้าสู่ระบบด้วย 2 ขั้นตอน โดยปกติแล้วตอนที่เรา Login เข้าระบบ ทุกคนก็จะกรอก username และ password เพื่อยืนยันตัวตน แต่การ Login ลักษณะนี้ จะมีความปลอดภัยค่อนข้างน้อย  
การยืนยันตัวตนชั้นที่ 2 นอกจากการใส่ password ก็มีหลายวิธี ขึ้นอยู่กับระบบที่เราใช้งาน เช่น การส่ง OTP ผ่าน SMS, การใช้ลายนิ้วมือ เป็นต้น

#### การเปิดใช้งาน Two-Factor Authentication บน Facebook มีขั้นตอนดังนี้

1. ไปที่ **ตั้งค่า** จากนั้นเลือก **การรักษาความปลอดภัยและการเข้าสู่ระบบ** และเลือกหัวข้อ **ใช้การยืนยันตัวตนแบบสองชั้น**
![](/FacebookAuthentication_Images/step1.png "Step 1"){:height="1100px" width="619px" style="float: right"} 

2. เลือกว่าต้องการ การยืนยันตัวตนแบบสองชั้นแบบใด  ในที่นี้ เลือกแบบ **แอพยืนยันตัวตน** จากนั้นทำการ สแกน QR CODE เพื่อเข้าสู่การ Authentication
![](/FacebookAuthentication_Images/step2.png "Step 2"){:height="1100px" width="619px" style="float: right"} 

3. เมื่อสแกน QR Code แล้ว ก็นำรหัสที่ได้ ไปกรอกในขั้นตอนต่อไป
![](/FacebookAuthentication_Images/step3.png "Step 3"){:height="1100px" width="619px" style="float: right"} 

4. เปิดการใช้งาน การยืนยันตัวตนแบบสองชั้น เรียบร้อย
![](/FacebookAuthentication_Images/step4.png "Step 4"){:height="1100px" width="619px" style="float: right"} 