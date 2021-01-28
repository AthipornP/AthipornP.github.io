---
layout: post
title: C# TryValidateModel
description: การตรวจสอบความถูกต้องของข้อมูลใน Model
image: assets/images/TryValidateModel/aspnet-core-mvc-logo.jpg
---

## Model คืออะไร?
โครงสร้างการเขียนโค้ตแบบ MVC (Model-View-Controller)  การส่งผ่านข้อมูลต่างๆ ส่วนใหญ่จะอยู่ในรูปแบบของ ***Model***<br/>Model คือแบบจำลองหรือ Class ที่ภายในบรรจุด้วย Property ต่างๆ สำหรับใช้ในการจัดเก็บข้อมูลเป็นกลุ่มก้อน หรือในภาษา OOP จะเรียกเป็น object data เช่น ข้อมูล Personal ภายในก็จะบรรจุข้อมูลชื่อ นามสกุล ส่วนสูง น้ำหนัก อายุ แล้วเมื่อต้องการรับ - ส่งข้อมูล เราก็จะรับ - ส่งไปทั้งก้อน Personal หรือส่งทั้ง object personal นั่นเอง<br/>ภายใน Model เราสามารถระบุ Requirement ต่างๆ ของแต่ละ Property ได้

## TryValidateModel(Object) Method
**Namespace:** Microsoft.AspNetCore.Mvc<br/>**Assembly:** Microsoft.AspNetCore.Mvc.Core.dll

TryValidateModel เป็น method overloads มีให้เลือกใช้งานหลายรูปแบบ ดังตารางด้านล่าง ([รายละเอียดเพิ่มเติม](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.tryvalidatemodel?view=aspnetcore-5.0#Microsoft_AspNetCore_Mvc_ControllerBase_TryValidateModel_System_Object_))<br/>ในบทความนี้จะเป็นตัวอย่างการใช้งาน **TryValidateModel(Object)**

|Overloads|    |
|---------|----|
|**TryValidateModel(Object)**|**Validates the specified model instance.**|
|TryValidateModel(Object, String)|Validates the specified model instance.|

## TryValidateModel(Object)
ใช้ในการตรวจสอบความถูกต้องของข้อมูลใน Property ที่อยู่ใน Object นั้น<br/>
ถ้า Object valid จะ return **true** ถ้าไม่จะ return **false**

## ตัวอย่าง Personal Model
~~~
using System;
using System.ComponentModel.DataAnnotations;

namespace TryValidateModelSample
{
    public class PersonalModel
    {
        [Required(ErrorMessage ="Firstname is required.")]
        [StringLength(20)]
        public string Firstname { get; set; }

        [Required(ErrorMessage = "Lastname is required.")]
        [StringLength(20)]
        public string Lastname { get; set; }

        public double Weight { get; set; }

        public double Height { get; set; }

        [Range(1,100)]
        public int Age { get; set; }
    }
}
~~~

## สร้าง Object ของ Personal Model
~~~
//สร้าง Object ของ Personal Model
var objPersonal = new PersonalModel
{
    Firstname = "Athiporn",
    Lastname = "Phumnicom",
    Weight = 82.00,
    Height = 178.00,
    Age = 31
};
~~~

## Validate Personal Model
ตรวจสอบความถูกต้องของ Object Personal โดยใช้ **TryValidateModel(Object)** Method<br/>
![]({{site.baseurl}}/assets/images/TryValidateModel/valid_true.png){:width="1100px" style="float: center"}
<br/>จากรูป Object \"objPersonal\" มีความถูกต้อง TryValidateModel จะ return ค่าเป็น true

ทดลองเปลี่ยนค่า Age จาก 31 เป็น 150 ซึ่งเกินจากที่เราได้กำหนดไว้ใน Model ด้วยคำสั่ง **[Range(1,100)]** แล้วลอง Validate อีกครั้งด้วย TryValidateMedel จะเห็นว่า return ค่าเป็น false ดังภาพด้านล่าง<br/>
![]({{site.baseurl}}/assets/images/TryValidateModel/valid_false.png){:width="1100px" style="float: center"}

---
Reference:
- [ControllerBase.TryValidateModel Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.tryvalidatemodel?view=aspnetcore-5.0#Microsoft_AspNetCore_Mvc_ControllerBase_TryValidateModel_System_Object_)