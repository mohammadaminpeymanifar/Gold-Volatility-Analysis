=====================================  Gold Volatility Analysis  ==================================
================ تحلیل نوسان و ریسک قیمت طلا با رویکرد Quantitative Finance =====================
**Gold Volatility Analysis** is a quantitative finance project focused on analyzing the volatility and downside risk of gold futures using historical market data and statistical modeling.
The project moves from basic return analysis to dynamic volatility modeling and tail-risk measurement, providing a practical workflow for financial risk analysis.
The main objectives of this project are to:
* Analyze historical gold price behavior
* Calculate daily and logarithmic returns
* Measure historical and rolling volatility
* Investigate volatility clustering
* Model time-varying volatility using GARCH
* Compare Normal and Student-t GARCH specifications
* Estimate Value at Risk (VaR)
* Estimate Expected Shortfall (ES)
* Compare historical and model-based risk measures

## Data
Historical data was obtained from **Yahoo Finance** using the ticker:
`GC=F`
This ticker represents **COMEX Gold Futures**.

### Sample Period
* Start: 2010-01-01
* End: 2026
* Observations: 4,207 price observations
* Return observations: 4,206
The dataset contains:
* Open
* High
* Low
* Close
* Volume


## Methodology
The project is organized into six analytical phases.

### Phase 1 — Data Collection
Historical Gold Futures data was downloaded and stored as raw CSV data.

### Phase 2 — Data Cleaning & EDA
The dataset was inspected for:
* Missing values
* Duplicate dates
* Invalid prices
* Chronological ordering
* Descriptive statistics
No missing values or duplicate dates were identified in the cleaned price dataset.

### Phase 3 — Return Analysis
Both simple and logarithmic returns were calculated.
Key characteristics of the return distribution included:
* Mean daily log return: **0.0321%**
* Daily log-return volatility: **1.0875%**
* Negative skewness
* High excess kurtosis
These characteristics indicate the presence of asymmetric and heavy-tailed return behavior in the sample.

### Phase 4 — Volatility Analysis
Historical and rolling volatility measures were calculated.
Key results:
* Daily volatility: **1.0838%**
* Annualized volatility: **17.2046%**
* Mean 30-day annualized volatility: **16.03%**
* Maximum 30-day annualized volatility: **47.54%**
Rolling volatility analysis also illustrates periods of volatility clustering.

### Phase 5 — GARCH Modeling
A GARCH(1,1) model was used to estimate time-varying conditional volatility.
Two specifications were evaluated:
1. GARCH(1,1) with Normal innovations
2. GARCH(1,1) with Student-t innovations
The Student-t specification produced:
* Higher log-likelihood
* Lower AIC
* Lower BIC
and was therefore selected as the primary volatility model for the subsequent risk analysis.
#### Student-t GARCH Results

| Parameter |  Value |
| --------- | -----: |
| μ         | 0.0488 |
| ω         | 0.0097 |
| α₁        | 0.0354 |
| β₁        | 0.9581 |
| α + β     | 0.9935 |
| ν         | 4.2340 |

The high persistence value indicates that volatility shocks in the sample tend to decay gradually.

### Phase 6 — VaR & Expected Shortfall
Historical and GARCH-based risk measures were calculated at the 95% and 99% confidence levels.

| Risk Measure        |     95% |     99% |
| ------------------- | ------: | ------: |
| Historical VaR      | 1.7138% | 3.0673% |
| GARCH VaR — Average | 1.6247% | 2.8144% |
| Historical ES       | 2.6290% | 4.3533% |
| GARCH ES — Average  | 2.4083% | 3.8630% |

Historical VaR represents an empirical loss threshold based on the historical return distribution.
GARCH-based VaR is dynamic and changes according to estimated conditional volatility.
Expected Shortfall goes beyond the VaR threshold and estimates the average severity of losses in the tail.



## Key Findings
The analysis highlights several important characteristics of gold futures returns:
1. Gold returns are not normally distributed in the observed sample.
2. The return distribution exhibits negative skewness and heavy tails.
3. Volatility varies considerably over time.
4. Volatility clustering is present in the return series.
5. A Student-t innovation distribution provides a better fit than the Normal specification among the tested GARCH models.
6. GARCH provides a dynamic framework for estimating conditional volatility and risk.
7. Expected Shortfall provides additional information about the severity of extreme losses beyond the VaR threshold.



## Project Structure
```text
Gold-Volatility-Analysis/
│
├── Data/
│   ├── raw/
│   │   └── gold_price.csv
│   │
│   └── processed/
│       ├── gold_clean.csv
│       ├── gold_returns.csv
│       ├── gold_volatility.csv
│       └── gold_risk_metrics.csv
│
├── notebooks/
│   └── 01_Data_Collection.ipynb
│
├── reports/
│
├── README.md
├── requirements.txt
└── .gitignore
```


## Limitations
This project is an analytical and educational quantitative-finance study.
Important limitations include:
* The analysis is based on historical data.
* Historical risk estimates are not guarantees of future losses.
* GARCH model results depend on model specification and distributional assumptions.
* The dataset represents COMEX Gold Futures rather than physical gold or LBMA spot prices.
* No transaction costs, liquidity constraints, leverage effects, or portfolio interactions are modeled.



## Future Extensions
Potential extensions include:
* Bitcoin vs Gold volatility comparison
* Gold vs S&P 500 risk analysis
* Portfolio diversification analysis
* Multi-asset VaR and Expected Shortfall
* CAPM and Fama-French analysis
* Backtesting VaR forecasts
* Volatility forecasting
* Power BI financial risk dashboard



## Conclusion
This project demonstrates a complete workflow for analyzing financial-market volatility and downside risk, starting from raw market data and progressing through return analysis, volatility estimation, GARCH modeling, VaR, and Expected Shortfall.
The main purpose is not only to calculate financial metrics, but to demonstrate how statistical and quantitative methods can be integrated into a practical financial analytics workflow.
======================================================================================================================================
**Gold Volatility Analysis** یک پروژه در حوزه **Quantitative Finance و Financial Analytics** است که با هدف بررسی نوسان و ریسک نزولی قیمت قراردادهای آتی طلا انجام شده است.
در این پروژه مسیر تحلیل از داده خام بازار آغاز شده و به محاسبه بازده، اندازه‌گیری نوسان، مدل‌سازی نوسان شرطی با GARCH و در نهایت اندازه‌گیری ریسک دنباله‌ای با VaR و Expected Shortfall می‌رسد.


## اهداف پروژه
اهداف اصلی پروژه عبارت‌اند از:
* بررسی رفتار تاریخی قیمت طلا
* محاسبه بازده روزانه و لگاریتمی
* اندازه‌گیری نوسان تاریخی و Rolling Volatility
* بررسی Volatility Clustering
* مدل‌سازی نوسان متغیر با زمان با استفاده از GARCH
* مقایسه GARCH نرمال و Student-t
* محاسبه Value at Risk
* محاسبه Expected Shortfall
* مقایسه روش Historical و GARCH-based Risk Measurement


## داده‌ها
داده‌های تاریخی از **Yahoo Finance** دریافت شده‌اند.
نماد مورد استفاده:
`GC=F`
این نماد مربوط به **قراردادهای آتی طلای COMEX** است.


### دوره داده
* شروع: 2010-01-01
* پایان: 2026
* تعداد مشاهدات قیمت: 4,207
* تعداد مشاهدات بازده: 4,206
متغیرهای اصلی:
* Open
* High
* Low
* Close
* Volume



## مراحل تحلیل
### Phase 1 — جمع‌آوری داده
داده تاریخی Gold Futures دریافت و به‌عنوان داده خام ذخیره شد.

### Phase 2 — پاک‌سازی و EDA
داده‌ها از نظر:
* مقادیر گمشده
* تاریخ‌های تکراری
* قیمت‌های نامعتبر
* ترتیب زمانی
* آمار توصیفی
بررسی شدند.
در دیتاست پاک‌سازی‌شده مقدار گمشده و تاریخ تکراری مشاهده نشد.

### Phase 3 — تحلیل بازده
بازده ساده و Log Return محاسبه شد.
نتایج اصلی:
* میانگین Log Return روزانه: **0.0321%**
* انحراف معیار روزانه Log Return: **1.0875%**
* Skewness منفی
* Excess Kurtosis بالا
این نتایج نشان می‌دهند که توزیع بازده در نمونه مورد بررسی دارای چولگی و دنباله‌های سنگین است.

### Phase 4 — تحلیل نوسان
نوسان روزانه و Rolling Volatility محاسبه شد.
نتایج:
* Daily Volatility: **1.0838%**
* Annualized Volatility: **17.2046%**
* میانگین Annualized 30D Volatility: **16.03%**
* حداکثر Annualized 30D Volatility: **47.54%**

همچنین دوره‌هایی از خوشه‌بندی نوسان مشاهده شد.

### Phase 5 — مدل GARCH
برای مدل‌سازی نوسان متغیر با زمان از GARCH(1,1) استفاده شد.
دو مدل بررسی شدند:
* GARCH(1,1) با توزیع Normal
* GARCH(1,1) با توزیع Student-t
مدل Student-t دارای:
* Log-Likelihood بالاتر
* AIC پایین‌تر
* BIC پایین‌تر

بود و به‌عنوان مدل اصلی برای تحلیل ریسک انتخاب شد.
پارامترهای اصلی مدل Student-t:

| پارامتر |  مقدار |
| ------- | -----: |
| μ       | 0.0488 |
| ω       | 0.0097 |
| α₁      | 0.0354 |
| β₁      | 0.9581 |
| α + β   | 0.9935 |
| ν       | 4.2340 |

مقدار بالای Persistence نشان می‌دهد که شوک‌های نوسان در نمونه مورد بررسی به‌سرعت از بین نمی‌روند.

### Phase 6 — VaR و Expected Shortfall
ریسک نزولی با دو رویکرد Historical و GARCH در سطوح اطمینان 95% و 99% محاسبه شد.

| معیار ریسک        |     95% |     99% |
| ----------------- | ------: | ------: |
| Historical VaR    | 1.7138% | 3.0673% |
| Average GARCH VaR | 1.6247% | 2.8144% |
| Historical ES     | 2.6290% | 4.3533% |
| Average GARCH ES  | 2.4083% | 3.8630% |

VaR یک آستانه برای زیان احتمالی ارائه می‌کند، در حالی که Expected Shortfall شدت متوسط زیان‌هایی را که از این آستانه عبور می‌کنند اندازه‌گیری می‌کند.



## یافته‌های کلیدی
این تحلیل چند ویژگی مهم از رفتار Gold Futures را نشان می‌دهد:
1. بازده‌ها در نمونه مورد بررسی از توزیع نرمال فاصله دارند.
2. توزیع بازده دارای چولگی منفی و دنباله‌های سنگین است.
3. میزان نوسان در طول زمان ثابت نیست.
4. دوره‌های Volatility Clustering مشاهده می‌شود.
5. در میان مدل‌های بررسی‌شده، Student-t GARCH برازش بهتری نسبت به Normal GARCH نشان داد.
6. GARCH امکان اندازه‌گیری پویای نوسان شرطی و ریسک را فراهم می‌کند.
7. Expected Shortfall اطلاعات بیشتری درباره شدت زیان‌های شدید نسبت به VaR ارائه می‌دهد.



## محدودیت‌های پروژه
این پروژه یک مطالعه آموزشی و تحلیلی در حوزه Quantitative Finance است.
محدودیت‌های مهم:
* تحلیل بر اساس داده‌های تاریخی انجام شده است.
* Historical VaR و ES تضمینی برای زیان‌های آینده نیستند.
* نتایج GARCH به مشخصات مدل و فرض توزیع وابسته هستند.
* داده‌ها مربوط به COMEX Gold Futures هستند، نه قیمت Spot یا LBMA Gold.
* هزینه معاملات، نقدشوندگی، اهرم و تعامل طلا با سایر دارایی‌ها در این پروژه مدل‌سازی نشده‌اند.



## توسعه‌های آینده
مراحل قابل توسعه پروژه:
* مقایسه نوسان Bitcoin و Gold
* تحلیل ریسک Gold و S&P 500
* Portfolio Risk & Diversification
* Multi-Asset VaR و Expected Shortfall
* CAPM و Fama-French
* Backtesting مدل VaR
* Volatility Forecasting
* ساخت Financial Risk Dashboard با Power BI



## جمع‌بندی
این پروژه یک Workflow نسبتاً کامل برای تحلیل نوسان و ریسک بازار مالی ارائه می‌کند؛ از **داده خام بازار** شروع شده و به **Return Analysis، Volatility Analysis، GARCH، VaR و Expected Shortfall** می‌رسد.
هدف پروژه صرفاً محاسبه چند شاخص مالی نیست؛ بلکه نمایش نحوه ترکیب **Python، Statistical Modeling و Quantitative Finance** برای ساخت یک فرآیند عملی تحلیل ریسک مالی است.
