# 📘 Studiu de Caz – Regularizare în Modele de Regressie  
**Elastic Net vs. Ridge vs. Lasso**  
*(include și experimentul suplimentar cu validare temporală)*

Acest repository conține implementarea unui studiu comparativ al metodelor de regularizare folosite pentru reducerea overfitting-ului în modelele de regresie, aplicate pe date reale din proiectul **Beijing Multi-Site Air Quality**.

Scopul proiectului este evaluarea impactului tehnicilor **L1 (Lasso)**, **L2 (Ridge)** și **Elastic Net** asupra performanței, stabilității coeficienților și capacității de generalizare.

---

## 🧠 Conținutul proiectului

### ✔ Pre-procesarea setului de date
- încărcarea și curățarea datelor brute  
- completarea valorilor lipsă (numeric/categoric)  
- One-Hot Encoding pentru direcția vântului  
- scalare standardizată  
- transformarea logaritmică a PM2.5  
- împărțirea Train/Test menținând ordinea temporală  

### ✔ Modelele implementate
- **Linear Regression** (baseline)  
- **Ridge Regression (L2)**  
- **Lasso Regression (L1)**  
- **Elastic Net (L1+L2)**  

Optimizarea hiperparametrilor a fost realizată atât cu **GridSearchCV (K-Fold)**, cât și într-un **experiment suplimentar** folosind **TimeSeriesSplit**, metoda corectă pentru date temporale.

### ✔ Analiză și vizualizări
- RMSE & R² (Train/Test)  
- analiză bias–varianță  
- curbe de învățare  
- distribuția predicțiilor (KDE)  
- comparația coeficienților + coeficienți eliminați  
- interpretarea modelului Elastic Net prin **SHAP**  

---

## 📊 Rezultate principale

### 🔹 Rezultatele inițiale (validare K-Fold)

| Model              | RMSE Test | Observații                                      |
|--------------------|-----------|--------------------------------------------------|
| Linear Regression  | 0.5047    | Precizie numerică ridicată, varianță ușor mare  |
| Lasso (L1)         | ~0.505    | Elimină puține variabile, regularizare slabă     |
| Ridge (L2)         | ~0.506    | Cel mai stabil în prezența multicoliniarității   |
| Elastic Net        | ~0.506    | Compromis bun L1+L2 → **l1_ratio = 0.1**        |

Concluzia inițială: **Elastic Net** era cel mai echilibrat model între reducerea varianței și menținerea performanței.

---

## 🧪 Experiment suplimentar: TimeSeriesSplit + grid rafinat

Pentru evaluare corectă pe date temporale a fost creat un notebook suplimentar:

elastic_net_timeseries_experiment.ipynb


### 🔍 Rezultate cheie
- Elastic Net converge la **l1_ratio = 0.01**, deci ≈99% penalizare L2 → comportament aproape identic cu **Ridge**.  
- Lasso elimină **3 coeficienți**, Elastic Net elimină **1**, Ridge nu elimină nimic.  
- Curbele de învățare indică stabilitate superioară pentru metodele L2.  
- Distribuția predicțiilor (KDE) este aproape identică pentru toate modelele.

### 🔎 Interpretare
Datasetul este dominat de multicoliniaritate → penalizarea **L2** este cea mai adecvată.  
Elastic Net devine, în practică, un model Ridge cu o mică componentă L1 pentru reducerea minimă a zgomotului.

---

## ▶️ Rulare notebook
Notebook-urile pot fi rulate în **Google Colab** încărcând manual fișierele `.ipynb`.  
Datasetul Kaggle trebuie încărcat manual (nu este inclus în repository).

---

## 📁 Structura repository-ului

├── TEMA2.ipynb # Studiul principal (analiza inițială)
├── elastic_net_timeseries_experiment.ipynb # Experiment suplimentar (TimeSeriesSplit)
└── README.md # Documentația proiectului


---

## 🏁 Concluzie

- Regresia liniară oferă cel mai mic RMSE, dar este mai sensibilă la varianță.  
- Modelele L2 (Ridge, Elastic Net) sunt cele mai stabile pe date reale.  
- Elastic Net, cu validare temporală, converge aproape complet către Ridge.  
- SHAP confirmă relevanța variabilelor PM10, DEWP, O3, NO₂ și TEMP.  

Acest proiect oferă o analiză completă, reproductibilă și interpretabilă a modului în care regularizarea influențează calitatea modelelor de regresie pe date reale.
