---
layout: post
title: C# Protected Memory
description: How to - Use Data Protection
image: assets/images/AssemblyLoadFile/dll-logo.png
---

## Data Protection
ใน .NET มีการ Provides data protection API (DPAPI) ซึ่งอนุญาตให้เราเข้ารหัสข้อมูลได้โดยใช้ข้อมูล Current user account หรือ Computer 

การใช้ ProtectedData Class ในการเข้ารหัสข้อมูล สามารถใช้งานได้ใน .NET Framework, .NET Core และ .NET 5 โดยเราสามารถกำหนดให้เข้ารหัสและถอดรหัสเฉพาะผู้ใช้ได้ หรือกำหนดให้เข้ารหัสด้วยบัญชีผู้ใช้คนหนึ่งแต่ทุกบัญชีในคอมพิวเตอร์เครื่องนั้นสามารถถอดรหัสได้

## การเข้ารหัส File หรือ Stream โดยใช้ Data Protection
1. Create random entropy
2. 