---
layout: post
title: C# AuthorizeAttribute
description: Authorization in ASP.NET Core
image: assets/images/AuthorizeAttribute/authorization.jpg
---

## Authorization in ASP.NET Core
ปกติ Application ส่วนใหญ่จะมีการจำกัดสิทธิ์ในการเข้าถึงหรือการเข้าใช้งาน ว่าผู้ใช้ระดับใดที่เข้าใช้งานระบบหรือฟังก์ชันนั้นได้บ้าง โดยเราสามารถกำหนดได้ที่ Class หรือ Method ได้เลย ซึ่งใน ASP.NET ได้มีการ Provide Class ให้เราได้เรียกใช้งานได้อย่างง่ายดาย เป็น Class ที่ชื่อว่า **\"AuthorizeAttribute\"** และ Class นี้มีความพิเศษตรงที่เป็น Attribute class ทำให้เราสามารถนำไป Applies กับ Class หรือ Method ของเราได้

## AuthorizeAttribute Class
**Namespace:** Microsoft.AspNetCore.Authorization<br/>**Assembly:** Microsoft.AspNetCore.Authorization.dll

|Properties|          |
|----------|----------|
|AuthenticationSchemes|Gets or sets a comma delimited list of schemes from which user information is constructed.|
|Policy|Gets or sets the policy name that determines access to the resource.|
|Roles|Gets or sets a comma delimited list of roles that are allowed to access the resource.|

## ตัวอย่างการใช้งาน AuthorizeAttribute
ในตัวอย่างมี 2 Method คือ Index และ Privacy ทำหน้าที่เป็น Controller เมื่อทดสอบรันโปรแกรม เราสามารถเข้าใช้งานได้ทั้ง 2 Method ดังรูป<br/>
![]({{site.baseurl}}/assets/images/AuthorizeAttribute/1.png){:width="1100px" style="float: center"}

ลองเข้าใช้งานหน้า Privacy จะสามารถเข้าใช้งานได้ปกติ<br/>
![]({{site.baseurl}}/assets/images/AuthorizeAttribute/2.png){:width="1100px" style="float: center"}

จากนั้น ทดสอบโดยการนำ **[Authorize]** ใส่ไว้เหนือ Method Privacy<br/>
![]({{site.baseurl}}/assets/images/AuthorizeAttribute/3.png){:width="1100px" style="float: center"}

ทดสอบเข้าหน้า Privacy อีกครั้ง จะพบว่าไม่สามารถเข้าใช้งานได้ เนื่องจากไม่มีสิทธิ์ ซึ่งการระบุ [Authorize] ผู้ใช้งานระบบจะต้องมีการทำ Authentication มาก่อนระบบจึงจะรู้ว่าเป็นใคร มีสิทธิ์เป็นอะไร จาก Error code จะเห็นว่ามีการเกิด Exception No authenticationScheme was specified ซึ่งเกี่ยวกับการ Authentication นั่นเอง<br/>
![]({{site.baseurl}}/assets/images/AuthorizeAttribute/4.png){:width="1100px" style="float: center"}

---
Reference:
- [AuthorizeAttribute Class](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute?view=aspnetcore-5.0)
- [Simple authorization in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authorization/simple?view=aspnetcore-5.0)
- [Authentication and Authorization in ASP.NET Web API](https://docs.microsoft.com/en-us/aspnet/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api)
- [Role-based authorization in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authorization/roles?view=aspnetcore-5.0)