# 📘 Studiu de Caz – Regularizare în Modele de Regresie  
**Elastic Net vs. Ridge vs. Lasso**

Acest repository conține notebook-ul **TEMA2.ipynb**, în care este implementat un studiu comparativ al metodelor de regularizare utilizate pentru reducerea overfitting-ului în modelele de regresie.

Scopul proiectului este analiza modului în care tehnicile **L1 (Lasso)**, **L2 (Ridge)** și **Elastic Net** influențează performanța, stabilitatea și generalizarea unui model de regresie aplicat pe date reale.

---

## 🧠 Conținutul proiectului

Notebook-ul include:

### ✔ Pre-procesarea setului de date  
- încărcarea datelor din proiectul Beijing Multi-Site Air Quality  
- curățare și completare valori lipsă  
- transformări pentru variabile numerice și categorice  
- scalare standardizată  
- transformarea logaritmică a variabilei țintă (PM2.5)  
- împărțirea datelor Train/Test fără shuffle (date temporale)

### ✔ Implementarea modelelor  
Modelele antrenate în notebook:

- **Linear Regression** (baseline)
- **Ridge Regression (L2)**
- **Lasso Regression (L1)**
- **Elastic Net (L1+L2)**

Optimizarea hiperparametrilor a fost realizată folosind **GridSearchCV**.

### ✔ Evaluare și analiză  
Notebook-ul conține:

- RMSE pe seturile Train și Test  
- R² pentru fiecare model  
- analiza bias–varianță  
- curbe de învățare  
- distribuția predicțiilor (KDE)  
- comparația coeficienților și a coeficienților eliminați  
- interpretare SHAP pentru modelul Elastic Net  

---

## 📊 Rezultate pe scurt

| Model | RMSE Test | Observații |
|------|-----------|------------|
| **Linear Regression** | 0.5047 | Precizie numerică cea mai ridicată, ușor overfitting |
| **Lasso (L1)** | 0.5050 | Elimină 2 variabile, regularizare foarte slabă |
| **Ridge (L2)** | 0.5063 | Cel mai stabil în prezența multicoliniarității |
| **Elastic Net** | 0.5064 | Cel mai bun compromis L1+L2, stabil și robust |

Elastic Net a identificat un **l1_ratio = 0.1**, ceea ce indică un dataset dominat de multicoliniaritate, unde penalizarea L2 este mai potrivită.

---

## ▶️ Rulare notebook

Poți rula notebook-ul în Google Colab încărcând local fișierul **TEMA2.ipynb**.

Datasetul necesită încărcare manuală (nu este inclus în repository).

---

## 📁 Fișiere în acest repository

├── TEMA2.ipynb # Notebook complet cu cod, grafice și analiză
└── README.md # Documentația proiectului


---

## 📚 Referințe

- Hastie, Tibshirani & Friedman – *The Elements of Statistical Learning*  
- Tibshirani – *Lasso Regression* (1996)  
- Zou & Hastie – *Elastic Net* (2005)  
- scikit-learn documentation  
- SHAP documentation  
- Beijing Air Quality Dataset – Kaggle  

---

## 🏁 Concluzie

Proiectul demonstrează că:

- Regresia liniară oferă cea mai mică eroare numerică,  
- Modelele regularizate sunt mai stabile în situații reale,  
- **Elastic Net** obține cel mai bun compromis între reducerea varianței și păstrarea performanței,  
- Interpretarea SHAP confirmă consistența și relevanța variabilelor.

Acest studiu oferă o analiză completă și reproductibilă a modului în care regularizarea influențează calitatea modelelor de regresie pe date reale.

