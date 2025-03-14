---
title: Dockerfile
showMetadata: true
editable: true
showToc: true
---

# โครงสร้างของ Dockerfile

แฟ้มข้อมูล Dockerfile เป็นแฟ้มข้อมูลที่ระบุคำสั่งสำหรับสร้างอิมเมจใหม่ แฟ้มข้อมูล Dockerfile ไม่ได้ใช้เก็บแฟ้มข้อมูลของแอปพลิเคชันที่ต้องการบรรจุในคอนเทนเนอร์ แต่ประกอบด้วยลำดับของชุดคำสั่งพร้อมคำสั่งและพารามิเตอร์ ชุดคำสั่ง คือ คำสั่งเฉพาะในรูปแบบคีย์เวิร์ดที่กำหนดโดยโปรแกรมด็อกเกอร์ ส่วนคำสั่ง คือ คำสั่งที่สามารถพิมพ์บนเชลล์ของลีนุกซ์หรือวินโดว์สได้ รูปแบบคำสั่งที่นิยมใช้ใน Dockerfile มีอยู่ 2 รูปแบบ คือ

- รูปแบบของเชลล์ เป็นรูปแบบคำสั่งที่เหมือนกับการพิมพ์คำสั่งบนเชลล์ของลีนุกซ์หรือวินโดว์ส แต่ละส่วนคั่นด้วยการเว้นวรรค หากมีหลายพารามิเตอร์ แต่ละพารามิเตอร์จะคั่นด้วยการเว้นวรรค จะโดยจะมีรูปแบบเป็น
    ```
    <ชุดคำสั่ง> <คำสั่ง> <พารามิเตอร์ของคำสั่ง>
    ```
- รูปแบบด็อกเกอร์ เป็นรูปแบบคำสั่งที่ออกแบบโดยด็อกเกอร์ นิยมใช้คำสั่งหรือพารามิเตอร์ที่มี
เว้นวรรค ถูกเขียนให้อยู่ในรูปแบบคล้ายอาร์เรย์ในภาษาเขียนโปรแกรมคือมีเครื่องหมายอัญประกาศครอบแต่ละคำสั่งและพารามิเตอร์ หากมีหลายพารามิเตอร์แต่ละพารามิเตอร์จะคั่นด้วยเครื่องหมายจุลภาค (,) โดยจะมีรูปแบบเป็น
    ```
    <ชุดคำสั่ง> ["คำสั่ง","พารามิเตอร์1","พารามิเตอร์2",…]
    ```

ในปัจจุบัน ผู้ใช้สามารถใช้รูปแบบใดรูปแบบหนึ่งสำหรับเขียนชุดคำสั่งใน Dockerfile หรือจะเขียนผสมกันระหว่างสองรูปแบบตามความถนัด เช่น คำสั่งแรกใช้รูปแบบเชลล์ อีกคำสั่งใช้รูปแบบด็อกเกอร์ เป็นต้น ในกรณีที่ต้องการคอมเมนต์ชุดคำสั่งบรรทัดไหนสามารถพิมพ์เครื่องหมาย # ให้อยู่ต้นบรรทัด บรรทัดนั้นทั้งบรรทัดจะไม่ถูกประมวลผลในขณะที่สร้างอิมเมจ ด้วยเหตุนี้ โครงสร้างของ Dockerfile จึงเป็นลักษณะที่
สนใจบรรทัด (Line sensitive) และไม่มีตัวคั่นบรรทัดอย่างเครื่องหมาย semi-colon (;) เหมือนในภาษาเขียนโปรแกรมอย่างภาษาซี และหากชุดคำสั่งในรูปแบบของเชลล์มีความยาวมากสามารถขึ้นต้นบรรทัดใหม่ด้วยเครื่องหมายทับขวา (\)


```sh class:"lineNo"
FROM centos:8
# บรรทัดนี้คอนเม้น
RUN yum install wget \
       unzip
CMD ["wget","http://server/file.zip"]
```

บรรทัดแรกมีชุดคำสั่ง FROM พารามิเตอร์เป็น centos:8 บรรทัดที่สองเป็นบรรทัดที่มีเครื่องหมาย # หมายถึงคอมเม้น คือ ไม่มีการประมวลผล บรรทัดที่สามเป็น มีชุดคำสั่งเป็น RUN และมีคำสั่ง yum เพื่อติดตั้งแพ็คเกจ คำสั่ง yum มีความยาว 2 บรรทัดและทำงานเหมือนเป็นคำสั่งบรรทัดเดียวเพราะท้ายบรรทัดที่สองมีเครื่องหมายทับขวา คำสั่ง yum นี้มีพารามิเตอร์เป็น install wget unzip จำนวน 3 พารามิเตอร์ บรรทัดที่ 5ชุดคำสั่งเป็น CMD มีคำสั่ง wget และพารามิเตอร์จำนวน 1 พารามิเตอร์ คือ http://server.file.zip

