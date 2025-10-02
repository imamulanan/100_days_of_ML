
---

# Gradient Descent এর তিনটা Flavor: Batch, Stochastic (SGD) এবং Mini-batch

Gradient Descent এর **তিনটা flavor** আছে – **Batch**, **Stochastic (SGD)**, আর **Mini-batch Gradient Descent**।
এগুলো মূলত **কোন data ব্যবহার করে parameter update করা হবে** সেই পার্থক্যের উপর নির্ভর করে।

---

## 1. Batch Gradient Descent

* এখানে **পুরো dataset** (সব training data) একসাথে ব্যবহার করে cost function এর gradient বের করা হয়।
* অর্থাৎ, parameter update করার আগে dataset-এর সবগুলো data point consider করা হয়।

**Update Formula:**

```
θ = θ - α * (1/N) * Σ[∂J(θ; xi, yi) / ∂θ]
```

এখানে:

* N = data point সংখ্যা
* ∂J(θ; xi, yi) = gradient

**Pros:**

* Convergence smooth এবং স্থিতিশীল হয়।
* Convex function হলে global minimum এ পৌঁছাতে পারবে।

**Cons:**

* খুব slow হয়, কারণ প্রতিবার update করতে পুরো dataset scan করতে হয়।
* Memory বেশি লাগে।

👉 ছোট dataset এর জন্য ভালো।

---

## 2. Stochastic Gradient Descent (SGD)

* এখানে **একটা মাত্র data point** দিয়ে gradient বের করে সাথে সাথেই parameter update করা হয়।
* অর্থাৎ, প্রতি step এ dataset থেকে randomly একটা sample নেই → gradient বের করি → update করি।

**Update Formula:**

```
θ = θ - α * ∂J(θ; xi, yi) / ∂θ
```

**Pros:**

* খুব fast, কারণ প্রতিবার একটুখানি data নিয়েই update হয়।
* Large dataset এর জন্য ভালো।
* Local minima থেকে বের হয়ে আসতে সাহায্য করে (noisy path এর কারণে)।

**Cons:**

* Convergence smooth না, zig-zag এর মতো move করে।
* অনেক iteration লাগতে পারে।

👉 বড় dataset বা online learning এর জন্য perfect।

---

## 3. Mini-batch Gradient Descent

* এখানে **dataset কে ছোট ছোট batch এ ভাগ করা হয়** (যেমন batch size = 32, 64, 128)।
* প্রতিবার parameter update করতে ওই batch টুকুই ব্যবহার হয়।

**Update Formula:**

```
θ = θ - α * (1/m) * Σ[∂J(θ; xi, yi) / ∂θ]
```

এখানে:

* m = batch size (ছোট group এর data point সংখ্যা)

**Pros:**

* Batch GD এর মতো stable এবং SGD এর মতো fast → দুটোর মধ্যে balance।
* GPU parallelization করা যায় (deep learning এ কাজে লাগে)।
* Memory usage নিয়ন্ত্রণে থাকে।

**Cons:**

* Batch size সঠিকভাবে না বাছলে efficiency কমে যেতে পারে।

👉 Deep Learning (TensorFlow, PyTorch) এ default হলো Mini-batch Gradient Descent।

---

## Visual Intuition

* **Batch GD** → smooth করে নিচে নামে (stable কিন্তু slow)।
* **SGD** → লাফালাফি করতে করতে নিচে নামে (fast কিন্তু noisy)।
* **Mini-batch GD** → ছোট ছোট ঢেউ খেলানো smooth descent (balance)।

---

## 🔑 Comparison Table

| Method                  | Data Used per Update | Speed       | Convergence Smoothness | Usage                       |
| ----------------------- | -------------------- | ----------- | ---------------------- | --------------------------- |
| **Batch GD**            | পুরো dataset         | Slow        | Very Smooth            | ছোট dataset                 |
| **Stochastic GD (SGD)** | 1 data point         | Fast        | Noisy/Zigzag           | বড় dataset, online learning |
| **Mini-batch GD**       | ছোট subset (batch)   | Medium/Fast | Smooth-ish             | Deep Learning, GPU training |

---

