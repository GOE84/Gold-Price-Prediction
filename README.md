#  Gold Price Prediction: Statistical vs. Deep Learning Analysis

**Author:** [Your Name]
**Major:** Computer Science & Innovation (CSI), Sripatum University (SPU)
**Project Type:** Time Series Forecasting & Quantitative Finance

---

##  Project Overview
โปรเจคนี้คือการสร้างระบบพยากรณ์ราคาทองคำรายเดือน (Monthly Gold Price) โดยการเปรียบเทียบประสิทธิภาพระหว่างโมเดลสถิติแบบดั้งเดิม (Classical Statistics) และโครงข่ายประสาทเทียม (Deep Learning) เพื่อวิเคราะห์ว่าโมเดลใดสามารถรับมือกับความผันผวนของตลาดในปี 2024-2025 ได้ดีกว่ากัน

##  Tech Stack
* **Platform:** Google Colab
* **Language:** Python 3.x
* **Data Source:** `yfinance` (Yahoo Finance API)
* **Libraries:** * `Pandas`, `NumPy` - Data Manipulation
  * `Matplotlib` - Visualization
  * `pmdarima` - Auto-ARIMA Modeling
  * `TensorFlow/Keras` - LSTM Neural Networks
  * `Scikit-learn` - Data Scaling & Metrics

##  Methodology

### 1. Data Collection & Preprocessing
* ดึงข้อมูล **Gold Futures (GC=F)** ย้อนหลังตั้งแต่ปี 2004 จนถึงปัจจุบัน
* ทำการ **Resampling** จากรายวันเป็นรายเดือน (Monthly Mean) เพื่อลด Noise
* ใช้ **MinMaxScaler** ปรับช่วงข้อมูลเป็น $[0, 1]$ สำหรับโมเดล LSTM

### 2. Modeling Approach

#### **Model A: ARIMA (AutoRegressive Integrated Moving Average)**
* ใช้เทคนิค Grid Search ผ่าน `auto_arima` เพื่อหาค่าพารามิเตอร์ $(p, d, q)$ ที่ดีที่สุด
* **Result:** โมเดลมีความแม่นยำในสภาวะตลาดปกติ แต่ไม่สามารถคาดการณ์ช่วงที่ราคาทะยานขึ้นอย่างรุนแรง (Structural Break) ในปี 2024 ได้

#### **Model B: LSTM (Long Short-Term Memory)**
* ออกแบบ Recurrent Neural Network (RNN) ชนิด LSTM จำนวน 2 ชั้น พร้อม **Dropout Layer** เพื่อป้องกัน Overfitting
* ใช้ **Lookback Window** ขนาด 12 เดือนในการทำนายเดือนถัดไป
* **Result:** โมเดลมีความยืดหยุ่นสูงและพยายามปรับตัวตามแนวโน้มราคาจริงได้ดีกว่า ARIMA

##  Backtesting Comparison
จากการทดสอบแบบ **Train-Test Split** (ข้อมูลล่าสุด 12 เดือน):
* **ARIMA:** ทายผลลัพธ์ค่อนข้างเป็นเส้นตรง (Underestimation)
* **LSTM:** สามารถจำลองความผันผวนได้ดีกว่า แต่อาจมี Time Lag ในช่วงที่ราคาพุ่งทำ New High



##  Future Roadmap
1. **Multivariate Input:** เพิ่มดัชนีค่าเงินดอลลาร์ (DXY Index) และอัตราดอกเบี้ยเป็นฟีเจอร์ช่วยทำนาย
2. **Sentiment Analysis:** นำ AI มาวิเคราะห์ข่าวจากสำนักข่าวการเงินเพื่อประเมินทิศทางตลาด
3. **Portfolio Application:** พัฒนาต่อยอดเป็นเครื่องมือช่วยตัดสินใจสำหรับระบบ Algo Trading

---

> **Note:** โปรเจคนี้เป็นส่วนหนึ่งของการศึกษาด้าน Data Science 
