---
layout: post
title: C# Regex Match
description: การใช้ Regex ในการค้นหา input string ที่ต้องการ
image: assets/images/RegexMatch/regex.png
---

##Regular Expressions คืออะไร?
**Regular Expressions** หรือเรียกย่อๆ ว่า ***regex*** ใช้ในการกำหนดรูปแบบหรือกลุ่มคำ เพื่อใช้ในการค้นหาในข้อความต่างๆ ตามที่เราต้องการ regex สามารถใช้ในการค้นหาในรูปแบบของข้อความธรรมดา ตัวเลข หรืออักษระพิเศษ โดยเราสามารถกำหนดได้ว่าจะให้ match แค่ 1 อัน หรือ match ได้หลายๆ อัน หรือไม่ match เลยก็ได้ regex มีให้ใช้งานในเกือบทุกภาษา แต่ในบทความนี้ขอเสนอการใช้งาน regex match ในรูปแบบของภาษา C# 

##Regex.Match Method
**Namespace:** System.Text.RegularExpressions
**Assembly:** System.Text.RegularExpressions.dll

---
Reference:

- [Regular Expressions คืออะไร ?](https://medium.com/@_trw/regular-expressions-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3-2fab4a91ea34)
- [C# Regex Examples
](https://www.c-sharpcorner.com/article/c-sharp-regex-examples/)
- [Regex.Match Method](https://docs.microsoft.com/en-us/dotnet/api/system.text.regularexpressions.regex.match?view=net-5.0)