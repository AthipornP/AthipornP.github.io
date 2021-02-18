---
layout: post
title: Type safety in Python
description: 
image: assets/images/TypeSafetyInPython/python-logo-master-v3-TM.png
---

## Type safety in Python
ตัวแปรที่ประกาศใน Python เป็น [Dynamically Typed](https://en.wikipedia.org/wiki/Type_system#Dynamic_type_checking_and_runtime_type_information) กล่าวคือ เราสามารถประกาศตัวแปร
โดยไม่ต้องระบุ data type ได้ ตัวแปรจะถูกระบุ type เมื่อเรามีการใส่ค่าให้มัน เช่น

~~~
name = "Athiporn Phumnicom"

print(type(a))
#<class 'str'>
~~~

จากตัวอย่าง ตัวแปร a ที่ได้สร้างไว้ เป็น type str
เพราะเรามีการระบุค่าที่เป็น str ให้กับ name
Python จะไม่รู้ว่าตัวแปรนั้นเป็น type อะไรจนกว่าจะรันคำสั่งบรรทัดนั้น

## เปรียบเทียบกับภาษา Java
ภาษา Java เป็น [Statically Typed](https://en.wikipedia.org/wiki/Type_system#Static_type_checking) กล่าวคือ เมื่อมีการสร้างตัวแปรในภาษา Java เราจะต้องระบุ String type ด้วย

~~~
String name = "Athiporn Phumnicom";
~~~

Java จะรู้ว่า name เป็น String ตั้งแต่การประกาศในตอนแรก เฉพาะฉะนั้นค่าที่เราจะระบุได้ ต้องเป็น type String เท่านั้น สมมุติถ้าเราใส่ค่าที่เป็น Int จะทำให้ compile error

## ทำไมต้องให้ความสำคัญกับ Types
โดยปกติ เราสามารถเขียนโค้ตได้เร็วกว่าถ้าภาษาที่เป็น dynamically-typed อย่าง Python เพราะเราไม่ต้องสนใจ ไม่ต้องคอยกังวลว่าตัวแปรที่ประกาศจะใช้เป็น type อะไร แต่เมื่อโปรแกรมหรือโค้ตที่เราเขียนมีขนาดใหญ่ขึ้น อาจทำให้เป็น bugs ได้ ภาษาที่เป็น static typing จึงเป็นตัวเลือกที่ดีกว่า

## ตัวอย่างโปรแกรม
~~~
def get_first_name(full_name):
    return full_name.split(" ")[0]

fallback_name = {
    "first_name": "UserFirstName",
    "last_name": "UserLastName"
}

raw_name = input("Please enter your name: ")
first_name = get_first_name(raw_name)

# If the user didn't type anything in, use the fallback name
if not first_name:
    first_name = get_first_name(fallback_name)

print(f"Hi, {first_name}!")
~~~

จากตัวอย่างเป็นโปรแกรมง่ายๆ ที่จะให้ User ป้อนชื่อเข้ามาแล้วแสดงผล เช่น **Hi, <first name>!** แต่ถ้า User ไม่พิมพ์อะไรเลย จะให้โปรแกรมแสดงผล **Hi, UserFirstName!** แทน

เมื่อลองรันดูจะเห็นว่าโปรแกรมก็ทำงานได้ปกติ แต่ปัญหาจะเกิดเมื่อ User ใส่ค่า black เข้ามา

~~~
Please enter your name:
Traceback (most recent call last):
  File "c:\Users\BlackDragon\source\repos\TypeSafe\sample3.py", line 14, in <module>
    first_name = get_first_name(fallback_name)
  File "c:\Users\BlackDragon\source\repos\TypeSafe\sample3.py", line 2, in get_first_name
    return full_name.split(" ")[0]
AttributeError: 'dict' object has no attribute 'split'
~~~

ปัญหานี้เกิดจากตัวแปร fallback_name ไม่ใช่ type string แต่มันคือ type dictionary เมื่อเรียกฟังก์ชัน get_frist_name แล้วส่งตัวแปร fallback_name เข้าไป ทำให้ฟังก์ชัน .split() ไม่สามารถทำงานได้

---
Reference:
- [How to Use Static Type Checking in Python 3.6](https://medium.com/@ageitgey/learn-how-to-use-static-type-checking-in-python-3-6-in-10-minutes-12c86d72677b)