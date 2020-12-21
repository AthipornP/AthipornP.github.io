---
layout: post
title: Cookie-based Session Management
description: Requirement from OWASP
image: assets/images/CookieSession/OWASP.png
---

# V3.4 Cookie-based Session Management
---
## Cookies
การแลกเปลี่ยน Session ID โดยใช้ Cookies  มีคุณลักษณะด้านความปลอดภัยหลายอย่างในรูปแบบของ
แอตทริบิวต์ ที่สามารถใช้เพื่อป้องกันการแลกเปลี่ยน Session ID ได้

#### 3.4.1 Verify that cookie-based session tokens have the 'Secure' attribute set.
***Secure Flag*** เมื่อมีการระบุแอตทริบิวต์นี้ จะเป็นการกำหนดว่า Cookie จะต้องส่งผ่านทางโปรโตคอล https (TLS/SSL) เท่านั้น โดยกระบวนการนี้จะเป็นวิธีการปกป้อง Session ID จากการถูกโจมตีด้วย Man-in-the-Middle เนื่องจากข้อมูลที่ส่งได้ทำการเข้ารหัสแล้ว

#### 3.4.2 Verify that cookie-based session tokens have the 'HttpOnly' attribute set.
***HttpOnly Flag*** เมื่อมีการระบุแอตทริบิวต์นี้ เว็บเบราเซอร์จะไม่อนุญาตให้ JavaScript เข้าถึงข้อมูล web cookie ของผู้ใช้งานได้  ดังนั้น document.cookie จะไม่สามารถเรียกใช้งานได้  ช่วยลดปัญหาช่องโหว่ประเภท XSS ได้

#### 3.4.3 Verify that cookie-based session tokens utilize the 'SameSite' attribute to limit exposure to cross-site request forgery attacks.
***SameSite Flag*** เป็นแอตทริบิวต์สำหรับกำหนดเพื่อป้องกันการโจมตีในรูปแบบของ Cross-Site Request Forgery (CSRF) ด้วยการป้องกันต้นทางของ Cookie ที่จะส่งมายัง Server

การกำหนด SameSite มี 3 รูปแบบ
- **Lax** คือการอนุญาตให้ส่ง Cookie ต้นทางจาก Website อื่นได้ ผ่าน HTTP GET บน Address bar เท่านั้น (การกด Link)
- **Strict** Cookie จะต้องถูกส่งมาจากต้นทางจาก Website เดียวกันเท่านั้น
- **None** คือการอนุญาต Cookie ต้นทางจากทั้งหมด แต่จะต้องใช้งานร่วมกับการกำหนด Secure Flag ด้วย (ส่งผ่าน https เท่านั้น)

#### 3.4.4 Verify that cookie-based session tokens use "__Host-" prefix to provide session cookie confidentiality.
***__Host-*** prefix เป็นการกำหนดเพื่อระบุว่าผู้ที่สามารถเข้าถึงและแก้ไข Cookie ได้จะต้องเป็น Domain เดียวกัน (Subdomain ไม่สามารถเข้าถึงหรือแก้ไขได้)

#### 3.4.5 Verify that if the application is published under a domain name with other applications that set or use session cookies that might override or disclose the session cookies, set the path attribute in cookie-based session tokens using the most precise path posible.
การตรวจสอบแอปพลิเคชั่นว่าอยู่ภายใต้โดเมนเดียวกันหรือไม่ เพื่อป้องกันการถูกเขียนทับของ Cookie หรือการเข้าถึง Cookie โดยไม่ได้รับอนุญาต

การกำหนด ***Domain*** แอตทริบิวต์ เป็นการระบุ hosts ที่อนุญาตให้รับ Cookie ได้ หากไม่ได้ระบุ ค่า default จะเป็น origin เดียวกันแต่ไม่รวม Subdomain  แต่ถ้ามีการระบุ Domain ไว้ Subdomain จะถูกรวมอยู่ในนั้นด้วย

> ตัวอย่าง :
ถ้ากำหนด ***Domain=mut.com*** ไว้ Cookie จะสามารถใช้งานภายใต้โดเมน mut.com รวมถึง ซับโดเมนด้วย เช่น miss.mut.com

การกำหนด ***Path*** แอตทริบิวต์ จะเป็นการอนุญาตให้กำหนดหรือใช้งาน Cookie ภายใต้ Path ที่กำหนดได้

> ตัวอย่าง :
ถ้ากำหนด ***Path=/docs*** เส้นทางที่ Match กับ /docs จะสามารถใช้งาน Cookie ได้ เช่น
>- /docs 
>- /docs/web
>- /docs/web/https

#### Reference
- [Using HTTP cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
- [SameSite cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite)
- [R029. Cookies with security attributes](https://fluidattacks.com/products/rules/list/029/)