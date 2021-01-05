---
layout: post
title: C# IdentityOptions
description: Broken Authentication
image: assets/images/IdentityOption/password_logo.jpeg
---

## Broken Authentication
การใช้ [ASP.NET Core Identity](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity?view=aspnetcore-2.2&tabs=visual-studio) ASP.NET Core Identity framework ได้มีการกำหนดค่าเริ่มต้นมาแล้วเป็นอย่างดี โดยใช้ Password hashes ใช้งานร่วมกับ salt 
Identity ใช้ฟังก์ชันการแฮช PBKDF2 สำหรับรหัสผ่านและสร้าง salt สำหรับผู้ใช้แต่ละคน ในบทความนี้เป็นตัวอย่างการใช้ IdentityOptions Class ในการกำหนด Password Policy

## IdentityOptions Class
**Namespace:** Microsoft.AspNetCore.Builder<br/>**Assembly:** Microsoft.AspNetCore.Identity.dll

IdentityOptions Class ใช้สำหรับการ Config ระบบ Identity โดยมี Properties มากมายให้เรียกใช้งานได้ ดังนี้ (บทความนี้เป็นตัวอย่างของการใช้ Password Property)

|Properties|             |
|----------|-------------|
|ClaimsIdentity|Gets or sets the ClaimsIdentityOptions for the identity system.|
|Cookies|Gets or sets the IdentityCookieOptions for the identity system.|
|Lockout|Gets or sets the LockoutOptions for the identity system.|
|OnSecurityStampRefreshingPrincipal|Invoked when the default security stamp validator replaces the user's ClaimsPrincipal in the cookie.|
|**Password**|**Gets or sets the PasswordOptions for the identity system.**|
|SecurityStampValidationInterval|Gets or sets the TimeSpan after which security stamps are re-validated.|
|SignIn|Gets or sets the SignInOptions for the identity system.|
|Tokens|Gets or sets the TokenOptions for the identity system.|
|User|Gets or sets the UserOptions for the identity system.|

## การกำหนด Password Policy โดยใช้ IdentityOptions Class
กำหนด Password Policy สำหรับใช้ในการลงทะเบียนเพื่อเข้าใช้งานระบบ ดังนี้
- ความยาวอย่างน้อย 8 ตัวอักษร
- ต้องมีตัวเลข
- ต้องมีตัวพิมพ์ใหญ่
- ต้องมีอักขระพิเศษ
![]({{site.baseurl}}/assets/images/IdentityOption/1.jpg){:width="1100px" style="float: center"}

ทดสอบการลงทะเบียนเข้าใช้งานระบบ ถ้าเราใส่ Password ไม่ถูกต้องตาม Password Policy จะไม่สามารถลงทะเบียนได้ ดังรูปด้านล่าง<br/>
![]({{site.baseurl}}/assets/images/IdentityOption/2.jpg){:width="1100px" style="float: center"}

---
Reference:
- [IdentityOptions Class](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.identityoptions?view=aspnetcore-1.1)
- [Configure ASP.NET Core Identity](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity-configuration?view=aspnetcore-5.0)
- [Introduction to Identity on ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity?view=aspnetcore-2.2&tabs=visual-studio)
- [OWASP:A2 Broken Authentication](https://cheatsheetseries.owasp.org/cheatsheets/DotNet_Security_Cheat_Sheet.html)