# Final-Project---DADS6003
## กลุ่ม 300 (ที่แปลว่า TF-IDF set max_features = 300)

<img width="935" height="491" alt="image" src="https://github.com/user-attachments/assets/0d0ad070-3c1b-4109-8f0e-b01d3b6d0ca5" />


# 1.	Read and understand the paper.


<img width="1494" height="628" alt="image" src="https://github.com/user-attachments/assets/6c9ee818-b15e-45c6-8aa1-d6637e2551a8" />

งานวิจัยฉบับนี้ ศึกษาเรื่องการประเมินตัวกรอง ในการตรวจจับ Phishing Email ที่มีการ Generate จากการป้อน Prompt ให้แก่ LLM (Large Language Model) หรือเรียกทั่วไปว่า AI โดยใช้ Feature ทางการเขียนต่างๆ
เนื่องจากปัจจุบัน ระบบการ Detect Phishing Email ของแต่ละ Email Service provider มักจะใช้เพียงการตรวจสอบ URL ที่อยู่ใน Email เท่านั้น ซึ่งปัจจุบันมีหลายวิธีที่จะหลีกเลี่ยงการตรวจจับนี้ได้แล้ว
เช่น เปลี่ยน URL เป็น URL ของเว็บอื่นที่น่าเชื่อถือ แล้ว Redirect ต่อมาที่ URL ที่เป็น Phishing
โดยในงานวิจัยจะมี 60 Feature ที่ใช้ในการทำแบบจำลอง (Model) ซึ่งมี 47 Feature ที่งานฉบับนี้เพิ่มขึ้นมาใหม่เพื่อการตรวจจับ Phishing Email 

*Phishing Email คือ Email ที่
## ประเภทของคุณสมบัติ (Feature type) และน้ำหนักในการ 
lexical feature (16.7%) เป็นกลุ่มคุณสมบัติด้านตัวอักษรและคำแบบเบื้องต้น เช่น จำนวนคำ จำนวนตัวอักษร

systactic feature (18.3%) กลุ่มคุณสมบัติทางวากยสัมพันธ์ พิจารณาในส่วนของโครงสร้างและไวยากรณ์ของเนื้อหาบน Email

punctuation feature (16.7%) หรือคุณสมบัติด้านเครื่องหมายวรรคตอน พิจารณาในส่วนของเครื่องหมายที่อยู่ในเนื้อหา เช่น เครื่องหมายตกใจ (Exclaimation)

readability feature (16.7%) คุณสมบัติความสามารถในการอ่าน พิจารณาความยากในการอ่านเนื้อหาของ Email โดยมีการใช้ดัชนีชี้วัด เช่น Flesch Reading Ease or SMOG Index

word category feature (11.7%) คุณสมบัติด้านประเภทของคำ พิจารณาประเภทคำที่อยู่บนเนื้อหา Email เช่น คำที่ให้ผู้ใช้กระทำการบน email (Click, Verify) หรือคำชวนต่างๆ (Promotional)

email-specific feature (6.7%) คุณสมบัติด้านที่เกี่ยวกับ Email พิจารณาคำ หรือสิ่งที่เกี่ยวข้องกับ Email เช่น เครื่องหมาย @ การพูดถึง Link ต่างๆ

complexity feature (5.0%) คุณสมบัติความซับซ้อน มีการใช้ Bigram Count, Trigram Count (การนับ Combination ของคำ 2,3 คำ)

stylistic feature (8.3%) คุณสมบัติโวหาร พิจารณาโทนเสียงของเนื้อหาบน email เช่น ความสุภาพ ความเร่งด่วน จากคำที่อยู่ในเนื้อหา

<img width="901" height="357" alt="image" src="https://github.com/user-attachments/assets/532e27b6-2825-471a-9f49-665bbafb4cdf" />



<img width="725" height="436" alt="image" src="https://github.com/user-attachments/assets/5549426c-763d-439f-b011-2979e18acbb9" />

งานวิจัยได้ใช้แบบจำลอง Machine Learning ในด้านการจำแนก (Classification) ที่เป็นที่นิยมจำนวน 4 แบบจำลอง โดยมีเป้าหมายเพื่อประเมินประสิทธิภาพในการใช้คุณลักษณะทางสไตล์การเขียนเพื่อจำแนกอีเมล
1. Logistic Regression

2. SVM (Support Vector Machine)

3. Random Forest

4. XGBoost 
   

นอกจากนี้ยังมีประเด็นที่น่าสนใจอีกอย่าง

<img width="735" height="224" alt="image" src="https://github.com/user-attachments/assets/305f0d2d-7e06-4092-b164-17cae2f80919" />


# 2.	Reproduce its results.

สร้าง Stylometric Features ตามที่ระบุใน Paper ด้วยการคำนวณจริง (Real Calculation)
ผลลัพธ์ที่ได้
<img width="421" height="227" alt="{D8F03CC6-E99E-4067-94AB-2C52CFED0E6C}" src="https://github.com/user-attachments/assets/41f81a80-ca43-4b8a-9e04-c1798c0a7d06" />




# 3.	Propose new ideas based on your research.

จากการศึกษา
