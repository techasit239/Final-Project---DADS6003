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



<img width="800" height="600" alt="{EB646097-0F2B-4CE1-BA2F-08D23EE2135E}" src="https://github.com/user-attachments/assets/b9ded863-3d62-4375-a1f8-a3cf92dea027" />

_ตารางที่ 4 Evaluation table from [original stylometric features]_


<img width="326" height="239" alt="{4C727D87-92B5-475A-B3AD-7C5A8A0FD935}" src="https://github.com/user-attachments/assets/5b8d187a-5dfb-440a-b19f-d7e045994a6c" />

_ตารางที่ 5 Confusion matrix table from [original stylometric features]_


<img width="994" height="590" alt="image" src="https://github.com/user-attachments/assets/f15c60e2-c99f-42e5-9e9b-95b014be8195" />

_แผนภูมิที่ 1 Top 10 feature ที่มีอิทธิพลต่อ Model RandomForrest_   


### 📊 1. Reproduce Results (Untuned)
> **Baseline Experiment:** การทดสอบโดยใช้ Stylometric Features แบบดั้งเดิม (ตาม Paper) และใช้ค่า Default Parameters (No Tuning)

จากการทดลองพบว่าโมเดล **Random Forest** ให้ประสิทธิภาพสูงสุด เหนือกว่าโมเดลพื้นฐาน (Logistic Regression) และโมเดลซับซ้อน (XGBoost) ที่ยังไม่ได้ปรับจูน

* 🏆 **Best Model:** Random Forest
* 🎯 **F1-score:** **83.33%**
* 🎯 **Recall:** **76.92%**
* 🎯 **Precision:** **90.91%**

#### 🔍 Key Insights & Feature Importance
Random Forest สามารถจับ **"ลายเซ็น" (Signature)** ของ Phishing Email ได้ดีที่สุดผ่านฟีเจอร์หลัก 3 อันดับแรก:

1.  **`punctuation_frequency` (10.0%)**: พฤติกรรมการใช้เครื่องหมายวรรคตอนที่ฟุ่มเฟือยผิดปกติ
2.  **`first_person_pronoun_count` (7.5%)**: การใช้สรรพนามแทนตนเอง (I, We, My) เพื่อสร้างเรื่องราว (Storytelling)
3.  **`ling_digit_count` (6.9%)**: การปรากฏของตัวเลขในเนื้อหา (เช่น จำนวนเงิน, รหัสอ้างอิง)

**สรุปและวิเคราะห์ผล**

   * สาเหตุที่ **Random Forest** ชนะในสถานการณ์นี้ เพราะลักษณะของ Stylometric Features (เช่น จำนวนคำ, ความถี่สัญลักษณ์) มีความสัมพันธ์แบบ **Non-linear** จึงมี **Noise** ปะปนอยู่มาก ซึ่ง Random Forest มีกลไกที่เรียกว่า **Bagging (Bootstrap Aggregating)** ที่ช่วยลดความแปรปรวน (Variance) และทนทานต่อ Noise ได้ดีกว่าโมเดลอื่นโดยไม่ต้องปรับจูน ในขณะที่ Logistic Regression (Linear) ไม่สามารถจับ Pattern ที่ซับซ้อนได้ และ XGBoost (Boosting) มักต้องการการจูน Hyperparameter ที่ละเอียดก่อนจึงจะแสดงประสิทธิภาพสูงสุด

# 3. Propose new ideas based on your research

   Project นี้เป็นการพัฒนาระบบตรวจจับ **Phishing Email** โดยมีเป้าหมายเพื่อต่อยอดจากงานวิจัยเดิม (Reproduce) และนำเสนอแนวทางใหม่ (New Ideas) เพื่อเพิ่มประสิทธิภาพความแม่นยำ โดยเปรียบเทียบระหว่างเทคนิค **Stylometric Analysis** (การวิเคราะห์สไตล์การเขียนแบบเดิมตามงานวิจัย) กับการใช้ **NLP (TF-IDF)** และ **Advanced Features** (พฤติกรรมการหลอกลวง)

### 🧪 Experimental Setup

ได้ออกแบบการทดลองออกเป็นทั้งหมด 5 รูปแบบ โดยแบ่งเป็น 1 รูปแบบเดิมตามงานวิจัย และ 4 รูปแบบใหม่
เพื่อเปรียบเทียบประสิทธิภาพตั้งแต่การทำซ้ำงานวิจัยเดิม (Baseline) ไปจนถึงการปรับปรุงด้วยเทคนิคใหม่ๆ (New Ideas)

| การทดลอง (Experiment) | รายละเอียด (Description) | Features ที่ใช้ | Models |
| :--- | :--- | :--- | :--- |
| **0. 🔁 Reproduce (Untuned)** | **Baseline:** จำลองตาม Paper 100% <br>*(ไม่จูน Hyperparameter, ไม่ตัด Feature)* | **Raw Stylometric** <br>*(~60 features)* | 4 Models <br>*(ตาม Paper)* |
| **1. 💡 Reproduce (Tuned)** | **Optimized Baseline:** ปรับปรุงจากข้อ 1 <br>*(จูนด้วย Optuna + ตัด Feature ซ้ำซ้อน)* | **Filtered Stylometric** <br>*(ตัด High Correlation)* | 9 Models |
| **2. 💡 Experiment A** | **Behavioral (New Idea):** <br>เพิ่มฟีเจอร์จับพฤติกรรม/เจตนาหลอกลวง | **Stylometric + 8 Advanced** | 9 Models |
| **3. 💡 Experiment B** | **Content-based (New Idea):** <br>ใช้ NLP (TF-IDF) จับ Keywords สำคัญ | **TF-IDF Only** <br>*(Max 300 features)* | 9 Models |
| **4. 💡 Experiment C** | **Hybrid (New Idea):** <br>รวมทุกเทคนิคเข้าด้วยกัน | **Stylometric + Advanced + TF-IDF** | 9 Models |

---

### 🛠️ Project Workflow

แผนภาพด้านล่างแสดงขั้นตอนการทำงาน (Pipeline) ตั้งแต่การเตรียมข้อมูล, การสร้าง Features ทั้ง 3 กลุ่ม, การแยกสายการทดลอง, ไปจนถึงการจูนโมเดลและการประเมินผลลัพธ์สุดท้าย

   ```mermaid
flowchart TD
    subgraph Input ["📂 Data Preparation"]
        Raw["Raw Emails (Train/Test)"] --> Clean["Preprocessing"];
    end

    subgraph Features ["⚙️ Feature Engineering"]
        Clean --> FeatRaw["1. Stylometric (Raw)"];
        Clean --> FeatAdv["2. Advanced (Behavioral)"];
        Clean --> FeatTFIDF["3. TF-IDF (Content)"];
        
        FeatRaw --> SelectCorr["✂️ Correlation Filtering<br/>(Remove highly correlated features)"];
        SelectCorr --> FeatStyloFiltered["Stylometric (Filtered)"];
        FeatAdv --> FeatAdvFiltered["Advanced (Filtered)"];
    end

    subgraph Experiments ["🧪 Experiment Scenarios"]
        %% Reproduce (Untuned)
        FeatRaw --> ExpR_Untuned["1. Reproduce (Untuned)<br/>4 Paper Models | No Tuning | Raw Feats"];
        
        %% New Ideas (Tuned)
        FeatStyloFiltered --> ExpR_Tuned["2. Reproduce (Tuned)<br/>9 Models | Tuned | Filtered Feats"];
        
        FeatStyloFiltered & FeatAdvFiltered --> ExpA["3. Exp A: Stylo + Adv<br/>(Behavioral Idea)"];
        
        FeatTFIDF --> ExpB["4. Exp B: TF-IDF Only<br/>(Content Idea)"];
        
        FeatStyloFiltered & FeatAdvFiltered & FeatTFIDF --> ExpC["5. Exp C: Combined All<br/>(Hybrid Idea)"];
    end

    subgraph Modeling ["🤖 AI Pipeline"]
        ExpR_Untuned --> TrainDefault["Train Default Models"];
        
        ExpR_Tuned & ExpA & ExpB & ExpC --> Tuning["Optuna Hyperparameter Tuning"];
        Tuning --> TrainTuned["Train Optimized Models"];
        
        TrainDefault & TrainTuned --> Valid["Stratified 5-Fold CV"];
    end

    subgraph Result ["📊 Final Evaluation"]
        Valid --> Test["Test on Unseen Data"];
        Test --> Metrics["F1-score Analysis"];
        Metrics --> Winner["🏆 Global Best Model Selection"];
    end

    subgraph Optimization ["🔍 Post-Training Analysis"]
        Winner --> Overfit["Check Overfitting (Cost Function)"];
        Winner --> Importance["Feature Importance Analysis"];
        Importance --> TopK["Select Top-K (10, 20, 30)"];
        TopK --> Final["🏁 Final Optimization Result"];
    end

    style Winner fill:#f9f,stroke:#333,stroke-width:4px
    style ExpB fill:#bbf,stroke:#333,stroke-width:2px
    style SelectCorr fill:#ffcccc,stroke:#d9534f,stroke-width:1px,stroke-dasharray: 5 5
    style Final fill:#d4edda,stroke:#155724,stroke-width:2px
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


# ⚖️ Features selection 

<img width="954" height="66" alt="{7F031135-3396-4A4E-B455-F89D4B8DBDC1}" src="https://github.com/user-attachments/assets/42dfac77-00e6-4f1d-adbe-6cade2423618" />

<img width="484" height="442" alt="image" src="https://github.com/user-attachments/assets/65ea2bfd-a9ca-4291-89ca-778b55d3c300" />

### ✂️ Feature Selection (Correlation Analysis)

เพื่อลดความซ้ำซ้อนของข้อมูล (Multicollinearity) และเพิ่มประสิทธิภาพของโมเดล เราได้ทำการวิเคราะห์ Correlation และตัด Features ที่มีความสัมพันธ์กันสูงเกิน 95% ออกจำนวน 12 ตัว ดังนี้:

```
Dropped Features (High Correlation > 0.95):
-------------------------------------------
1.  uppercase_word_ratio_2        # ซ้ำซ้อนกับ upper_ratio
2.  gunning_fog_index             # ซ้ำซ้อนกับ readability scores อื่นๆ
3.  bigram_unique_count           # สัมพันธ์กับ word_count สูง
4.  trigram_total_count           # สัมพันธ์กับ word_count สูง
5.  trigram_unique_count          # สัมพันธ์กับ word_count สูง
6.  personalisation_markers_count # ซ้ำซ้อนกับ pronoun counts
7.  ling_word_count               # ซ้ำซ้อนกับ word_count หลัก
8.  ling_unique_word_count        # ซ้ำซ้อนกับ vocab_size
9.  ling_email_count              # ซ้ำซ้อนกับ num_emails
10. ling_upper_ratio              # ซ้ำซ้อนกับ upper_ratio
11. ling_space_count              # ซ้ำซ้อนกับ space_count
12. ling_alpha_count              # ซ้ำซ้อนกับ char_count
```



---

# 📋 Result


# Experiment : Reproduce Stylometric only


<img width="800" height="600" alt="{2A5A1EBF-5936-4CB1-BF35-87E62DA76855}" src="https://github.com/user-attachments/assets/b42daca3-f9ac-47c2-90a3-51e9614ee01e" />

_ตารางที่ 6 ผลลัพธ์การ Reproduce จาก Test data_  


<img width="315" height="408" alt="{9016A039-598E-46C2-AE65-099E5D4152AC}" src="https://github.com/user-attachments/assets/e4b5adeb-d13d-4de9-89a0-0b39daf62cdc" />

_ตารางที่ 7 Confusion matrix ของ Reproduce จาก Test data_  


<img width="994" height="590" alt="image" src="https://github.com/user-attachments/assets/1c205f50-f326-43ef-91ef-fd15bd28559f" />

_แผนภูมิที่ 1 Top 10 feature ที่มีอิทธิพลต่อ Model XGBoost_   


   **สรุปผลลัพธ์**
### 📊 1. Reproduce Results (Tuned)
> **Optimized Baseline:** การทดสอบโดยใช้ Stylometric Features เดิม (ตาม Paper) แต่พัฒนาด้วยการคัดกรองฟีเจอร์ที่ซ้ำซ้อน (Feature Selection) และปรับจูน Hyperparameter ด้วย Optuna

จากการทดลองพบว่าโมเดล **CatBoost** พลิกกลับมาเป็นผู้ชนะด้วยประสิทธิภาพที่สูงขึ้นอย่างชัดเจน (F1-score เพิ่มจาก 83.33% เป็น **88.00%**) แซงหน้า Random Forest ที่เป็นแชมป์ในรอบ Untuned

* 🏆 **Best Model:** CatBoost
* 🎯 **F1-score:** **88.00%**
* 🎯 **Recall:** **84.62%**
* 🎯 **Precision:** **91.67%**

#### 🔍 Key Insights & Feature Importance
CatBoost ยังคงให้ความสำคัญกับ "ลายเซ็น" เดิมของ Phishing แต่สามารถเรียนรู้น้ำหนักความสำคัญได้ละเอียดขึ้น:

1.  **`punctuation_frequency` (13.8%)**: การใช้เครื่องหมายวรรคตอนที่มากผิดปกติยังคงเป็นสัญญาณที่ชัดเจนที่สุด
2.  **`first_person_pronoun_count` (11.5%)**: การเล่าเรื่องด้วยสรรพนามบุรุษที่ 1 (I, We) เพื่อสร้างความน่าเชื่อถือหรือความเห็นอกเห็นใจ
3.  **`ling_digit_count` (7.7%)**: การปรากฏของตัวเลขในเนื้อหา (เช่น จำนวนเงิน, วันที่, รหัส) เพื่อสร้างความสมจริง

**สรุปและวิเคราะห์ผล:**

   * การที่ **CatBoost** (Gradient Boosting) สามารถแซงหน้า Random Forest (Bagging) ในรอบนี้ได้ แสดงให้เห็นถึงพลังของ **Hyperparameter Tuning** ที่ช่วยให้โมเดลเรียนรู้จากข้อผิดพลาดเดิมซ้ำๆ (Sequential Learning) จนสามารถเพิ่มประสิทธิภาพเฉลี่ยในการจับ พวก Phishing email ได้ดีขึ้น (F1-score) และกวาด (Recall) ได้มากขึ้นเป็น 88.00% และ 84.62% ตามลำดับ (จากเดิมที่ RamdomForrest F1 83.33% และ Recall 76.92%) ซึ่ง CatBoost มีจุดเด่นเรื่อง **Ordered Boosting** ที่ช่วยลดปัญหา Overfitting ได้ดีกว่าโมเดล Boosting อื่นๆ เมื่อได้รับการปรับจูนอย่างเหมาะสม จึงสามารถรีดประสิทธิภาพจาก Stylometric Features ได้สูงสุด


# Experiment A : Stylometric + 8 Advanced Features


<img width="800" height="600" alt="{F4AF9952-1D80-4426-898E-A74154BF340F}" src="https://github.com/user-attachments/assets/399166ba-3733-4d06-8a75-97f78508a94a" />

_ตารางที่ 8 ผลลัพธ์การ Reproduce และเพิ่ม 8 Advance Features_  

<img width="530" height="573" alt="{AB50F651-0F6E-4DC7-A85E-96EEBE38AEA2}" src="https://github.com/user-attachments/assets/76bace5c-6a24-43cc-8279-c1a8a394a462" />

_ตารางที่ 9 Confusion matrix ของการทำ Reproduce และเพิ่ม 8 Advance Features_  

<img width="1073" height="451" alt="image" src="https://github.com/user-attachments/assets/7e6a   9f9c-d316-40f6-ad25-f2f9e2fa7d02" />

_แผนภูมิที่ 2 Top 10 feature ที่มีอิทธิพลต่อ Model XGBoost (รวม Advance Feature)_   


   **สรุปผลลัพธ์**
   - จากการทดลอง Experiment A ที่ได้นำเสนอไอเดียใหม่โดยการเพิ่ม 8 Advanced Features เข้ากับ Stylometric Features เดิม พบว่าโมเดล XGBoost ยังคงเป็น Model ที่มีประสิทธิภาพสูงที่สุด และยังเพิ่มประสิทธิภาพสูงขึ้นอย่างชัดเจนจากการทดสอบเดิม โดยทำค่า F1-score ได้ถึง 88.00% (สูงกว่างาน Reproduce ที่ทำได้ 83.33%) พร้อมค่า Precision ที่สูงถึง 91.67% โดยจุดเปลี่ยนสำคัญ อยู่ที่การเพิ่มฟีเจอร์ด้านพฤติกรรม (Behavioral Features) เข้ามา โดยเฉพาะ Action_Time_Coercion_Density ที่กลายเป็น Feature ที่มีอิทธิพลสูงสุด (Feature Importance 15.9%) มากกว่า Feature เดิม จึงบ่งชี้ได้ว่า Model ยังสามารถเรียนรู้ "เจตนาการบีบคั้น" ของคนร้ายที่ต้องการให้เหยื่อรีบกระทำบางอย่างได้ และเมื่อทำงานร่วมกับสัญญาณการตะโกนกดดัน (upper_ratio) และการสร้างฟอร์มทางการปลอม (char_freq_[) ทำให้ Model ยกระดับจากการมองแค่เพียง "สไตล์การเขียน" มาเป็นการตรวจจับที่ "กลยุทธ์การหลอกลวง" (Deception Tactics) เพิ่มเติม ส่งผลให้สามารถคัดกรองอีเมล Phishing ได้อย่างแม่นยำและครอบคลุมยิ่งขึ้นกว่างานวิจัยเดิม


# Experiment B : TF-IDF only


<img width="800" height="600" alt="{3DF8F4E0-48D5-4D52-96BB-E4557BE2CF4E}" src="https://github.com/user-attachments/assets/edecec60-e1fb-4144-b36a-21722c698beb" />

_ตารางที่ 10 ผลลัพธ์การ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF_   

<img width="535" height="588" alt="{5EE6A487-495A-41F3-85BA-BB2F5AE27218}" src="https://github.com/user-attachments/assets/5ef7a515-2ae3-4f85-b9dd-d2602858b20b" />

_ตารางที่ 11 Confusion matrix ของการทำ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF_  

<img width="946" height="451" alt="image" src="https://github.com/user-attachments/assets/c4245e93-5a53-48e0-8b50-7dcb3e64f606" />

_แผนภูมิที่ 3 Top 10 feature ที่มีอิทธิพลต่อ Model SVM (รวมตัวแปรจากการทำ TF-IDF)_  

   **สรุปผลลัพธ์**
   - จากการทดลอง Experiment B ที่เปลี่ยนแนวทางมาใช้เทคนิค NLP ด้วยการสกัดคำศัพท์สำคัญ (TF-IDF) เพียงอย่างเดียว พบว่าเกิดจุดเปลี่ยนสำคัญที่ทำให้โมเดลกลุ่มเส้นตรง (Linear) อย่าง SVM พลิกกลับมาเป็น Model ที่ประสิทธิภาพชนะ Model อื่นๆ ขาดลอย ด้วยค่า F1-score สูงถึง 96.30% และจุดสำคัญคือค่า Recall ได้เต็ม 100% (ไม่ปล่อยให้ Phishing หลุดรอดไปได้แม้แต่ฉบับเดียว) ซึ่งเอาชนะโมเดลตระกูล Boosting ที่เคยเป็น Model ที่ประสิทธิภาพสูงสุดจากการทดลองอื่นได้อย่างราบคาบ สาเหตุเนื่องจากเพราะข้อมูลแบบข้อความ (Text) ที่ถูกแปลงเป็น TF-IDF นั้นมีลักษณะเป็นมิติที่กว้าง และกระจายตัว ซึ่งลักษณะข้อมูลดังกล่าวเหมาะกับโมเดลอย่าง SVM และ Logistic Regression ที่เก่งในการขีดเส้นแบ่ง (Hyperplane) เพื่อแยกแยะคำศัพท์อันตรายอย่าง 'organization', 'xyz' หรือ 'solutions' ได้อย่างเด็ดขาดและแม่นยำ ในขณะที่โมเดลซับซ้อนอย่าง Decision Tree หรือ Boosting กลับทำผลงานได้ลดลงเพราะข้อมูลที่มีขนาดเล็ก (Small Data) ทำให้เกิดสัญญาณรบกวน (Noise) ได้ง่าย จึงสรุปได้ว่าสำหรับโจทย์นี้ การจับผิดที่ "เนื้อหา (Content)" เป็นวิธีการที่ทรงพลังและแม่นยำที่สุด


# Experiment C : Hybrid >> [Stylometric + 8 Advanced Features] + [TF-IDF]


<img width="800" height="600" alt="{02D2D0DB-F8B4-4CDF-8884-DCC82D07EECC}" src="https://github.com/user-attachments/assets/135483b0-643d-4cbd-8aee-6a8a4743a175" />

_ตารางที่ 12 ผลลัพธ์การ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF และ 8 Advance Feature_  

<img width="523" height="580" alt="{5007D3A1-1D73-47D3-9880-6721343CE9F3}" src="https://github.com/user-attachments/assets/7ec056d7-a804-48f0-9324-87c460deeb76" />

_ตารางที่ 13 Confusion matrix และเพิ่มตัวแปรจากวิธีการ TF-IDF และ 8 Advance Feature_  

<img width="1065" height="451" alt="image" src="https://github.com/user-attachments/assets/552ec521-2bc2-4d1b-9d2b-2790f3c30c60" />

_แผนภูมิที่ 4 Top 10 feature ที่มีอิทธิพลต่อ Model Random Forest (รวมตัวแปรจากการทำ TF-IDF และ 8 Advance Feature)_  

   **สรุปผลลัพธ์**
   - จากการทดลอง Experiment C ที่เป็นการรวมทุกอย่าง โดยเอา Feature จากทุกการทดสอบมาใช้ร่วมกัน (Stylometric + Advanced + TF-IDF) พบว่า Model ที่ประสิทธิภาพสูงสุดกลับเปลี่ยนเป็น Random Forest ซึ่งทำคะแนน F1-score ได้สูงสุดถึง 92.31% (ประสิทธิภาพชนะ SVM ที่เป็น Top Model รอบที่แล้ว) เนื่องจากในกรณีที่เอาข้อมูลหลายประเภทมาผสมกัน ทั้งแบบนับคำ (TF-IDF) แบบสถิติ (Stylometric) และแบบพฤติกรรม (Advanced) ข้อมูลจะมีความ "หลากหลายและซับซ้อน" สูงมาก ซึ่งเป็นสิ่งที่ Model ตระกูลต้นไม้ (Tree-based) อย่าง Random Forest ที่เก่งเรื่องการจัดการข้อมูลผสมๆ กันและมีความเสถียรสูง (Robust) ไม่ค่อยหวั่นไหวกับ Noise หรือฟีเจอร์ที่เยอะเกินไป ต่างจาก SVM หรือ Logistic Regression ที่เมื่อมี Feature หลากหลายประเภทรวมกันมาก กลับทำผลงานตกลงไปเหลือแค่ ~76-80% เพราะเริ่มเกิดความสับสนในการขีดเส้นแบ่ง และเมื่อดูลึกลงไปใน Feature ที่ Random Forest เลือกใช้ ก็พบว่ามีการผสมผสาน Feature กันอย่างลงตัวระหว่าง คำศัพท์ ('organization'), พฤติกรรมการบีบคั้น ('Action_Time_Coercion'), และสัญลักษณ์แปลกๆ (']') แสดงให้เห็นว่าการผสมผสาน Feature ช่วยให้ Model มองเห็นภาพรวมได้ดี แต่ต้องเลือก Model ที่ "จัดการความยุ่งเหยิง" ได้เก่งอย่าง Random Forest ถึงจะรีดประสิทธิภาพออกมาได้ดีที่สุด


# Best Experiment & Best Model

<img width="768" height="515" alt="{6AD1C3F6-D882-43AC-A623-0090DA53BE6D}" src="https://github.com/user-attachments/assets/5a3ec026-13ca-4293-a2fa-2b1c1dffb96c" />


   **สรุปผลลัพธ์**
   - สรุปภาพรวมการเปรียบเทียบทั้ง 4 การทดลอง จากการเปรียบเทียบผลลัพธ์ทั้งหมด พบว่า Experiment B (TF-IDF only) คือแนวทางที่มีประสิทธิภาพสูงสุดอย่างชัดเจน โดยทำค่า F1-score ได้สูงถึง 96.30% ด้วยโมเดล SVM ซึ่งเอาชนะแนวทาง Stylometric เดิม (Reproduce) และแนวทางผสมผสาน (Exp A, C) ได้ขาดลอย สาเหตุหลักมาจากชุดข้อมูลมีขนาดเล็ก (Small Data) แต่มีมิติสูงจากคำศัพท์ (High Dimensionality) ซึ่งเป็นทางถนัดของ SVM ที่สามารถขีดเส้นแบ่ง (Hyperplane) ระหว่างคำศัพท์ปกติและคำศัพท์ Phishing ได้อย่างเด็ดขาด ในขณะที่ Experiment C (Combined) ตามมาเป็นอันดับสอง (F1 92.31%) โดยโมเดลที่ชนะคือ Random Forest ซึ่งสะท้อนให้เห็นว่าเมื่อข้อมูลมีความหลากหลายปนเปกันสูง (Mixed Data Types ระหว่าง Text และ Stat) โมเดลตระกูล Tree-based ที่มีความเสถียรจะจัดการกับ Noise ได้ดีกว่า ส่วน Experiment A และ Reproduce ที่เน้นการวิเคราะห์สไตล์และพฤติกรรมนั้น แม้จะได้โมเดล XGBoost มาช่วยรีดประสิทธิภาพได้ดีที่สุด (F1 88% และ 83%) จากความสามารถในการจับ Pattern ที่ซับซ้อน แต่ก็ยังไม่เพียงพอที่จะสู้กับพลังของการวิเคราะห์เนื้อหา (NLP) ได้ จึงสรุปได้ว่าสำหรับโจทย์นี้ **"Content is King"** การรู้คำศัพท์สำคัญเพียงไม่กี่คำ มีน้ำหนักในการตัดสินใจมากกว่าโครงสร้างประโยคหรือพฤติกรรม



# Check Best model overfitting

<img width="855" height="547" alt="image" src="https://github.com/user-attachments/assets/d8570448-83d3-4fb6-a685-21f8fc3bae65" />


   **สรุปผลลัพธ์**
   - สรุปผลกราฟ Learning Curve ของ Best Model (SVM) จากการตรวจสอบกราฟ Learning Curve (Log Loss vs Training Size) ของโมเดล SVM ซึ่งเป็นโมเดลที่ดีที่สุดใน Experiment B (TF-IDF) พบลักษณะที่บ่งชี้ถึง Good fitting อย่างชัดเจน โดยเส้น Training Loss (สีแดง) เริ่มต้นที่จุด Errorสูงมาก แล้วจึงลดลงอย่างชัดเจนเมื่อเจอกับข้อมูลที่หลากหลายขึ้น ในขณะที่เส้น Validation Loss (สีน้ำเงิน) เริ่มต้นจากจุดที่ต่ำกว่า และมีแนวโน้มลดต่ำลงอย่างต่อเนื่องและวิ่งเข้าหาเส้น Training Loss จนช่องว่างระหว่างสองเส้น (Gap) แคบลงเรื่อยๆ เมื่อ Training Size เพิ่มขึ้น ลักษณะการลู่เข้าหากัน (Convergence) ที่ระดับ Loss ต่ำทั้งคู่แบบนี้ แสดงให้เห็นว่าโมเดลเรียนรู้ Pattern จากข้อมูลได้ดีโดยไม่เกิดอาการ Overfitting (จำข้อสอบ) หรือ Underfitting (เรียนรู้ไม่พอ) แม้จะมีข้อมูล Train เพียง 100 ตัวอย่าง แต่โมเดลก็สามารถสรุปกฎเกณฑ์เพื่อนำไปใช้กับข้อมูลใหม่ (Unseen Data) ได้อย่างมีประสิทธิภาพและน่าเชื่อถือ




# Feature selection analysis on [best model from best experiment]

<img width="1050" height="350" alt="{C9F95754-EC37-4004-88BE-16D0B46F997C}" src="https://github.com/user-attachments/assets/8058e539-3d1a-44bc-8e5f-e71992b0b681" />


   **สรุปผลลัพธ์**
   - จากการทดสอบลดทอนจำนวนฟีเจอร์ในโมเดล SVM (Best Model) พบปรากฏการณ์ที่น่าสนใจคือการใช้ Keyword สำคัญเพียง 10 คำแรก (Top-10) ก็สามารถทำค่า F1-score ได้สูงถึง 88.89% ซึ่งเหนือกว่างานวิจัยเดิมที่ใช้ Stylometric features ทั้งหมดเสียอีก และเมื่อขยายขอบเขตเป็น 20 คำ (Top-20) ประสิทธิภาพได้ไต่ระดับไปถึงจุดสูงสุดที่ F1-score 92.86% โดยสามารถจับ Phishing ได้ครบทุกฉบับ (Recall 100%) แต่เมื่อเพิ่มเป็น 30 คำ ผลลัพธ์กลับคงที่ ไม่เกิดการพัฒนาเพิ่มเติม ซึ่งบ่งชี้ว่า **"หัวใจสำคัญ" ของการหลอกลวงซ่อนอยู่ในกลุ่มคำศัพท์เล็กๆ เพียง 20 คำแรกเท่านั้น (เช่น คำสั่งเร่งด่วน หรือคำเกี่ยวกับการเงิน) ส่วนที่เหลือเป็นเพียงส่วนประกอบที่ไม่ส่งผลต่อการตัดสินใจ**



   **ข้อเสนอแนะ**
   - แนวทางพัฒนาต่อในอนาคต (Future Work) แทนที่จะมุ่งเน้นการหา Feature เชิงโครงสร้างที่ซับซ้อน ควรหันมาพิจารณาเทคนิค NLP ขั้นสูง เช่น การใช้ Word Embeddings หรือ Transformer-based models (เช่น BERT) ที่สามารถเข้าใจบริบท และความหมายแฝงของประโยคได้ดียิ่งขึ้น เพื่อดักทาง Phishing ยุคใหม่ที่อาจเปลี่ยนคำศัพท์หลบเลี่ยง Keyword เดิมๆ แต่ยังคงเจตนาหลอกลวงแบบเดิม











