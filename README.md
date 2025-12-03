# Final-Project---DADS6003
## กลุ่ม 300 (ที่แปลว่า TF-IDF set max_features = 300)

<img width="935" height="491" alt="image" src="https://github.com/user-attachments/assets/0d0ad070-3c1b-4109-8f0e-b01d3b6d0ca5" />

# 1.	Read and understand the paper.


<img width="1494" height="628" alt="image" src="https://github.com/user-attachments/assets/6c9ee818-b15e-45c6-8aa1-d6637e2551a8" />

งานวิจัยฉบับนี้ศึกษาเรื่องการตรวจจับ Phishing Email ที่มีการ Generate จาก AI ซึ่งสร้างโดยโดยการป้อน Prompt ให้แก่ AI เพื่อให้ AI Generate content ออกมา 
เนื่องจากปัจจุบัน ระบบการ Detect Phishing Email ของแต่ละ Email ญrovider มักจะใช้เพียงการตรวจสอบ URL ที่อยู่ใน Email เท่านั้น ซึ่งปัจจุบันมีหลายวิธีที่จะหลีกเลี่ยงการตรวจจับนี้ได้แล้ว
จึงมุ่งเน้นการตรวจจับจากเนื้อหาของ Email แทน โดยในงานวิจัยจะมี 60 Feature ที่ใช้ในการทำแบบจำลอง (Model) ซึ่งมี 47 Feature ที่งานฉบับนี้เพิ่มขึ้นมาใหม่เพื่อการตรวจจับ Phishing Email 

*Phishing Email คือ Email หลอกลวงที่ปลอมตัวเป็นแหล่งที่น่าเชื่อถือเพื่อหลอกให้ผู้รับเปิดเผยข้อมูลส่วนตัว เช่น รหัสผ่าน ข้อมูลบัตรเครดิต หรือข้อมูลธนาคาร 
## ประเภทของคุณสมบัติ (Feature type) 
**lexical feature** เป็นกลุ่มคุณสมบัติด้านตัวอักษรและคำแบบเบื้องต้น เช่น จำนวนคำ จำนวนตัวอักษร

**systactic feature** กลุ่มคุณสมบัติทางวากยสัมพันธ์ พิจารณาในส่วนของโครงสร้างและไวยากรณ์ของเนื้อหาบน Email

**punctuation feature** หรือคุณสมบัติด้านเครื่องหมายวรรคตอน พิจารณาในส่วนของเครื่องหมายที่อยู่ในเนื้อหา เช่น เครื่องหมายตกใจ (Exclaimation)

**readability feature** คุณสมบัติความสามารถในการอ่าน พิจารณาความยากในการอ่านเนื้อหาของ Email โดยมีการใช้ดัชนีชี้วัด เช่น Flesch Reading Ease or SMOG Index

**word category feature** คุณสมบัติด้านประเภทของคำ พิจารณาประเภทคำที่อยู่บนเนื้อหา Email เช่น คำที่ให้ผู้ใช้กระทำการบน email (Click, Verify) หรือคำชวนต่างๆ (Promotional)

**email-specific feature** คุณสมบัติด้านที่เกี่ยวกับ Email พิจารณาคำ หรือสิ่งที่เกี่ยวข้องกับ Email เช่น เครื่องหมาย @ การพูดถึง Link ต่างๆ

**complexity feature** คุณสมบัติความซับซ้อน มีการใช้ Bigram Count, Trigram Count (การนับ Combination ของคำ 2,3 คำ)

**stylistic feature** คุณสมบัติโวหาร พิจารณาโทนเสียงของเนื้อหาบน email เช่น ความสุภาพ (จับคำว่า please เป็นต้น) ความเร่งด่วน (จับคำว่า urgent)  จากคำที่อยู่ในเนื้อหา

<img width="901" height="357" alt="image" src="https://github.com/user-attachments/assets/532e27b6-2825-471a-9f49-665bbafb4cdf" />



<img width="725" height="436" alt="image" src="https://github.com/user-attachments/assets/5549426c-763d-439f-b011-2979e18acbb9" />

งานวิจัยได้ใช้แบบจำลอง Machine Learning ในด้านการจำแนก (Classification) ที่เป็นที่นิยมจำนวน 4 แบบจำลอง โดยมีเป้าหมายเพื่อประเมินประสิทธิภาพในการใช้คุณลักษณะทางสไตล์การเขียนเพื่อจำแนกอีเมล
1. Logistic Regression

2. SVM (Support Vector Machine)

3. Random Forest

4. XGBoost 
   
โดยในการทำแบบจำลอง จะใช้ข้อมูล email แปลงเป็น Feature ตามที่กำหนด ทั้ง 60 แบบ ก่อนนำเข้าแบบจำลอง
นอกจากนี้ยังมีประเด็นที่น่าสนใจอีกอย่าง


<img width="735" height="224" alt="image" src="https://github.com/user-attachments/assets/305f0d2d-7e06-4092-b164-17cae2f80919" />


# 2.	Reproduce its results.

สร้าง Stylometric Features ตามที่ระบุใน Paper ด้วยการคำนวณจริง (Real Calculation)

ผลลัพธ์ที่ได้จาก Unseen data (test dataset)

**ตารางที่ ... Evaluation table from [original stylometric features]**

<img width="800" height="600" alt="{D8F03CC6-E99E-4067-94AB-2C52CFED0E6C}" src="https://github.com/user-attachments/assets/41f81a80-ca43-4b8a-9e04-c1798c0a7d06" />

**ตารางที่ ... Confusion matrix table from [original stylometric features]**

<img width="384" height="412" alt="{52573E75-3F8A-4B87-B636-2280146CBEF2}" src="https://github.com/user-attachments/assets/d98696aa-7678-4d20-badb-46afdc09695b" />

   **สรุปผลลัพธ์**
   - จากการ reproduce โดยอาศัยการสร้าง feature จากเทคนิค stylometric ตามงานวิจัยอย่างเดียว พบว่าพวก Model ชนิด Gradient Boosting สมัยใหม่ทั้งหลาย เช่น XGBoost, LightGBM และ CatBoost ให้ประสิทธิภาพในการจับ Phishing email ได้ดีที่สุด โดยมีค่า Recall, Precision และ F1-score อยู่เท่ากันทั้ง 3 Models ที่ 77%, 91% และ 83% ตามลำดับ จึงสามารถตีความได้ว่า ถ้าเป็น feature แบบ stylometric เพียงอย่างเดียว เหล่า Model Boosting จะเป็น Model ที่เหมาะสมที่สุด เพราะ Stylometric feature เป็น feature ที่มีความซับซ้อนในการประเมินด้านภาษา ไม่ใช่เส้นตรง (Non-linear) ซึ่ง Model กลุ่ม Boosting เป็น Model ที่เก่งในด้านการสร้างเงื่อนไขซับซ้อน จากการที่ตัวมันอาศัยการ improve ตัวเองไปเรื่อยๆจาก data subset ตัวก่อนๆ
   - ในทางกลับกันพวก Model ตัวพื้นฐานที่เป็นเส้นตรง (Linear) เช่น Linear Regression, SVM พอต้องใช้ stylometric feature ในการ train model ให้ประสิทธิภาพออกมาได้แค่ระดับกลางๆที่ F1~77% น้อยกว่าพวกตระกูล Boosting อย่างเห็นได้ชัด เนื่องจาก Stylometric feature มันไม่ได้แปรผันตรงไปตรงมา เหมือนพวก TF-IDF เสมอไป เช่น ประโยค/คำศัพท์ ยิ่งยาวยิ่งค่าสูง บาง feature จำเป็นต้องอาศัยความรู้ด้านภาษาศาสตร์เชิงลึกเข้ามาวิเคราะห์เพื่อให้คะแนน ทำให้ Model เชิงเส้นตรงตีความได้ยาก
   - Naive Bayes (Non-iterative model) ให้ผลลัพธ์ที่ค่อนข้าง Conservative มาก คือ ได้ Precision สูงมากที่ 83% ในทางกลับกันกลับได้ Recall แค่ 38% เท่านั้น ทำให้ F1-score ร่วงไปอยู่อันดับท้ายสุด จึงตีความได้ว่า Model แทบจะจับ หรือ กวาดพวก Phishing email ไม่ได้เลย แต่ถ้าจับได้คือส่วนใหญ่จะใช่ แต่ในงานนี้ Recall แทบจะเป็นตัวที่มีความสำคัญที่สุด เนื่องจากต้องปล่อยให้ Phishing email หลุดไปน้อยที่สุด ดังนั้นจึงสรุปได้ว่า Model Naive Baes ไม่ควรใช้ train ด้วย Stylometric feature  


# 3. Propose new ideas based on your research

Project นี้เป็นการพัฒนาระบบตรวจจับ **Phishing Email** โดยมีเป้าหมายเพื่อต่อยอดจากงานวิจัยเดิม (Reproduce) และนำเสนอแนวทางใหม่ (New Ideas) เพื่อเพิ่มประสิทธิภาพความแม่นยำ โดยเปรียบเทียบระหว่างเทคนิค **Stylometric Analysis** (การวิเคราะห์สไตล์การเขียนแบบเดิม) กับการใช้ **NLP (TF-IDF)** และ **Advanced Features** (พฤติกรรมการหลอกลวง)

เราได้ออกแบบการทดลอง (Experimental Design) ออกเป็น 4 รูปแบบ เพื่อวัดผลกระทบของ Feature แต่ละชุด ดังนี้

### 🧪 Experimental Setup

| การทดลอง (Experiment) | รายละเอียด (Description) | Features ที่ใช้ |
| :--- | :--- | :--- |
| **🔁 Reproduce** | **Baseline:** จำลองผลลัพธ์ตาม Paper ต้นฉบับ | **Stylometric Only** <br>*(ไม่รวม 8 Advanced Features)* |
| **💡 Experiment A** | **Behavioral:** เพิ่มฟีเจอร์จับพฤติกรรมคนโกง | **Stylometric + 8 Advanced Features** |
| **💡 Experiment B** | **Content-based:** ใช้ NLP จับ Keywords สำคัญ | **TF-IDF Only** |
| **💡 Experiment C** | **Hybrid:** รวมทุกเทคนิคเข้าด้วยกัน | **Stylometric + TF-IDF + Advanced** |

---

### 🛠️ Project Workflow

แผนภาพด้านล่างแสดงขั้นตอนการทำงาน (Pipeline) ตั้งแต่การเตรียมข้อมูล, การสร้าง Features ทั้ง 3 กลุ่ม, การแยกสายการทดลอง, ไปจนถึงการจูนโมเดลและการประเมินผลลัพธ์สุดท้าย

   ```mermaid
flowchart TD
    subgraph Input ["📂 Data Preparation"]
        Raw["Raw Emails (Train/Test)"] --> Clean["Preprocessing"];
    end

    subgraph Features ["⚙️ Feature Engineering"]
        Clean --> Feat1["1. Stylometric (Paper Reproduce)"];
        Clean --> Feat2["2. Advanced (Behavioral)"];
        Clean --> Feat3["3. TF-IDF (NLP Content)"];
    end

    subgraph Experiments ["🧪 Experiment Scenarios"]
        Feat1 --> ExpR["Reproduce: Stylo Only"];
        Feat1 & Feat2 --> ExpA["Exp A: Stylo + Adv"];
        Feat3 --> ExpB["Exp B: NLP Only"];
        Feat1 & Feat2 & Feat3 --> ExpC["Exp C: All Combined"];
    end

    subgraph Modeling ["🤖 AI Pipeline"]
        ExpR & ExpA & ExpB & ExpC --> Tuning["Optuna Hyperparameter Tuning"];
        Tuning --> Train["Train 9 ML Models (Boosting, Linear, Trees)"];
        Train --> Valid["5-Fold Cross Validation"];
    end

    subgraph Result ["📊 Final Evaluation"]
        Valid --> Test["Test on Unseen Data"];
        Test --> Metrics["F1-score Analysis"];
        Metrics --> Winner["🏆 Best Model Selection"];
    end

    subgraph Optimization ["🔍 Feature Selection (Best Model)"]
        Winner --> Importance["Analyze Feature Importance"];
        Importance --> TopK["Select Top-K Features (10, 20, 30)"];
        TopK --> Retrain["Retrain & Re-evaluate"];
        Retrain --> Final["🏁 Final Optimization Result"];
    end

    style Winner fill:#f9f,stroke:#333,stroke-width:4px
    style ExpB fill:#bbf,stroke:#333,stroke-width:2px
    style Final fill:#d4edda,stroke:#155724,stroke-width:2px,stroke-dasharray: 5 5
   ```

---

### 📋 Result

# Experiment : Reproduce Stylometric only

<img width="800" height="600" alt="{05D4AD2D-A912-4724-A4E4-2A25CDDEC12F}" src="https://github.com/user-attachments/assets/3d1f0cf0-344e-4caa-beb8-76a22fae141e" />

<img width="374" height="386" alt="{474366A0-C70E-4648-B9C3-178C94C77019}" src="https://github.com/user-attachments/assets/ac02ca8f-06cb-4995-8d4f-849773fca692" />

<img width="594" height="276" alt="{2240CD48-DC33-4DEC-9A4B-5BCF041A3159}" src="https://github.com/user-attachments/assets/62123edd-dbd3-4ed4-8983-5b7df021309f" />


# Experiment A : Stylometric + 8 Advanced Features

<img width="800" height="600" alt="{74648B7A-48E8-4BC0-ABCB-A4B2E4C8C6C6}" src="https://github.com/user-attachments/assets/2c37d4a6-f03f-46f5-a678-872dd9028828" />

<img width="374" height="386" alt="{F804FC69-172C-4B35-9C9B-0E43E38F5B6E}" src="https://github.com/user-attachments/assets/1125d90f-c875-4651-9e53-93cb3135e04c" />

<img width="580" height="237" alt="{121AC9BB-95D9-4BD1-972D-4C4043C8C980}" src="https://github.com/user-attachments/assets/610bfaba-1f06-45ab-ac6a-c4ab736d15a7" />


# Experiment B : TF-IDF only

<img width="800" height="600" alt="{1AB13AA2-EB63-403D-AB6F-E9DA699E95E2}" src="https://github.com/user-attachments/assets/5f183a11-d02c-4c86-9d53-8c75ed467bdd" />

<img width="374" height="386" alt="{38952657-B9AD-4183-B914-74224371A108}" src="https://github.com/user-attachments/assets/4fec280f-fa35-4196-b41b-33e1f43070ce" />


# Experiment C : Hybrid >> [Stylometric + 8 Advanced Features] + [TF-IDF]

<img width="800" height="600" alt="{E7B7E454-36C9-4F22-8A7B-454177D98CB3}" src="https://github.com/user-attachments/assets/56691362-871f-4b67-9fd4-bb8a7a28fe9e" />

<img width="374" height="386" alt="{F256B857-45C3-48F7-8FC5-8BDB42F87A54}" src="https://github.com/user-attachments/assets/a44b37ab-2409-4a13-82e4-69db185ff2f6" />

<img width="545" height="225" alt="{33A7F80A-317B-46C5-B86A-BE81A9F4E381}" src="https://github.com/user-attachments/assets/9c717ba1-e6a6-46c5-9d7d-95eff45ea431" />


# Best Experiment & Best Model

<img width="568" height="420" alt="{2792B258-9378-49B9-A123-0638046B6438}" src="https://github.com/user-attachments/assets/0a534117-5870-46af-8c36-d1eb1d85bc23" />


# Check Best model overfitting

<img width="666" height="424" alt="{EA90A41B-707C-4549-B820-49F2BE5B4AAE}" src="https://github.com/user-attachments/assets/bdf60ecb-92df-48ed-ad52-5cdc54728595" />















