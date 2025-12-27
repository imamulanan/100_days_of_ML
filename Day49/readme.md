# 1. **MAE (Mean Absolute Error)**

👉 Formula:

$$
MAE = \frac{1}{n}\sum_{i=1}^{n} |y_i - \hat{y_i}|
$$

* এখানে $y_i$ = আসল মান (actual value)
* $\hat{y_i}$ = মডেলের predict করা মান (predicted value)
* $| \cdot |$ = absolute value (চিহ্ন বাদ দিয়ে শুধু দূরত্ব ধরা)

🔹 **বোঝায়:** prediction কতটা **average দূরত্বে ভুল করেছে**, দিক (positive/negative) ধরা হয় না।

---

# 2. **MSE (Mean Squared Error)**

👉 Formula:

$$
MSE = \frac{1}{n}\sum_{i=1}^{n} (y_i - \hat{y_i})^2
$$

* এখানে error (ভুল) কে **square** করা হয়।

🔹 **বোঝায়:** average squared error।
🔹 বড় error গুলোকে বেশি গুরুত্ব দেয় (কারণ square করার ফলে error বড় হয়ে যায়)।

---

# 3. **RMSE (Root Mean Squared Error)**

👉 Formula:

$$
RMSE = \sqrt{MSE} = \sqrt{\frac{1}{n}\sum_{i=1}^{n} (y_i - \hat{y_i})^2}
$$

* MSE এর square root।

🔹 **বোঝায়:** error এর **আসল scale** এ ফিরিয়ে আনে (কারণ MSE তে square হয়ে যায়, তাই আসল unit থাকে না)।
🔹 MAE এর চেয়ে **বড় error বেশি শাস্তি (penalize)** দেয়।

---

### **Comparison (সহজভাবে):**

* **MAE** → গড় ভুলের পরিমাণ, সব ভুলকে সমানভাবে দেখে।
* **MSE** → গড় ভুলের বর্গ, বড় ভুলকে বেশি গুরুত্ব দেয়।
* **RMSE** → MSE এর root, আসল data scale এ error বোঝায় এবং বড় ভুলকেও বেশি শাস্তি দেয়।



# **$R^2$ score** বা **Coefficient of Determination** হলো regression model-এর একটি **goodness of fit** মাপার পদ্ধতি।

---

## 📌 Definition:

$$
R^2 = 1 - \frac{SS_{res}}{SS_{tot}}
$$

যেখানে,

* $SS_{res} = \sum (y_i - \hat{y_i})^2$ → **Residual Sum of Squares** (prediction error এর বর্গের যোগফল)
* $SS_{tot} = \sum (y_i - \bar{y})^2$ → **Total Sum of Squares** (data কতটা গড় থেকে বিচ্যুত)
* $y_i$ = আসল মান
* $\hat{y_i}$ = predict করা মান
* $\bar{y}$ = আসল মানের গড়

---

## 📌 Interpretations:

* **$R^2 = 1$** → Model পুরোপুরি perfect fit (সব prediction আসল মানের সাথে মিলে গেছে)।
* **$R^2 = 0$** → Model গড় মান ($\bar{y}$) predict করার চেয়ে ভালো কিছু করছে না।
* **$R^2 < 0$** → Model আসলে গড় মান predict করার থেকেও খারাপ।

---

## 📌 সহজ ভাষায়:

👉 $R^2$ basically বলে দেয় **model data এর variation এর কত শতাংশ explain করতে পারছে**।

যেমন:

* $R^2 = 0.85$ হলে → Model data এর 85% variation ধরতে পারছে।
* $R^2 = 0.30$ হলে → Model মাত্র 30% variation ধরতে পারছে।

---
# **Adjusted R²**
আমরা জানি **R² score** শুধু বলে কতটা variation model ধরতে পারছে। কিন্তু সমস্যা হলো—
👉 যখন তুমি model-এ নতুন নতুন feature (independent variable) যোগ করো, তখন R² **কখনো কমে না** (হয় একই থাকে, নয়তো বেড়ে যায়), এমনকি সেই feature যদি আসলে কাজে না লাগে!

এই সমস্যা দূর করার জন্য এসেছে **Adjusted R²**।

---

## 📌 Formula:

$$
Adjusted\ R^2 = 1 - \Bigg( \frac{(1 - R^2)(n - 1)}{n - p - 1} \Bigg)
$$

যেখানে,

* $n$ = data point সংখ্যা
* $p$ = independent variable (feature) সংখ্যা
* $R^2$ = সাধারণ R² score

---

## 📌 Key Difference:

* **R²:** শুধু model-এর fit মাপে, feature বাড়ালেই বেড়ে যায়।
* **Adjusted R²:** feature এর সংখ্যা অনুযায়ী R² কে adjust করে।

---

## 📌 Interpretations:

* যদি নতুন feature model-কে **উন্নত করে**, তাহলে Adjusted R² বাড়বে।
* যদি feature **অপ্রয়োজনীয় হয়**, তাহলে Adjusted R² **কমে যাবে**।
* তাই model-এ feature selection এর ক্ষেত্রে Adjusted R² বেশি নির্ভরযোগ্য।

---

## 📌 সহজ উদাহরণ:

ধরো, তুমি একটা model বানালে যেখানে R² = 0.80।

* যদি নতুন feature যোগ করার পর R² = 0.82 হয়, কিন্তু Adjusted R² = 0.79 → বুঝতে হবে feature আসলে তেমন কাজে লাগেনি।
* কিন্তু যদি Adjusted R² = 0.81 হয় → বুঝতে হবে feature সত্যিই কাজে লেগেছে।

---

👉 তাহলে বলা যায়:

* **R²** = শুধু fit এর মাপ।
* **Adjusted R²** = fit + feature efficiency (অপ্রয়োজনীয় feature বাদ দিয়ে বিচার করে)।

---
