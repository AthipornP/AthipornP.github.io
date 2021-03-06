---
layout: post
title: Digital Signature Verification
description: 
image: assets/images/DigitalSignatureVerification/DigitalSignature.jpg
---

# Digital Signature Verification
**Digital Signature** คือลายเซ็นที่อยู่ในรูปแบบของอิเล็กทรอนิกส์ ที่มีคุณสมบัติด้านความปลอดภัยเพื่อให้มีความน่าเชื่อถือมากยิ่งขึ้น ประกอบด้วย

1. Signer Authentication เป็นความสามารถในการพิสูจน์ว่าใครเป็นคนเซ็นเอกสาร ตัวลายเซ็นจะสามารถใช้ในการเชื่อมโยงไปยังบุคคลที่เซ็นเอกสารได้
2. Data Integrity เป็นความสามารถในการตรวจสอบ หรือพิสูจน์ได้ว่ามีการแก้ไขเอกสารหลังจากที่ได้มีการเซ็นไปแล้วหรือไม่
3. Non-repudiation การไม่สามารถปฏิเสธความรับผิดชอบได้ เนื่องจากลายเซ็นที่สร้างขึ้นมีเอกลักษณ์ สามารถพิสูจน์ในชั้นศาลได้ว่าใครเป็นผู้เซ็นเอกสาร


#### หลักการทำงานของ Digital Signature
การทำงานของ Digital Signature แบ่งการทำงานเป็น 2 ส่วนด้วยกันคือ ผู้ส่งและผู้รับ
เมื่อผู้ส่งได้เขียนข้อมูลลงในอีเมล์เป็นที่เรียบร้อยแล้ว ระบบจะทำการแปลงไฟล์อีเมล์ที่เป็นไฟล์ Document เพื่อหาค่า Hash Value ด้วย Hash Algorithm 

![]({{site.baseurl}}/assets/../../../assets/images/DigitalSignatureVerification/digital-signature.jpg){:width="1100px" style="float: center"}

หลังจากได้ค่า Hash Value เป็นที่เรียบร้อยแล้วก็นำค่านี้มาใส่กุญแจของผู้ส่งด้วยการเข้ารหัสแบบ Asymmetric ซึ่งหลังเสร็จกระบวนการนี้ก็จะได้เป็นลายเซ็นดิจิตอล (Digital Signature) หลังจากนั้นอีเมล์จะส่งไปยังผู้รับ ซึ่งผู้รับเองจะได้รับอีเมล์แยกออกเป็น 2 ส่วนด้วยกันคือ ส่วนของกุญแจที่ทางผู้ส่งได้ส่งมาให้ด้วยกับไฟล์เอกสาร (Document) ซึ่งกระบวนการแรกระบบจะนำกุญแจที่ส่งมาด้วยทำการถอดรหัสแบบ Asymmetric ให้ได้ค่า Hash Value เสียก่อนหลังจากได้ค่า Hash Value ที่ได้จากกุญแจเป็นที่เรียบร้อยแล้ว ระบบก็จะทำการหาค่า Hash Value จากไฟล์เอกสารที่ส่งมาด้วย ด้วยการหาค่าจาก Hash Algorithm เมื่อได้ค่า Hash Value จากไฟล์เอกสารและกุญแจหรือ Digital Signature แล้วก็นำค่า Hash Value มาเปรียบเทียบกัน ถ้าค่า Hash Value ถูกต้อง เอกสารนั้นก็จะสามารถเปิดอ่านได้ แต่ถ้าไม่ผู้รับก็จะไม่สามารถเปิดดูเอกสารนั้นได้ เนื่องจากอีเมล์ที่ส่งไปอาจจะมีการดัดแปลงแก้ไขเนื้อหาระหว่างทางส่งก็เป็นไปได้

#### ประโยชน์ของ Digital Signature
ซึ่งระบบนี้มีประโยชน์อย่างมากเรื่องความปลอดภัยและช่วยสร้างความมั่นใจให้กับผู้ใช้งานเป็นอย่างมาก โดยเราสามารถแบ่งออกมาเป็นข้อ ๆ ดังนี้

1. เรื่องความปลอดภัยถือว่ามีความปลอดภัยในระดับที่สูง พร้อมกันนั้นยังได้รับการรับรองจากองค์กรกลาง (Certification Authority – CA) ทำการรับรอง Digital Signature อีกด้วย ซึ่งทำให้ผู้ใช้มีความมั่นใจในความถูกต้องและความปลอดภัยอย่างมาก
2. การปลอมแปลง Digital Signature นั้นเป็นเรื่องที่ทำได้ยากเพราะถ้าเอกสารที่ส่งไปแปลงค่า Hash Value ไม่เท่ากันแล้วเอกสารนั้นก็จะเปิดไม่ได้เลย
3. เมื่อใช้ Digital Signature เอกสารก็จะไม่ถูกเปิดอ่านหรือแก้ไขระหว่างทางที่ส่งมาอย่างแน่นอน
4. ระยะทางในการส่งไม่ใช่ปัญหาสำหรับการส่งอีเมล์แบบ Digital Signature อย่างแน่นอนจากประโยชน์ที่กล่าวมาทำให้การส่งอีเมล์และเอกสารแบบ Digital Signature เป็นระบบที่ได้รับความน่าเชื่อถืออย่างมากสำหรับผู้ที่ต้องการความถูกต้องและต้องการความเป็นส่วนตัว

---

#### Reference
- [ลายเซ็นอิเล็กทรอนิกส์ Digital Signature คืออะไร](https://www.bcircle.co.th/2017/09/30/digital-signature/)
- [Digital Signature คืออะไร](https://sites.google.com/site/thanitaphat59/homework/digital-signature-khux-xari)


