---
layout: post
title: C# Assembly Load
description: Load file with strong name assemblies
image: assets/images/IdentityOption/password_logo.jpeg
---

## Assembly
โปรแกรมในภาษา C# อาจประกอบด้วย source code หนึ่งไฟล์หรือหลายๆ ไฟล์ก็ได้ คลาสหนึ่งคลาสอาจถูกนิยามไว้ภายในไฟล์เดียว (ปรกติจะมีนามสกุล .cs) หรือหลายๆ ไฟล์ก็ได้ 
<br/>
![]({{site.baseurl}}/assets/images/AssemblyLoadFile/1.png){:width="1100px" style="float: center"}

เมื่อผ่านการคอมไพล์โปรแกรมให้เป็นโปรแกรมประยุกต์ จะได้ไฟล์นามสกุล .exe หากคอมไพล์โปรแกรมให้เป็นไลบรารี (คือโปรแกรมที่ไม่มี method main()) จะได้ไฟล์นามสกุล .dll แม้ไฟล์ทั้งสองแบบนี้ จะมีนามสกุลเหมือนโปรแกรมแบบ Win32 แต่โครงสร้างภายในกลับไม่เหมือนกันเลย โดยไฟล์ assembly จะบรรจุโค้ดที่คอมไพล์แล้ว (เป็นภาษา MSIL ที่อยู่ในสภาพไบนารี) และข้อมูลแบบ metadata ให้โปรแกรมอื่นสามารถนำไป Reference เพื่อเรียกใช้งาน Class หรือ Method ภายในไฟล์ .dll ได้โดยไม่ต้องเขียนเองใหม่ทั้งหมด

Assemble ที่ผ่านการ Sign แล้ว จะเกิดเป็น Strong name<br/>Strong name ประกอบด้วย 
- **Assembly name** คือชื่อของ dll file
- **Version Number** คือ เวอร์ชั่นของ dll
- **Culture information** คือ Culture เราสามารถกำหนดเองได้ แต่ถ้าไม่ได้กำหนด ค่า default จะเป็น neutral
- **Public key token** จะเกิดจากการเอา 3 ค่าแรก ผ่านกระบวนการ Sign แล้วจะเกิดเป็น Public key token

ในการ Load file assemblies มาใช้งานนั้น เราจะโหลดผ่าน Method ที่ชื่อว่า **\"Assembly.Load(String)\"** วิธีนี้จะช่วยป้องกันการเรียกใช้งาน Assembly ที่ไม่ถูกต้อง เนื่องจากเราต้องระบุเป็น Strong name ของ Assembly นั้น และยังช่วยเรื่องผู้ไม่หวังดีนำไฟล์ .dll ไปแก้ไขแล้วให้เราเรียกใช้ โปรแกรมจะไม่สามารถทำงานได้ เนื่องจากไฟล์ .dll ที่ถูกแก้ไขและมีการ Sign ใหม่แล้ว จะมีค่า Strong name ที่เปลี่ยนไป

![]({{site.baseurl}}/assets/images/AssemblyLoadFile/2.png){:width="1100px" style="float: center"}

## Assembly.Load Method
**Namespace:** System.Reflection<br/>**Assembly:** System.Runtime.dll

## ตัวอย่างการใช้งาน Assembly.Load Method
ผมจะลอง list assemblies ที่มีอยู่ในเครื่องขึ้นมาทั้งหมด โดยใช้ Tools Developer Command Prompt แล้วใช้คำสั่ง gacutil –l<br/>
![]({{site.baseurl}}/assets/images/AssemblyLoadFile/3.png){:width="1100px" style="float: center"}

ทดสอบโหลด \"System.Text.Encoding, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL\" เข้ามาใช้งานใน Project ของเรา
~~~
var assembly = Assembly.Load("System.Text.Encoding, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a");
~~~

<br/>
![]({{site.baseurl}}/assets/images/AssemblyLoadFile/4.png){:width="1100px" style="float: center"}

---
Reference:
- 