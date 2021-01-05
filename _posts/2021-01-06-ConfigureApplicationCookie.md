---
layout: post
title: C# CookieOptions
description: Weak Account management
image: assets/images/CookieOptions/webCookies_normal-1.png
---

## Weak Account management
การเขียนโปรแกรมในรูปแบบ Web Application ต้องมีการเก็บ State ต่างๆ ที่ Client โดยการเก็บลงใน Cookie นั่นเอง

เนื่องจาก Cookie ทำงานอยู่ฝั่ง Client ทำให้สามารถถูกเปลี่ยนแปลงแก้ไขได้ง่ายจากผู้ไม่หวังดี ดังนั้นเราจำเป็นจะต้อง Config cookie ให้มีความปลอดภัยตั้งแต่ฝั่ง Server

ใน .NET Core มี Class ให้เราได้เรียกใช้งานเพื่อ Config cookie เมื่อต้องการ Response ไปให้ Client โดยการ Config ใน Class **\"CookieOptions\"**

## CookieOptions Class
**Namespace:** Microsoft.AspNetCore.Http<br/>**Assembly:** Microsoft.AspNetCore.Http.Features.dll

ภายใน CookieOptions Class ประกอบไปด้วย Properties ให้เราใช้งานได้ ดังนี้

|Properties|       |
|----------|-------|
|Domain|Gets or sets the domain to associate the cookie with.|
|Expires|Gets or sets the expiration date and time for the cookie.|
|HttpOnly|Gets or sets a value that indicates whether a cookie is accessible by client-side script.|
|IsEssential|Indicates if this cookie is essential for the application to function correctly. If true then consent policy checks may be bypassed. The default value is false.|
|MaxAge|Gets or sets the max-age for the cookie.|
|Path|Gets or sets the cookie path.|
|SameSite|Gets or sets the value for the SameSite attribute of the cookie. The default value is Unspecified|
|Secure|Gets or sets a value that indicates whether to transmit the cookie using Secure Sockets Layer (SSL)--that is, over HTTPS only.|


## ตัวอย่างการใช้งาน CookieOptions Class
การใช้งาน เราต้อง New object ของ CookieOptions ขึ้นมาก่อนแล้วจึงกำหนด Properties ที่เราต้องการ
~~~
var cookieOptions = new CookieOptions
{
    // Set the secure flag, which Chrome's changes will require for SameSite none.
    // Note this will also require you to be running on HTTPS
    Secure = true,

    // Set the cookie to HTTP only which is good practice unless you really do need
    // to access it client side in scripts.
    HttpOnly = true,

    // Add the SameSite attribute, this will emit the attribute with a value of none.
    // To not emit the attribute at all set the SameSite property to (SameSiteMode)(-1).
    SameSite = SameSiteMode.None,

    Expires = new DateTimeOffset(DateTime.Now.AddDays(1))
};
~~~

เมื่อต้องมีการส่ง Cookie ไปยัง Client ให้ระบุ Cookie Option ที่เราได้กำหนดไว้ไปด้วย โดยใช้คำสั่ง **Response.Cookies.Append(string key, string value, CookieOptions options);** ดังตัวอย่างด้านล่างนี้
~~~
Response.Cookies.Append("Code4Sec", "Sample_Cookie", cookieOptions);
~~~

ทดลองรันคำสั่ง และตรวจสอบใน Browser (ในตัวอย่างจะใช้ Firefox นะครับ) โดยการกด F12 เพื่อเปิดโหมด Developer จากนั้นเปิด Tab Storage ในหัวข้อ Cookies จะพบว่ามี Cookie key \"Code4Sec\" ที่เราได้สั่ง Response มาจาก Server ซึ่งมี Option Secure เป็น true, HttpOnly เป็น true, SameSite เป็น None และ Expire ในวันถัดไป<br/>
![]({{site.baseurl}}/assets/images/CookieOptions/2.png){:width="1100px" style="float: center"}

---
Reference:
- [CookieOptions Class](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.cookieoptions?view=aspnetcore-5.0)
- [ASP.NET MVC Tutorial Cookies](https://asp.mvc-tutorial.com/httpcontext/cookies/)