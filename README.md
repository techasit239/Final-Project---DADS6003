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

เราได้ออกแบบการทดลองออกเป็นทั้งหมด **5 รูปแบบ** โดยแบ่งเป็นกลุ่ม **Reproduce** (ทำซ้ำงานวิจัยเดิม) และกลุ่ม **New Ideas** (แนวคิดใหม่) เพื่อเปรียบเทียบประสิทธิภาพตั้งแต่ระดับพื้นฐาน (Baseline) ไปจนถึงระดับผสมผสาน (Hybrid) ดังนี้

#### 1. รายละเอียดรูปแบบการทดลอง (Overview)

| การทดลอง (Experiment) | รายละเอียด (Description) | Features ที่ใช้ | Models |
| :--- | :--- | :--- | :--- |
| **1. 🔁 Reproduce (Untuned)** | **Baseline:** จำลองตาม Paper 100% <br>*(ไม่จูน Hyperparameter, ไม่ตัด Feature)* | **Raw Stylometric** <br>*(~60 features)* | 4 Models <br>*(ตาม Paper)* |
| **2. 💡 Reproduce (Tuned)** | **Optimized:** ปรับปรุง Baseline <br>*(จูนด้วย Optuna + ตัด Feature ซ้ำซ้อน)* | **Filtered Stylometric** <br>*(ตัด High Correlation)* | 9 Models |
| **3. 💡 Experiment A** | **Behavioral (New Idea):** <br>เพิ่มฟีเจอร์จับพฤติกรรม/เจตนาหลอกลวง | **Stylometric + 8 Advanced** | 9 Models |
| **4. 💡 Experiment B** | **Content-based (New Idea):** <br>ใช้ NLP (TF-IDF) จับ Keywords สำคัญ | **TF-IDF Only** <br>*(Max 300 features)* | 9 Models |
| **5. 💡 Experiment C** | **Hybrid (New Idea):** <br>รวมทุกเทคนิคเข้าด้วยกัน | **Stylo + Advanced + TF-IDF** | 9 Models |

---

#### 2. เปรียบเทียบองค์ประกอบทางเทคนิค (Technical Matrix)

ตารางเช็คลิสต์แสดงเทคนิคและฟีเจอร์ที่เปิดใช้งานในแต่ละการทดลอง

| การทดลอง (Experiment) | Tuning Model | Feature Selection | Stylometric Features | Advanced Features | TF-IDF |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **1. 🔁 Reproduce (Untuned)** | | | ✅ | | |
| **2. 💡 Reproduce (Tuned)** | ✅ | ✅ | ✅ | | |
| **3. 💡 Experiment A** | ✅ | ✅ | ✅ | ✅ | |
| **4. 💡 Experiment B** | ✅ | ✅ | | | ✅ |
| **5. 💡 Experiment C** | ✅ | ✅ | ✅ | ✅ | ✅ |

> **คำอธิบายเพิ่มเติม:**
> * **Tuning Model:** การใช้ `Optuna` เพื่อค้นหาค่า Hyperparameter ที่ดีที่สุด (20 Trials)
> * **Feature Selection:** การตัดฟีเจอร์ที่ซ้ำซ้อนกันสูง (Correlation > 0.95)
> * **Models:**
>   * *4 Models:* Logistic, SVM, RandomForest, XGBoost
>   * *9 Models:* เพิ่ม AdaBoost, CatBoost, LightGBM, NaiveBayes, DecisionTree


---

### 🛠️ Project Workflow

แผนภาพด้านล่างแสดงขั้นตอนการทำงาน (Pipeline) ตั้งแต่การเตรียมข้อมูล, การสร้าง Features ทั้ง 5 กลุ่ม, การแยกสายการทดลอง, ไปจนถึงการจูนโมเดลและการประเมินผลลัพธ์สุดท้าย

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

    subgraph Modeling ["🏋️‍♂️ Training & Tuning Model"]
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

<img width="690" height="296" alt="{1B3799F4-8DA9-4AF2-B226-A3CC5F476399}" src="https://github.com/user-attachments/assets/df7345fd-11c9-474d-9e4b-a27d74938a04" />






<img width="484" height="442" alt="image" src="https://github.com/user-attachments/assets/65ea2bfd-a9ca-4291-89ca-778b55d3c300" />






<img width="570" height="160" alt="{F0ACF7C7-7B92-4143-B8E9-6480C5878E46}" src="https://github.com/user-attachments/assets/cb870467-abe5-4717-9759-1ebed03bb5ad" />


<img width="570" height="160" alt="{7A003D1B-E0ED-4C1B-95AE-B887AA152DE2}" src="https://github.com/user-attachments/assets/a52d8cfa-4745-4ebc-9c70-e8fc997d893a" />


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

   * การที่ **CatBoost** (Gradient Boosting) สามารถแซงหน้า Random Forest (Bagging) ในรอบนี้ได้ แสดงให้เห็นถึงพลังของ **Hyperparameter Tuning** ที่ช่วยให้โมเดลเรียนรู้จากข้อผิดพลาดเดิมซ้ำๆ (Sequential Learning) จนสามารถเพิ่มประสิทธิภาพเฉลี่ยในการจับ พวก Phishing email ได้ดีขึ้น (F1-score) และกวาด (Recall) ได้มากขึ้นเป็น **88.00%** และ **84.62%** ตามลำดับ (จากเดิมที่ RamdomForrest F1 83.33% และ Recall 76.92%) ซึ่ง CatBoost มีจุดเด่นเรื่อง **Ordered Boosting** ที่ช่วยลดปัญหา Overfitting ได้ดีกว่าโมเดล Boosting อื่นๆ เมื่อได้รับการปรับจูนอย่างเหมาะสม จึงสามารถรีดประสิทธิภาพจาก Stylometric Features ได้สูงสุด


# Experiment A : Stylometric + 8 Advanced Features


<img width="800" height="600" alt="{0ADFD18D-8229-4534-A2A6-F4E1D90FBBB9}" src="https://github.com/user-attachments/assets/2aa9f069-b055-4fea-9d79-95fa4999d585" />

_ตารางที่ 8 ผลลัพธ์การ Reproduce และเพิ่ม 8 Advanced Features_  


<img width="312" height="405" alt="{8C9FA559-F76B-4E27-BB0B-3B8192B7DF83}" src="https://github.com/user-attachments/assets/72595496-52d5-4652-85ac-3ed2f9d5b92d" />

_ตารางที่ 9 Confusion matrix ของการทำ Reproduce และเพิ่ม 8 Advanced Features_  


<img width="994" height="590" alt="image" src="https://github.com/user-attachments/assets/9331f5fe-b6d1-46b0-b527-92cbd3771a46" />

_แผนภูมิที่ 2 Top 10 feature ที่มีอิทธิพลต่อ Model XGBoost (รวม Advanced Features)_   


### 💡 3. Experiment A (Behavioral Features)
> **New Idea:** การทดสอบโดยนำ Stylometric Features เดิมมาผสมผสานกับ **8 Advanced Features** (พฤติกรรมการหลอกลวง) พร้อมทั้งทำการคัดเลือกฟีเจอร์ (Feature Selection) และปรับจูนโมเดล (Tuning)

จากการทดลองพบว่าโมเดล **Random Forest** ให้ประสิทธิภาพสูงสุด โดยสามารถทำคะแนนได้เท่ากับแบบ Reproduce tuned (แต่ AUC สูงขึ้นเล็กน้อย) ดังนั้นการเพิ่มฟีเจอร์ด้านพฤติกรรมช่วยให้โมเดลเกิด False alarm ลดลง

* 🏆 **Best Model:** Random Forest
* 🎯 **F1-score:** **88.00%**
* 🎯 **Recall:** **84.62%**
* 🎯 **Precision:** **91.67%**

#### 🔍 Key Insights & Feature Importance
Random Forest ได้เลือกใช้ฟีเจอร์ผสมผสานระหว่าง "สไตล์การเขียน" และ "เจตนาของคนร้าย" ในการจับผิด 3 อันดับแรก:

1.  **`punctuation_frequency` (11.2%)**: ความถี่ของเครื่องหมายวรรคตอนที่ผิดปกติ ยังคงเป็นสัญญาณหลักในการคัดกรองเบื้องต้น
2.  **`first_person_pronoun_count` (8.5%)**: การใช้สรรพนามแทนตัว (I, We) เพื่อสร้างความน่าเชื่อถือหรือแอบอ้างเป็นองค์กร
3.  **`Action_Time_Coercion_Density` (7.4%)**: *[Advanced Feature]* ความหนาแน่นของคำสั่งที่บีบบังคับเรื่องเวลา (เช่น "Click Now", "24 Hours") ซึ่งเป็นฟีเจอร์ใหม่ที่ช่วยจับ "เจตนาเร่งรัด" ของคนร้ายได้สำเร็จ

**สรุปและวิเคราะห์ผล:**
   * จากผลถึงแม้ว่าค่า F1-score, Recall และ Precision (88.00%, 84.62% และ 91.67% ตามลำดับ) จะเท่ากับในการทดลองที่แล้วที่ไม่ได้ใส่ Advanced featured เข้าไป แต่ผู้ชนะกลับเปลี่ยนมือเป็น **Random Forest** (Bagging) แทนที่ **CatBoost** (Gradient Boosting) แต่ค่า AUC 96.45% มีค่าที่มากขึ้นเล็กน้อยจากการทดลองที่แล้ว (95.86%) รวมถึงตัว Advanced feature ที่เราใส่เข้าไป คือ **`Action_Time_Coercion_Density`** ขึ้นมาติดอันดับ Top 3 จึงทำให้สามารถสรุปได้ 2 อย่างคือการใส่ Advanced featured เข้าไปทำให้ไปช่วย**ลด False alarm (TPR) ลง** และ Advanced Feature ใหม่ที่ใส่เข้าไปทำให้การแยกทำได้ชัดเจนยิ่งขึ้น โดย**ไม่ต้องไปใช้โมเดลที่ซับซ้อนแบบประเภท Boosting ก็สามารถแยกแยะ Phishing email ได้ประสิทธิภาพเท่าเดิม**



# Experiment B : TF-IDF only


<img width="800" height="600" alt="{20DDDA85-3491-47A8-BA81-3E69786B0FE0}" src="https://github.com/user-attachments/assets/af79664c-eeea-48bd-9e43-b95ec5d1ebf2" />

_ตารางที่ 10 ผลลัพธ์การ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF_   

<img width="249" height="333" alt="{86F3E982-7422-4A87-9AA3-73BB1915FA2E}" src="https://github.com/user-attachments/assets/c03e279e-bfeb-4350-b501-f8a4b20ca235" />

_ตารางที่ 11 Confusion matrix ของการทำ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF_  

<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/7e9a24b9-d6bf-4a6e-8785-c434fb3341be" />

_แผนภูมิที่ 3 Top 10 feature ที่มีอิทธิพลต่อ Model SVM (รวมตัวแปรจากการทำ TF-IDF)_  

### 📝 4. Experiment B (Content-based Features)
> **New Idea:** การทดสอบโดยเปลี่ยนแนวทางมาใช้เทคนิค **Natural Language Processing (NLP)** ด้วยการสกัดคำศัพท์สำคัญแบบ **TF-IDF** (Term Frequency-Inverse Document Frequency) เพื่อวิเคราะห์เนื้อหา (Content) ภายในอีเมลแทนการดูสไตล์

จากการทดลองพบว่าเกิดจุดเปลี่ยนสำคัญ เมื่อโมเดล **SVM (Support Vector Machine)** พลิกกลับมาเป็นผู้ชนะขาดลอย โดยสามารถทำคะแนนได้สมบูรณ์แบบ (**Perfect Score**) ในทุกมิติ ซึ่งพิสูจน์แล้วว่าสำหรับชุดข้อมูลนี้ "เนื้อหา" คือกุญแจสำคัญที่สุดในการจับผิด

* 🏆 **Best Model:** SVM
* 🎯 **F1-score:** **100.00%**
* 🎯 **Recall:** **100.00%**
* 🎯 **Precision:** **100.00%**

#### 🔍 Key Insights & Feature Importance
SVM สามารถขีดเส้นแบ่ง (Hyperplane) ระหว่างอีเมลดีและร้ายได้อย่างเด็ดขาด โดยอาศัย Keyword สำคัญ 3 อันดับแรก:

1.  **`organization` (1.9%)**: คำศัพท์ทั่วไปที่ดูเป็นทางการ แต่มักถูกใช้ใน Phishing Template เพื่ออ้างถึงหน่วยงานโดยไม่ระบุชื่อ
2.  **`xyz` (1.5%)**: คำศัพท์เฉพาะหรือส่วนประกอบของโดเมนที่ผิดปกติ ซึ่งเป็น "Indicator of Compromise" ที่ชัดเจนมากในชุดข้อมูลนี้
3.  **`management` (1.2%)**: การอ้างถึงฝ่ายบริหารเพื่อสร้างอำนาจ (Authority) กดดันให้เหยื่อปฏิบัติตาม

**สรุปและวิเคราะห์ผล:**
* การที่ **SVM (Support Vector Machine)** สามารถทำคะแนนได้สมบูรณ์แบบ **(Perfect Score 100%)** ในทุกมิติทั้ง **Accuracy, F1-score และ Recall** ในการทดลองนี้ ถือเป็นจุดเปลี่ยนสำคัญที่ชี้ให้เห็นว่าลักษณะของข้อมูลแบบ **TF-IDF** ซึ่งเป็น **High-dimensional Sparse Data** นั้นเข้าทางกับกลไกของ SVM ที่เก่งในการขีดเส้นแบ่งข้อมูล (Hyperplane) ในมิติที่สูงได้แบบแยกออกจากกันชัดเจน (Linear Separability) โดยสามารถแยกแยะ Keyword สำคัญของ Phishing (เช่น organization, xyz) ออกจากอีเมลปกติได้ชัดเจนกว่าโมเดลที่มีความซับซ้อนสูงอย่าง Gradient Boosting (เช่น XGBoost, LightGBM) ที่ประสิทธิภาพตกลงอย่างเห็นได้ชัดในรอบนี้ (F1 เหลือเพียง ~72-75%) เนื่องจากโมเดลกลุ่ม Tree-based มักจะมีข้อจำกัดในการจัดการกับข้อมูล Sparse ที่มีฟีเจอร์จำนวนมากแต่มีจำนวนตัวอย่างน้อย (Small Data) จึงสรุปได้ว่าสำหรับโจทย์นี้ การวิเคราะห์ที่ "เนื้อหา" (Content-based) ด้วยโมเดลเชิงเส้นให้ผลลัพธ์ที่แม่นยำและเสถียรที่สุด

# Experiment C : Hybrid >> [Stylometric + 8 Advanced Features] + [TF-IDF]


<img width="800" height="600" alt="{E8055934-C81C-4840-9A7E-2AFA786C60B9}" src="https://github.com/user-attachments/assets/1cf2cd51-2a32-4ad2-807d-017941591c5a" />

_ตารางที่ 12 ผลลัพธ์การ Reproduce และเพิ่มตัวแปรจากวิธีการ TF-IDF และ 8 Advance Feature_  


<img width="284" height="365" alt="{6150D481-7F67-4C24-BC15-B143676ED699}" src="https://github.com/user-attachments/assets/80147d96-5d2e-4aed-85a7-332264a0babd" />

_ตารางที่ 13 Confusion matrix และเพิ่มตัวแปรจากวิธีการ TF-IDF และ 8 Advance Feature_  


<img width="994" height="590" alt="image" src="https://github.com/user-attachments/assets/19203b84-ab16-4cb1-bb91-7256bc6bab60" />

_แผนภูมิที่ 4 Top 10 feature ที่มีอิทธิพลต่อ Model Random Forest (รวมตัวแปรจากการทำ TF-IDF และ 8 Advance Feature)_  


### 🧬 5. Experiment C (Hybrid Features)
> **New Idea:** การทดสอบแบบ "รวมทุกอย่าง" โดยนำฟีเจอร์ทุกประเภทมารวมกัน (Stylometric + Advanced + TF-IDF) เพื่อดูว่าการใช้ข้อมูลทุกมิติจะช่วยให้โมเดลเก่งขึ้นหรือไม่

จากการทดลองพบว่าโมเดล **Random Forest** กลับมาครองแชมป์อีกครั้ง โดยทำคะแนนได้สูงถึง **92.31%** ในทุกมิติ (Precision, Recall, F1) ซึ่งสูงกว่าการใช้ Stylometric เพียงอย่างเดียว แต่ยังเป็นรอง Experiment B (TF-IDF only) เล็กน้อย

* 🏆 **Best Model:** Random Forest
* 🎯 **F1-score:** **92.31%**
* 🎯 **Recall:** **92.31%**
* 🎯 **Precision:** **92.31%**

#### 🔍 Key Insights & Feature Importance
Random Forest แสดงความสามารถในการ "คัดเลือกสิ่งที่ดีที่สุด และ เสถียรที่สุด" จากทั้งสองรูปแบบของ Feature (Style + Content) โดย Top 3 Features มาจากคนละกลุ่มกันอย่างชัดเจน:

1.  **`punctuation_frequency` (5.8%)**: *[Stylometric]* ความผิดปกติของการใช้เครื่องหมายวรรคตอน ยังคงเป็นFeatureที่ใช้จับได้มากที่สุด
2.  **`organization` (5.7%)**: *[TF-IDF]* คำศัพท์ที่บ่งบอกถึงการแอบอ้างองค์กร
3.  **`first_person_pronoun_count` (4.0%)**: *[Stylometric]* การใช้สรรพนามแทนตัวเองเพื่อสร้างเรื่องราว

**สรุปและวิเคราะห์ผล:**
   * ใน Experiment B (TF-IDF ล้วน) ข้อมูลเป็น Text ที่กระจายตัว (Sparse) ซึ่งเข้าทาง **SVM** ที่สุด แต่ใน Experiment C เราได้นำข้อมูลสถิติ (Stylometric/Advanced) ที่เป็นตัวเลขทึบ (Dense) มาผสมกับ Text ทำให้ข้อมูลมีความ **ผสมผสาน (Mixed Data Types)** และมีความซับซ้อนสูงขึ้น และ การผสมฟีเจอร์หลายๆแบบในชุดข้อมูลขนาดเล็ก (Small Data) ทำให้เกิด Noise และความซับซ้อนที่ทำให้ SVM หรือ Linear Models เริ่ม Sensitive แต่ **Random Forest** มีจุดเด่นเรื่องการจัดการฟีเจอร์ที่หลากหลายและ**ตัด Noise ได้ดีผ่านการทำ Feature Subsampling และ Bagging** จึงสามารถคัดเลือกเฉพาะฟีเจอร์ที่ **เนื้อๆ เน้นๆ** จากทั้งฝั่ง Style และ Content มาใช้ร่วมกันได้ดีที่สุด แม้ประสิทธิภาพรวมจะลดลงจาก Exp B เล็กน้อย (96% -> 92%) เนื่องมาจากปัญหา Curse of Dimensionality (ฟีเจอร์เยอะเกินไปเมื่อเทียบกับจำนวนข้อมูล)



# 🏆 Best Experiment & Best Model

<img width="634" height="528" alt="{329DF658-3BF2-4864-94B5-D2C3BC9E4F20}" src="https://github.com/user-attachments/assets/4e9a47e2-4115-43b0-bec0-a870a19a8094" />

   * จากการเปรียบเทียบผลการทดลองทั้ง 5 รูปแบบ (ตั้งแต่การทำซ้ำงานวิจัยเดิม ไปจนถึงการนำเสนอไอเดียใหม่) พบว่าแนวทางการวิเคราะห์ **เนื้อหา (Content-based) หรือ TF-IDF** ใน **Experiment B** ให้ผลลัพธ์ที่ดีที่สุด เมื่อเปรียบเทียบกับการวิเคราะห์ที่**สไตล์การเขียน (Stylometric)** ที่ถูกใส่เข้าไปในการทดลองอื่น

#### 🥇 **Winner: Experiment B (TF-IDF Only)**
* **Model:** **SVM** (C ≈ 56.7)
* **ผลลัพธ์:** ทำคะแนนได้สมบูรณ์แบบ (**F1-score 100%**) บนข้อมูลทดสอบที่ไม่เคยเห็นมาก่อน (Unseen Data)

**สรุปและวิเคราะห์ผล:**
   * สาเหตุที่ **SVM** ชนะขาดลอย และยังสามารถจับ Phishing ได้ครบและถูกต้องทุกเมลในการทดลองนี้ (100%) เป็นเพราะลักษณะของข้อมูล **TF-IDF** นั้นเป็น **High-dimensional Sparse Data** (มิติสูงแต่ข้อมูลกระจายตัว) ซึ่งเป็นทางถนัดของ SVM ที่เก่งในเรื่อง **Linear Separability** ในการขีดเส้นแบ่ง (Hyperplane) ระหว่างคลาสในมิติที่สูงมากๆ ได้อย่างแม่นยำ โดยเฉพาะเมื่อ Keyword (เช่น organization, xyz) เป็นตัวใช้จับได้อย่างชัดเจน (Strong Predictor or Strong X) การใช้โมเดลเส้นตรงที่ที่แยกออกได้ชัดเจนอย่าง SVM จึงให้ผลลัพธ์ดีกว่าโมเดลที่ซับซ้อนอย่างกลุ่ม tree-based model




# 📈 Check Best model overfitting

<img width="691" height="470" alt="image" src="https://github.com/user-attachments/assets/96d1fb81-751a-4a52-8ce4-33cc93b0cc4b" />


   **สรุปผลลัพธ์**
   
   * จากการตรวจสอบกราฟ Learning Curve (Log Loss vs Training Size) ของโมเดล SVM ซึ่งเป็นผู้ชนะใน Experiment B (TF-IDF) พบลักษณะที่บ่งชี้ถึง **Good fitting** (การนำไปใช้จริงได้ดี) อย่างชัดเจน โดยเส้น Training Loss (สีแดง) มีค่าสูงเล็กน้อยในช่วงแรกของการเทรนแล้วจึงลดลงเมื่อจำนวนข้อมูลในการเทรนเพิ่มขึ้นตั้งแต่ ~25 samples ในขณะที่เส้น Validation Loss (สีน้ำเงิน) เริ่มต้นจากจุดที่สูงกว่ามากแต่ลดระดับลงอย่างรวดเร็วและวิ่งเข้าหาเส้น Training Loss จนช่องว่าง (Gap) แคบลงเรื่อยๆ ลักษณะการลู่เข้าหากัน (Convergence) ที่ระดับ Error ต่ำทั้งคู่เช่นนี้ ยืนยันว่าโมเดลไม่ได้เพียงแค่เก่งแต่จำข้อสอบ (Overfitting) แต่สามารถจับ Pattern ของ Keyword สำคัญได้จริง (Good fit) เมื่อต้องเจอกับข้อมูลที่ไม่เคยเห็นมาก่อน (Unseen Data)





# 🫗 Feature selection analysis on [best model from best experiment]

<img width="850" height="276" alt="{7FE8ADF3-E655-418E-8DAB-D757BEE1B2A0}" src="https://github.com/user-attachments/assets/d4bbfea6-7a83-4ed1-9252-9468268f3b05" />


   **สรุปผลลัพธ์**
   * จากการทดสอบ**ลดทอนจำนวนฟีเจอร์ในโมเดล SVM (Best Model)** พบว่าการใช้ Keyword สำคัญ**เพียง 20 คำแรก (Top-20)** ก็สามารถทำค่า **F1-score ได้เต็ม 100%** แล้ว ซึ่งเหนือกว่างานวิจัยเดิมที่ใช้ Stylometric features ทั้งหมด จึงสรุปได้ว่าเราไม่จำเป็นต้องใช้ฟีเจอร์ทั้งหมด 300 ตัว (ตาม max_features ใน TF-IDF ที่ตั้งค่าไว้ 300) แต่เพียงแค่ใช้ Top 20 Features ที่คัดมาแล้ว ก็สามารถสร้างระบบตรวจจับ Phishing ที่แม่นยำที่สุด (100%) และทำงานได้รวดเร็วที่สุด (Lightweight Model) ได้แล้ว

   **ข้อเสนอแนะ**
   * แนวทางพัฒนาต่อในอนาคต (Future Work) แทนที่จะมุ่งเน้นการหา Feature เชิงโครงสร้างที่ซับซ้อน ควรหันมาพิจารณาเทคนิค NLP ขั้นสูง เช่น การใช้ Word Embeddings หรือ Transformer-based models (เช่น BERT) ที่สามารถเข้าใจบริบท และความหมายแฝงของประโยคได้ดียิ่งขึ้น เพื่อดักทาง Phishing ยุคใหม่ที่อาจอัพเกรดเปลี่ยนคำศัพท์หลบเลี่ยง Keyword เดิมๆ เป็น Keyword ใหม่ๆ











