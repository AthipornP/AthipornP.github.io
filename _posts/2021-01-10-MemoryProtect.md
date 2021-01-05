---
layout: post
title: C# Protected Memory
description: Managing the sensitive information in your code
image: assets/images/MemoryProtect/data-encrypted.jpg
---

## Data Protection
ในการเขียนโปรแกรม สิ่งสำคัญที่สุดคือข้อมูลที่มีการใช้งานภายในโปรแกรม ซึ่งอาจเป็นข้อมูลที่สำคัญมากหรือ Sensitive data<br/>
บางส่วนอาจมีการเก็บใน Disk บางส่วนอาจอยู่ใน Memory แล้วแต่โปรแกรมเมอร์จะออกแบบ<br/>
แต่ในกรณีที่จำเป็นจะต้องเก็บข้อมูลสำคัญลงใน Memory ใน .NET ได้ Provides ProtectedMemory Class ให้เราได้เรียกใช้งานในการปกป้องข้อมูลสำคัญใน Memory<br/>

## ProtectedMemory Class
**Namespace:** System.Security.Cryptography<br/>**Assembly:** System.Security.dll

ใน ProtectedMemory Class ได้ Provides 2 Methods ในการป้องกันและยกเลิกการป้องกันข้อมูลใน Memory

|Methods|             |
|-------|-------------|
|Protect(Byte[], MemoryProtectionScope)|Protects the specified data.|
|Unprotect(Byte[], MemoryProtectionScope)|Unprotects data in memory that was protected using the Protect(Byte[], MemoryProtectionScope) method.|

## ตัวอย่างการใช้งาน ProtectedMemory Class
ในการเรียกใช้งาน Protect Method ข้อมูลที่ต้องการป้องกัน จะต้องเป็น Bytes array ที่มีขนาด 16<br/>
กรณีที่ข้อมูลมีขนาดใหญ่ อาจจะต้องมีการนำ Loop เข้ามาช่วยในการแบ่งข้อมูลเพื่อให้ได้ขนาดตามที่กำหนด

~~~
using System;
using System.Security.Cryptography;
using System.Text;

namespace ProtectedMemorySample
{
    class Program
    {
        static void Main(string[] args)
        {
            var data = "####Code4Sec####";
            Console.WriteLine("Original data: {0}",data);
            // Create the original data to be encrypted (The data length should be a multiple of 16).
            byte[] secret = Encoding.UTF8.GetBytes(data);
            Console.WriteLine("Before Protect: {0}", BitConverter.ToString(secret));          

            // Encrypt the data in memory. The result is stored in the same array as the original data.
            ProtectedMemory.Protect(secret, MemoryProtectionScope.SameLogon);
            Console.WriteLine("Protect: {0}", BitConverter.ToString(secret));

            // Decrypt the data in memory and store in the original array.
            ProtectedMemory.Unprotect(secret, MemoryProtectionScope.SameLogon);
            Console.WriteLine("Unprotect: {0}", BitConverter.ToString(secret));

            Console.ReadLine();
        }
    }
}
~~~

<br/>
![]({{site.baseurl}}/assets/images/MemoryProtect/1.png){:width="1100px" style="float: center"}

## ผลลัพธ์
<br/>
![]({{site.baseurl}}/assets/images/MemoryProtect/2.png){:width="1100px" style="float: center"}

---
Reference:
- [ProtectedMemory Class](https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.protectedmemory?view=netframework-4.8)
- [ProtectedMemory.Protect Method](https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.protectedmemory.protect?view=netframework-4.8)
- [ProtectedMemory.Unprotect Method](https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.protectedmemory.unprotect?view=netframework-4.8)