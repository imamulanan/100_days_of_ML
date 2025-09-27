# **Gradient Descent**

Gradient Descent একটা **optimization algorithm** যেটা মূলত Machine Learning এবং Deep Learning এ সবচেয়ে বেশি ব্যবহার করা হয়।

### সহজভাবে বললে:

তুমি যদি একটা function (ধরা যাক cost function বা loss function) কে minimize করতে চাও, তখন Gradient Descent তোমাকে সাহায্য করে ধীরে ধীরে সেই function এর সর্বনিম্ন (minimum) জায়গায় পৌঁছাতে।

---

### কাজ করার ধাপ:

1. **Initial guess**: প্রথমে parameter (θ) এর একটা starting value ধরি।
2. **Gradient বের করা**: Cost function এর slope (derivative) বের করি θ এর respect এ।
3. **Update rule**: θ কে update করি এই formula দিয়ে –

$$
\theta = \theta - \alpha \cdot \frac{\partial J(\theta)}{\partial \theta}
$$

এখানে,

* $\theta$ = parameter
* $J(\theta)$ = cost function
* $\alpha$ = learning rate (step size)

4. **Repeat**: এই process বারবার করলে আমরা cost function এর minimum এর দিকে চলে যাই।

---

### Intuition (উদাহরণ):

ধরো তুমি একটা পাহাড়ের উপরে দাঁড়িয়ে আছো, আর তোমার লক্ষ্য হলো নিচের উপত্যকায় নামা। তুমি চোখ বেঁধে আছো, তাই slope টা অনুভব করে একেক ধাপে নিচের দিকে নামছো। প্রতিবার slope অনুযায়ী ঠিক করছো কতদূর নামবে। এটাই gradient descent।

---

### Gradient Descent এর Types:

1. **Batch Gradient Descent** → সব ডাটা ব্যবহার করে একসাথে update।
2. **Stochastic Gradient Descent (SGD)** → একেকটা ডাটা পয়েন্ট ব্যবহার করে update।
3. **Mini-batch Gradient Descent** → ডাটাকে ছোট ছোট batch করে update।

---



