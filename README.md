# Market Basket Analysis with Apriori & Association Rules

This project performs **Market Basket Analysis** using the **Apriori algorithm** and **association rule mining** to discover meaningful product relationships from transaction data. It helps identify which items are frequently purchased together and evaluates the strength of these relationships using various metrics.

---

## 📁 Project Overview

This project includes:

* Data cleaning & preparation
* Converting transactional data into a one-hot encoded format suitable for Apriori
* Mining frequent itemsets
* Generating association rules
* Filtering & interpreting the results using metrics such as **support**, **confidence**, **lift**, **leverage**, **conviction**, **Jaccard**, and more.

---

## 📊 Workflow Summary

### **1. Load and clean the dataset**

* Remove missing values
* Filter invalid quantity or price
* Convert invoices into proper transaction records

### **2. Encode data for Apriori**

Use **TransactionEncoder** to transform each transaction into a binary (True/False) matrix instead of OneHotEncoder, because:

* Apriori requires **transactions with multiple items per row**, not single categorical columns
* OneHotEncoder is designed for single categorical features, not item lists
* TransactionEncoder is optimized for market basket structures

### **3. Generate frequent itemsets**

```python
frequent_itemsets = apriori(
    df_encoded, 
    min_support=0.01, 
    use_colnames=True
)
```

### **4. Generate association rules**

```python
rules = association_rules(
    frequent_itemsets, 
    metric="lift", 
    min_threshold=1
)
```

### **5. Interpret the metrics**

Each rule includes:

* **Support** – How common the item combination is
* **Confidence** – Probability of buying consequent given antecedent
* **Lift** – Strength of association; lift > 1 indicates a positive relationship
* **Leverage** – Difference from expected frequency
* **Conviction, Zhang’s metric, Jaccard, Certainty, Kulczynski** – Additional quality measures

Example interpretation:

| Antecedent                      | Consequent                  | Confidence | Lift | Meaning                                                        |
| ------------------------------- | --------------------------- | ---------- | ---- | -------------------------------------------------------------- |
| pack of 72 retrospot cake cases | 60 teatime fairy cake cases | 0.36       | 8.67 | Strongly associated; customers who buy one often buy the other |

---

## 🛠 Technologies Used

* Python
* Pandas
* mlxtend (Apriori & association rules)
* Jupyter Notebook

---

## 📈 Sample Output

Frequent itemsets and association rules are printed in DataFrame tables, including metrics like:

* `support`
* `confidence`
* `lift`
* `conviction`
* `zhangs_metric`
* `jaccard`
* and more

---

