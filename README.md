# Final-Project---DADS6003
## กลุ่ม 300⚔️ (ที่แปลว่า TF-IDF set max_features = 300)

<img width="935" height="491" alt="image" src="https://github.com/user-attachments/assets/0d0ad070-3c1b-4109-8f0e-b01d3b6d0ca5" />

# 1.	Read and understand the paper.


<img width="1494" height="628" alt="image" src="https://github.com/user-attachments/assets/6c9ee818-b15e-45c6-8aa1-d6637e2551a8" />

งานวิจัยฉบับนี้ศึกษาเรื่องการตรวจจับ Phishing Email ที่มีการ Generate จาก AI ซึ่งสร้างโดยโดยการป้อน Prompt ให้แก่ AI เพื่อให้ AI Generate content ออกมา 
สาเหตุเนื่องจากปัจจุบัน ระบบการ Detect Phishing Email ของ Email Provider แต่ละเจ้ามักจะใช้เพียงการตรวจสอบ URL ที่อยู่ใน Email เท่านั้น ซึ่งปัจจุบันมีหลายวิธีที่จะหลีกเลี่ยงการตรวจจับนี้ได้แล้ว
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

_ตารางที่ 1 การประเมินค่าของแบบจำลองแต่ละประเภทในงานวิจัย_

<img width="725" height="436" alt="image" src="https://github.com/user-attachments/assets/5549426c-763d-439f-b011-2979e18acbb9" />  

_ตารางที่ 2 Confusion matrix ของแบบจำลองแต่ละประเภทในงานวิจัย_

งานวิจัยได้ใช้แบบจำลอง Machine Learning ในด้านการจำแนก (Classification) ที่เป็นที่นิยมจำนวน 4 แบบจำลอง โดยมีเป้าหมายเพื่อประเมินประสิทธิภาพในการใช้คุณลักษณะทางสไตล์การเขียนเพื่อจำแนกอีเมล  
**1. Logistic Regression**

**2. SVM (Support Vector Machine)**

**3. Random Forest**

**4. XGBoost**
   
โดยในการทำแบบจำลอง จะใช้ข้อมูล email แปลงเป็น Feature ตามที่กำหนด ทั้ง 60 แบบ ก่อนนำเข้าแบบจำลอง


<img width="735" height="224" alt="image" src="https://github.com/user-attachments/assets/305f0d2d-7e06-4092-b164-17cae2f80919" />  
  
_ตารางที่ 3 ประสิทธิภาพของแบบจำลอง XGBoost เมื่อมีการลบ Feature แต่ละขั้น_


# 2.	Reproduce its results.

สร้าง Stylometric Features ตามที่ระบุใน Paper ด้วยการคำนวณจริง (Real Calculation)

ผลลัพธ์ที่ได้จาก Unseen data (test dataset)



<img width="800" height="600" alt="{4F32B022-F510-4F26-8FC6-75B7C32402B1}" src="https://github.com/user-attachments/assets/416fdd27-5ad3-4910-bd8e-ee38c3e189a9" />

_ตารางที่ 4 Evaluation table from [original stylometric features]_

<img width="535" height="590" alt="{AA13E833-CE31-444B-A04D-B9D289332014}" src="https://github.com/user-attachments/assets/e9342708-c28e-49d8-bd83-244889512521" />

_ตารางที่ 5 Confusion matrix table from [original stylometric features]_


   **สรุปผลลัพธ์**
   - จากการ reproduce โดยอาศัยการสร้าง feature จากเทคนิค stylometric ตามงานวิจัยอย่างเดียว พบว่า Model ประเภท Gradient Boosting สมัยใหม่ ได้แก่ XGBoost, LightGBM และ CatBoost ให้ประสิทธิภาพในการจับ Phishing email ได้ดีที่สุด โดยมีค่า Recall, Precision และ F1-score เท่ากันทั้ง 3 Models ที่ 85%, 92% และ 88% ตามลำดับ จึงสามารถตีความได้ว่า ถ้าเป็น feature แบบ stylometric เพียงอย่างเดียว เหล่า Model Boosting จะเป็น Model ที่เหมาะสมที่สุด เพราะ Stylometric feature เป็น feature ที่มีความซับซ้อนในการประเมินด้านภาษา ไม่ใช่เส้นตรง (Non-linear) ซึ่ง Model กลุ่ม Boosting เป็น Model ที่เก่งในด้านการสร้างเงื่อนไขซับซ้อน จากการที่ตัวมันอาศัยการ improve ตัวเองไปเรื่อยๆจาก data subset ตัวก่อนๆ
   - ในทางกลับกันพวก Model ตัวพื้นฐานที่เป็นเส้นตรง (Linear) เช่น Linear Regression, SVM พอต้องใช้ stylometric feature ในการ train model ให้ประสิทธิภาพออกมาได้แค่ระดับกลางๆที่ F1~80% ซึ่งน้อยกว่า Model ประเภท Boosting อย่างเห็นได้ชัด เนื่องจาก Stylometric feature ไม่ได้แปรผันตรงไปตรงมา เหมือนพวก TF-IDF เสมอไป เช่น ประโยค/คำศัพท์ ยิ่งยาวยิ่งค่าสูง บาง feature จำเป็นต้องอาศัยความรู้ด้านภาษาศาสตร์เชิงลึกเข้ามาวิเคราะห์เพื่อให้คะแนน ทำให้ Model เชิงเส้นตรงตีความได้ยาก
   - ในส่วน Naive Bayes (Non-iterative model) ให้ผลลัพธ์ที่ค่อนข้าง Conservative เนื่องจากได้ Precision สูงมากที่ 83% แต่ในทางกลับกันกลับได้ Recall แค่ 38% เท่านั้น ส่งผลให้ F1-score ร่วงไปอยู่อันดับท้ายสุด จึงตีความได้ว่า Model แทบจะจับ หรือ กวาดพวก Phishing email ไม่ได้เลย แต่ถ้าจับได้คือส่วนใหญ่จะใช่ (มีความแม่นยำ แต่กวาดได้น้อย) แต่ในงานนี้ Recall แทบจะเป็นตัวที่มีความสำคัญที่สุด เนื่องจากต้องปล่อยให้ Phishing email หลุดไปน้อยที่สุด ดังนั้นจึงสรุปได้ว่า Model Naive Baes ไม่ควรใช้ train ด้วย Stylometric feature  


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

# รายละเอียด Advanced features 8 ตัว ที่เพิ่มเข้ามา
### 🛡️ 8 Advanced Features (New Ideas)

ได้พัฒนาฟีเจอร์ใหม่ 8 ตัว เพื่อตรวจจับ "พฤติกรรม" และ "กลยุทธ์ทางจิตวิทยา" ของ Phishing Email โดยเฉพาะ

| # | Feature Name | Description | Mechanism |
| :-: | :--- | :--- | :--- |
| 1 | **Imposter Domain Similarity** | ตรวจจับการปลอมแปลงโดเมน (Typosquatting) | วัดความคล้ายคลึงระหว่าง URL ในอีเมลกับโดเมนจริง (เช่น `g0ogle` vs `google`) |
| 2 | **Macro Security Bypass** | ตรวจจับความพยายามฝัง Malware | นับคำสั่งหลอกให้เปิดระบบความปลอดภัย เช่น *"Enable Content"*, *"Enable Macros"* |
| 3 | **Temporal Pressure Score** | วัดระดับการกดดันทางเวลา | คำนวณสัดส่วนคำเร่งรีบ เช่น *"Urgent"*, *"Immediately"*, *"24 hours"* |
| 4 | **Action-Time Coercion** | วัดการบังคับให้กระทำทันที | ตรวจหา Pattern ของ **Action Verb** คู่กับ **Time Constraint** |
| 5 | **Subject-Body Mismatch** | ตรวจจับความไม่สอดคล้องของเนื้อหา | วัดความเหมือน (Similarity) ระหว่าง Subject และ Body |
| 6 | **Emotional Polarity Variance** | ตรวจจับความผิดปกติของอารมณ์ | วัดความแกว่งของ Sentiment (VADER) ในแต่ละประโยค |
| 7 | **Conflicting Authority** | ตรวจจับการอ้างอำนาจที่น่าสงสัย | นับคำอ้างตำแหน่ง (Admin/Support) ที่มาพร้อมคำสั่งเสี่ยง (Download/Password) |
| 8 | **Semantic Cohesion** | วัดความสมเหตุสมผลของภาษา | คำนวณสัดส่วนคำที่ไม่ซ้ำ (Unique Words Ratio) เพื่อจับ Bot-generated text |



---

# 📋 Result

# Experiment : Reproduce Stylometric only


<img width="800" height="600" alt="{4F32B022-F510-4F26-8FC6-75B7C32402B1}" src="https://github.com/user-attachments/assets/416fdd27-5ad3-4910-bd8e-ee38c3e189a9" />

_ตารางที่ 6 ผลลัพธ์การ Reproduce จาก Test data_  

<img width="535" height="590" alt="{AA13E833-CE31-444B-A04D-B9D289332014}" src="https://github.com/user-attachments/assets/e9342708-c28e-49d8-bd83-244889512521" />

_ตารางที่ 7 Confusion matrix ของ Reproduce จาก Test data_  

<img width="1002" height="451" alt="image" src="https://github.com/user-attachments/assets/2056ce9f-2578-480f-8e85-bcb3cb42fc8e" />

_แผนภูมิที่ 1 Top 10 feature ที่มีอิทธิพลต่อ Model XGBoost_   


# Experiment A : Stylometric + 8 Advanced Features


<img width="800" height="600" alt="{55C532B4-68F1-4A10-8D36-F89C40817CC8}" src="https://github.com/user-attachments/assets/2e5083b6-4477-4f88-90fb-94bca8512c21" />  

_ตารางที่ 8 ผลลัพธ์การ Reproduce และเพิ่ม 8 Advance Features_  

<img width="422" height="462" alt="{143567E3-F421-4CB5-9A92-C1244BB3AD04}" src="https://github.com/user-attachments/assets/b9eaf958-5bca-41ef-9d3f-c404cf7dd073" />  

_ตารางที่ 9 Confusion matrix ของการทำ Reproduce และเพิ่ม 8 Advance Features_  

<img width="1073" height="451" alt="image" src="https://github.com/user-attachments/assets/72c7d77d-09ee-421e-ab7b-e8cec3c8238a" />  

_แผนภูมิที่ 2 Top 10 feature ที่มีอิทธิพลต่อ Model XGBoost (รวม Advance Feature)_   



# Experiment B : TF-IDF only


<img width="800" height="600" alt="{9A4CECF7-F93E-4B75-9975-864C215BEE48}" src="https://github.com/user-attachments/assets/dc01e6fc-b419-4a0c-a7d2-d834c7a8a90b" />  

_ตารางที่ 10 ผลลัพธ์การ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF_   

<img width="428" height="466" alt="{EC9463A2-68EB-4E4C-8C65-72580F291FCA}" src="https://github.com/user-attachments/assets/9be2e5f6-31e6-4a20-bd45-5e48211bb1c1" />  

_ตารางที่ 11 Confusion matrix ของการทำ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF_  

<img width="946" height="451" alt="image" src="https://github.com/user-attachments/assets/6128e70b-9a79-42e9-9f71-d71d72c736ef" />  

_แผนภูมิที่ 3 Top 10 feature ที่มีอิทธิพลต่อ Model SVM (รวมตัวแปรจากการทำ TF-IDF)_  


# Experiment C : Hybrid >> [Stylometric + 8 Advanced Features] + [TF-IDF]


<img width="800" height="600" alt="{F034AAB4-646F-4B4A-9A99-981813F5FFD8}" src="https://github.com/user-attachments/assets/166bf6bb-5a20-4d24-9f87-8b446621f183" />  

_ตารางที่ 12 ผลลัพธ์การ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF และ 8 Advance Feature_  

<img width="470" height="510" alt="{034C1F4E-7057-46C1-B922-0A5F542D761F}" src="https://github.com/user-attachments/assets/a15f06a6-4b76-41e5-983f-87679fbf8cfb" />  

_ตารางที่ 13 Confusion matrix และเพิ่มตัวแปรจากวิธีการ TF-IDF และ 8 Advance Feature_  

<img width="1065" height="451" alt="image" src="https://github.com/user-attachments/assets/228f6d4f-37a6-4f44-9899-4b42ad266102" />  

_แผนภูมิที่ 4 Top 10 feature ที่มีอิทธิพลต่อ Model Random Forest (รวมตัวแปรจากการทำ TF-IDF และ 8 Advance Feature)_  


# Best Experiment & Best Model

<img width="685" height="518" alt="{56670471-A412-47B4-B5C6-003DA7F57131}" src="https://github.com/user-attachments/assets/b6829352-f1f4-4ff0-a1e9-3fc912703960" />



# Check Best model overfitting

<img width="846" height="547" alt="image" src="https://github.com/user-attachments/assets/c34c81d0-fc63-43e5-a88c-c95af51c9b66" />



# Feature selection analysis on [best model from best experiment]

<img width="858" height="284" alt="{8C13E1A9-73B2-4490-A39A-A47433254471}" src="https://github.com/user-attachments/assets/b298609e-344b-4712-83e4-44bade6405d5" />













