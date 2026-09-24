# Gold Volatility Analysis
## Quantitative Analysis Report | گزارش تحلیل کمی


## 1. Introduction | مقدمه
This report presents a quantitative analysis of historical Gold Futures price behavior, volatility, and downside risk.
The analysis uses daily COMEX Gold Futures data obtained through Yahoo Finance with ticker `GC=F`. The sample covers approximately 2010 to 2026 and contains 4,207 daily observations.
The project progresses from descriptive return analysis to volatility modeling using GARCH(1,1), followed by Value at Risk (VaR) and Expected Shortfall (ES) estimation.

این گزارش به بررسی کمی رفتار تاریخی قیمت، نوسان‌پذیری و ریسک نزولی قراردادهای آتی طلا می‌پردازد.
داده‌های مورد استفاده مربوط به قراردادهای آتی طلای COMEX با نماد `GC=F` است که از طریق Yahoo Finance دریافت شده‌اند. دوره مورد بررسی تقریباً از سال 2010 تا 2026 را پوشش می‌دهد و شامل 4,207 مشاهده روزانه است.
روند تحلیل از بررسی توصیفی بازده‌ها شروع شده و سپس به مدل‌سازی نوسان با GARCH(1,1)، محاسبه Value at Risk و در نهایت Expected Shortfall می‌رسد.


=====================================================================================
# 2. Data & Preprocessing | داده و پیش‌پردازش
The raw dataset contains:
* Open
* High
* Low
* Close
* Volume
The dataset was checked for missing values, duplicate dates, invalid prices, and chronological ordering.

The analysis found:
* 4,207 observations
* No missing values in the cleaned price dataset
* No duplicate dates
* No non-positive prices
* Chronological ordering preserved
The cleaned dataset was stored in:
`Data/processed/gold_clean.csv`

داده خام شامل متغیرهای زیر است:
* قیمت باز شدن
* بالاترین قیمت
* پایین‌ترین قیمت
* قیمت پایانی
* حجم معاملات
داده‌ها از نظر مقادیر گمشده، تاریخ‌های تکراری، قیمت‌های نامعتبر و ترتیب زمانی بررسی شدند.

نتایج بررسی:
* 4,207 مشاهده
* بدون مقدار گمشده در داده پاک‌سازی‌شده
* بدون تاریخ تکراری
* بدون قیمت صفر یا منفی
* ترتیب زمانی صحیح
داده پاک‌سازی‌شده در فایل زیر ذخیره شد:
`Data/processed/gold_clean.csv`


=================================================================================================
# 3. Return Analysis | تحلیل بازده

## 3.1 Daily and Log Returns | بازده روزانه و لگاریتمی
Two return measures were calculated:
* Simple Daily Return
* Log Return
The mean daily log return was approximately:
**0.0321%**
The standard deviation of log returns was approximately:
**1.0875%**
The return distribution showed negative skewness and substantial excess kurtosis.
For log returns:
* Skewness ≈ **-0.742**
* Excess Kurtosis ≈ **7.551**
These characteristics indicate that the observed return distribution was not well represented by a simple Normal distribution, particularly in its tails.

دو نوع بازده محاسبه شد:
* بازده ساده روزانه
* بازده لگاریتمی
میانگین بازده لگاریتمی روزانه تقریباً:
**0.0321%**
و انحراف معیار آن تقریباً:
**1.0875%**
بود.
توزیع بازده‌ها دارای چولگی منفی و Kurtosis بالاتر از حالت نرمال بود.
برای Log Return:
* Skewness ≈ **-0.742**
* Excess Kurtosis ≈ **7.551**
این نتایج نشان می‌دهند که توزیع بازده‌های مشاهده‌شده، به‌خصوص در دنباله‌ها، با یک توزیع نرمال ساده به‌خوبی توصیف نمی‌شود.


============================================================================================
# 4. Volatility Analysis | تحلیل نوسان‌پذیری
The estimated historical daily volatility was:
**1.0838%**
Using 252 trading days, annualized volatility was estimated at:
**17.2046%**
Rolling volatility measures were also calculated using 7-day and 30-day windows.
The 30-day annualized rolling volatility reached a maximum of approximately:
**47.54%**
The variation in rolling volatility indicates that market risk was not constant throughout the sample.
Periods of relatively calm market conditions were followed by periods of substantially higher volatility.


نوسان‌پذیری تاریخی روزانه برابر با:
**1.0838%**
برآورد شد.
با فرض 252 روز معاملاتی، نوسان‌پذیری سالانه‌شده تقریباً:
**17.2046%**
بود.
همچنین نوسان‌پذیری Rolling برای پنجره‌های 7 و 30 روزه محاسبه شد.
حداکثر نوسان‌پذیری سالانه‌شده 30 روزه تقریباً:
**47.54%**
به دست آمد.
تغییرات قابل توجه Rolling Volatility نشان می‌دهد که ریسک بازار در طول دوره ثابت نبوده است.
دوره‌های آرام‌تر با دوره‌هایی از افزایش قابل توجه نوسان‌پذیری همراه بوده‌اند.


===========================================================================================
# 5. GARCH Modeling | مدل‌سازی GARCH

## 5.1 Normal GARCH(1,1)
A GARCH(1,1) model with Normally distributed innovations was initially fitted to logarithmic returns.
The estimated persistence was:
**α + β ≈ 0.985**
This indicates a high degree of persistence in conditional volatility.
The model also reduced the remaining autocorrelation in squared standardized residuals, suggesting that the GARCH structure captured a substantial portion of the volatility dependence in the sample.

ابتدا یک مدل GARCH(1,1) با فرض توزیع نرمال برای نوآوری‌ها روی بازده لگاریتمی برازش داده شد.
میزان Persistence مدل برابر با:
**α + β ≈ 0.985**
به دست آمد.
این مقدار نشان‌دهنده Persistence بالای نوسان‌پذیری شرطی در نمونه مورد بررسی است.
همچنین بررسی Residualهای استانداردشده نشان داد که وابستگی موجود در مربع Residualها تا حد زیادی توسط ساختار GARCH توضیح داده شده است.


=============================================================================================
# 6. Student-t GARCH Model | مدل GARCH با توزیع Student-t
Because the return distribution exhibited heavy tails, a Student-t GARCH(1,1) specification was also estimated.
The Student-t model produced:
* Log-Likelihood ≈ **-5794.55**
* AIC ≈ **11599.10**
* BIC ≈ **11630.82**
* α ≈ **0.0354**
* β ≈ **0.9581**
* Persistence ≈ **0.9935**
* Degrees of Freedom ≈ **4.23**
Compared with the Normal specification, the Student-t model produced a higher log-likelihood and lower AIC and BIC.
Therefore, the Student-t GARCH model was selected as the primary volatility model for the subsequent risk analysis.
The estimated degrees of freedom are also consistent with the heavy-tailed behavior observed during the return-distribution analysis.


با توجه به وجود دنباله‌های سنگین در توزیع بازده‌ها، مدل GARCH(1,1) با توزیع Student-t نیز برازش داده شد.
نتایج مدل:
* Log-Likelihood ≈ **-5794.55**
* AIC ≈ **11599.10**
* BIC ≈ **11630.82**
* α ≈ **0.0354**
* β ≈ **0.9581**
* Persistence ≈ **0.9935**
* Degrees of Freedom ≈ **4.23**
در مقایسه با مدل نرمال، مدل Student-t دارای Log-Likelihood بالاتر و مقادیر AIC و BIC پایین‌تری بود.
بنابراین مدل Student-t GARCH به عنوان مدل اصلی نوسان‌پذیری برای تحلیل ریسک انتخاب شد.
همچنین مقدار Degrees of Freedom حدود 4.23 با وجود رفتار Heavy-Tailed مشاهده‌شده در تحلیل بازده‌ها سازگار است.


===============================================================================================
# 7. Value at Risk | ارزش در معرض ریسک
Historical VaR was calculated at 95% and 99% confidence levels.
The results were:

| Measure        |     95% |     99% |
| -------------- | ------: | ------: |
| Historical VaR | 1.7138% | 3.0673% |

At the 95% level, the estimated historical daily loss threshold was approximately 1.71%.
At the 99% level, the threshold increased to approximately 3.07%.
These are historical sample estimates and should not be interpreted as guaranteed future loss limits.


Historical VaR در سطوح اطمینان 95 و 99 درصد محاسبه شد.
نتایج:

| معیار          |     95% |     99% |
| -------------- | ------: | ------: |
| Historical VaR | 1.7138% | 3.0673% |

در سطح اطمینان 95 درصد، آستانه زیان روزانه تاریخی تقریباً 1.71 درصد بود.
در سطح 99 درصد، این مقدار به حدود 3.07 درصد افزایش یافت.
این اعداد بر اساس نمونه تاریخی محاسبه شده‌اند و نباید به عنوان حد قطعی زیان آینده در نظر گرفته شوند.


=================================================================================================
# 8. GARCH-Based VaR | VaR مبتنی بر GARCH
Unlike historical VaR, which provides a fixed threshold, GARCH-based VaR is conditional and changes over time according to estimated volatility.
Using the Student-t GARCH model, the average estimated VaR was:

| Measure           |     95% |     99% |
| ----------------- | ------: | ------: |
| Average GARCH VaR | 1.6247% | 2.8144% |

The maximum estimated GARCH VaR reached approximately:
* 95%: **4.2917%**
* 99%: **7.4344%**
This illustrates how conditional risk can increase substantially during high-volatility periods.


برخلاف Historical VaR که یک آستانه نسبتاً ثابت بر اساس توزیع تاریخی بازده‌ها ارائه می‌کند، GARCH-based VaR به‌صورت شرطی و پویا تغییر می‌کند.
با استفاده از مدل Student-t GARCH، میانگین VaR برآوردشده برابر بود با:

| معیار             |     95% |     99% |
| ----------------- | ------: | ------: |
| Average GARCH VaR | 1.6247% | 2.8144% |

حداکثر VaR برآوردشده توسط مدل GARCH تقریباً به مقادیر زیر رسید:
* 95%: **4.2917%**
* 99%: **7.4344%**
این موضوع نشان می‌دهد که در دوره‌های افزایش نوسان، ریسک شرطی می‌تواند به شکل قابل توجهی افزایش پیدا کند.


==================================================================================================
# 9. Expected Shortfall | زیان مورد انتظار
Expected Shortfall extends VaR by measuring the average loss beyond the VaR threshold.
Historical ES estimates were:

| Measure       |     95% |     99% |
| ------------- | ------: | ------: |
| Historical ES | 2.6290% | 4.3533% |

The GARCH-based average ES estimates were:

| Measure          |     95% |     99% |
| ---------------- | ------: | ------: |
| Average GARCH ES | 2.4083% | 3.8630% |

The difference between VaR and ES demonstrates that identifying a loss threshold alone is not sufficient for understanding extreme downside risk.


Expected Shortfall با بررسی میانگین زیان‌هایی که از آستانه VaR عبور می‌کنند، اطلاعات بیشتری درباره ریسک دنباله توزیع ارائه می‌دهد.
Historical ES:

| معیار         |     95% |     99% |
| ------------- | ------: | ------: |
| Historical ES | 2.6290% | 4.3533% |

میانگین GARCH-based ES:

| معیار            |     95% |     99% |
| ---------------- | ------: | ------: |
| Average GARCH ES | 2.4083% | 3.8630% |

تفاوت بین VaR و ES نشان می‌دهد که صرفاً تعیین یک آستانه زیان برای درک ریسک‌های شدید کافی نیست و بررسی شدت زیان‌های فراتر از آن آستانه نیز اهمیت دارد.



==============================================================================================================
# 10. Overall Interpretation | جمع‌بندی کلی
The analysis provides a progression from descriptive financial analysis toward conditional risk modeling.
The return distribution showed negative skewness and heavy tails. Rolling volatility demonstrated that risk varied over time. GARCH modeling then provided a framework for estimating conditional volatility.
The Student-t specification was selected over the Normal specification based on the observed information criteria and likelihood values.
Finally, VaR and Expected Shortfall translated the volatility analysis into interpretable downside-risk measures.
The project therefore demonstrates how historical market data can be transformed into a structured quantitative risk-analysis workflow.


این پروژه یک مسیر مرحله‌به‌مرحله از تحلیل توصیفی بازار تا مدل‌سازی شرطی ریسک ارائه می‌دهد.
توزیع بازده‌ها دارای چولگی منفی و دنباله‌های سنگین بود. تحلیل Rolling Volatility نیز نشان داد که سطح ریسک در طول زمان ثابت نیست. سپس مدل GARCH چارچوبی برای برآورد نوسان‌پذیری شرطی فراهم کرد.
مدل Student-t بر اساس مقایسه Log-Likelihood، AIC و BIC نسبت به مدل نرمال انتخاب شد.
در نهایت، VaR و Expected Shortfall نتایج مدل‌سازی نوسان را به معیارهای قابل تفسیر برای اندازه‌گیری ریسک نزولی تبدیل کردند.
در نتیجه، این پروژه نشان می‌دهد که چگونه می‌توان داده‌های تاریخی بازار را به یک فرآیند ساختاریافته برای تحلیل کمی ریسک تبدیل کرد.

---
==============================================================================================================
# 11. Limitations | محدودیت‌ها
Several limitations should be considered:
* The analysis uses historical Gold Futures data.
* Historical behavior does not guarantee future behavior.
* VaR and ES depend on the selected methodology and model assumptions.
* GARCH captures conditional volatility but does not explain every source of market risk.
* Model risk remains present even when the Student-t specification is used.
* Transaction costs, liquidity constraints, portfolio interactions, and macroeconomic variables are outside the scope of this project.


محدودیت‌های اصلی پروژه عبارت‌اند از:

* تحلیل بر اساس داده‌های تاریخی Gold Futures انجام شده است.
* رفتار گذشته تضمینی برای رفتار آینده نیست.
* VaR و ES به روش محاسبه و فرضیات مدل وابسته هستند.
* GARCH نوسان‌پذیری شرطی را مدل می‌کند اما تمام منابع ریسک بازار را توضیح نمی‌دهد.
* حتی با استفاده از Student-t، ریسک مدل همچنان وجود دارد.
* هزینه معاملات، محدودیت نقدشوندگی، تعامل با سایر دارایی‌های پرتفوی و متغیرهای اقتصاد کلان در این پروژه بررسی نشده‌اند.


==============================================================================================================
# 12. Conclusion | نتیجه‌گیری
This project developed a complete quantitative workflow for analyzing gold market volatility and downside risk.
The workflow progressed through:
**Market Data → Returns → Volatility → GARCH → VaR → Expected Shortfall**
The results provide a foundation for extending the analysis toward multi-asset risk modeling, portfolio diversification, and quantitative financial dashboards.


در این پروژه یک Workflow کامل برای تحلیل کمی نوسان‌پذیری و ریسک نزولی بازار طلا ایجاد شد.
مسیر اصلی پروژه به شکل زیر بود:
**داده بازار → بازده → نوسان‌پذیری → GARCH → VaR → Expected Shortfall**
این نتایج می‌توانند پایه‌ای برای توسعه تحلیل به سمت مدل‌سازی ریسک چنددارایی، بررسی Diversification پرتفوی و ساخت داشبوردهای مالی کمی باشند.
