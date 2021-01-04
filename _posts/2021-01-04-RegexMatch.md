---
layout: post
title: C# Regex Match
description: การใช้ Regex ในการค้นหา input string ที่ต้องการ
image: assets/images/RegexMatch/regex.png
---

##  Regular Expressions คืออะไร?
**Regular Expressions** หรือเรียกย่อๆ ว่า ***regex*** ใช้ในการกำหนดรูปแบบหรือกลุ่มคำ เพื่อใช้ในการค้นหาในข้อความต่างๆ ตามที่เราต้องการ <br/>regex สามารถใช้ในการค้นหาในรูปแบบของข้อความธรรมดา ตัวเลข หรืออักษระพิเศษ โดยเราสามารถกำหนดได้ว่าจะให้ match แค่ 1 อัน หรือ match ได้หลายๆ อัน หรือไม่ match เลยก็ได้ การนำไปประยุกต์ใช้งาน เช่น การตรวจสอบ input ว่าเป็นข้อมูลที่เราต้องการหรือไม่<br/>regex มีให้ใช้งานในเกือบทุกภาษา แต่ในบทความนี้ขอเสนอการใช้งาน regex match ในรูปแบบของภาษา C# 

## Regex.Match Method
**Namespace:** System.Text.RegularExpressions<br/>**Assembly:** System.Text.RegularExpressions.dll

Regex.Match เป็น method overloads มีให้เลือกใช้งานหลายรูปแบบ ดังตารางด้านล่าง ([รายละเอียดเพิ่มเติม](https://docs.microsoft.com/en-us/dotnet/api/system.text.regularexpressions.regex.match?view=net-5.0))<br/>ในบทความนี้จะเป็นตัวอย่างการใช้งาน **Regex.Match(String)**

|Overloads|    |
|---------|----|
|Match(String, String, RegexOptions, TimeSpan)|Searches the input string for the first occurrence of the specified regular expression, using the specified matching options and time-out interval.|
|Match(String, Int32, Int32)|Searches the input string for the first occurrence of a regular expression, beginning at the specified starting position and searching only the specified number of characters.|
|Match(String, String, RegexOptions)|Searches the input string for the first occurrence of the specified regular expression, using the specified matching options.|
|Match(String, Int32)|Searches the input string for the first occurrence of a regular expression, beginning at the specified starting position in the string.|
|**Match(String)**|**Searches the specified input string for the first occurrence of the regular expression specified in the Regex constructor.**|
|Match(String, String)|Searches the specified input string for the first occurrence of the specified regular expression.|

## Match(String)
ใช้ในการค้นหาคำหรือประโยคที่ต้องการจาก regex โดย method นี้จะ return match อันแรกที่พบใน input string

~~~
using System;
using System.Text.RegularExpressions;

namespace Code4Sec.RegexMatchSample
{
    class Program
    {
        static void Main(string[] args)
        {
            string text = "Hello! One Code4Sec Two Code4Sec Three Code4Sec";
            string pattern = @"(\w+)\s+(Code4Sec)";

            // Instantiate the regular expression object.
            Regex r = new Regex(pattern, RegexOptions.IgnoreCase);

            // Match the regular expression pattern against a text string.
            Match m = r.Match(text);
            int matchCount = 0;
            while (m.Success)
            {
                Console.WriteLine("Match" + (++matchCount));
                for (int i = 1; i <= 2; i++)
                {
                    Group g = m.Groups[i];
                    Console.WriteLine("Group" + i + "='" + g + "'");
                    CaptureCollection cc = g.Captures;
                    for (int j = 0; j < cc.Count; j++)
                    {
                        Capture c = cc[j];
                        System.Console.WriteLine("Capture" + j + "='" + c + "', Position=" + c.Index);
                    }
                }
                m = m.NextMatch();
            }
        }
    }
}
~~~

จากตัวอย่างด้านบน ได้ระบุ regular expression pattern **(\w+)\s+(Code4Sec)** มีความหมายดังนี้

|Pattern|Description|
|-------|-----------|
| (\w+)|ขึ้นต้นด้วยคำอะไรก็ได้|
|\s+|มีช่องว่างระหว่างคำ|
|(Code4Sec)|ต้องเป็นคำว่า \"Code4Sec\" ในตัวอย่างได้ระบุ RegexOptions.IgnoreCase เพื่อเป็นการบอกว่าเป็นอักษรพิมพ์เล็กหรือพิมพ์ใหญ่ก็ได้|

เมื่อ Run คำสั่งแล้วจะได้ผลลัพธ์ดังภาพ
![]({{site.baseurl}}/assets/images/RegexMatch/1.png){:width="1100px" style="float: center"}

ผลลัพธ์ที่ได้จาก Match method จะ return เป็น substring แรกที่พบในประโยค<br/>
ในตัวอย่างประโยคแรกที่ match คือ \"One Code4Sec\"  ในตัวอย่างมีการใช้ลูป while และคำสั่ง m.NextMatch() เพื่อให้หาคำที่ match ในลำดับถัดไป

---
Reference:

- [Regular Expressions คืออะไร ?](https://medium.com/@_trw/regular-expressions-%E0%B8%84%E0%B8%B7%E0%B8%AD%E0%B8%AD%E0%B8%B0%E0%B9%84%E0%B8%A3-2fab4a91ea34)
- [C# Regex Examples
](https://www.c-sharpcorner.com/article/c-sharp-regex-examples/)
- [Regex.Match Method](https://docs.microsoft.com/en-us/dotnet/api/system.text.regularexpressions.regex.match?view=net-5.0)