Questo progetto analizza 14 anni di dati storici (2004-2018) della rete elettrica PJM per identificare pattern di consumo e prevedere situazioni di stress per la rete (rischio Blackout).

L'obiettivo è trasformare dati grezzi orari in un **Sistema di Supporto Decisionale** che permetta all'azienda di:
1.  Pianificare la manutenzione nei giorni a basso carico.
2.  Pre-allertare le centrali di riserva nei giorni critici.

---

## Il Problema
Le compagnie elettriche affrontano due rischi opposti:
* **Sottostima della domanda:** Rischio Blackout.
* **Sovrastima della domanda:** Spreco economico (centrali accese inutilmente).

La sfida di questo progetto è stata costruire un modello predittivo affidabile partendo da un dataset minimalista (solo 2 colonne: Data e Consumo), senza dati meteorologici o economici esterni.

---

## Workflow del Progetto

Il notebook segue una pipeline di Data Science completa:

### 1. Data Cleaning & Engineering
* Gestione delle serie temporali e rimozione dei duplicati dovuti al cambio dell'ora legale (DST).
* Estrazione di feature temporali (Mese, Giorno, Anno).

### 2. Exploratory Data Analysis (EDA)
* **Trend:** Identificato il fenomeno del "Disaccoppiamento" (consumi stabili nonostante la crescita economica grazie all'efficienza energetica).
* **Profilo Orario:** Individuato il problema estivo (14:00 - 18:00), momento di massimo rischio per la rete a causa dell'aria condizionata.

### 3. Segmentazione (Unsupervised Learning)
Utilizzo dell'algoritmo **K-Means Clustering** per categorizzare le giornate in 3 profili operativi:
* **Mite:** Basso rischio (Mezze stagioni).
* **Standard:** Carico costante (Inverno).
* **Critico:** Alto rischio blackout (Estate torrida).

### 4. Predictive Modeling (Supervised Learning)
Addestramento di un classificatore **Random Forest** per prevedere la classe di rischio del giorno successivo basandosi solo sul calendario.

---

## Risultati Chiave

Il modello ha raggiunto un'**Accuratezza del 74%** sul Test Set.

| Metrica | Valore | Insight di Business |
| :--- | :--- | :--- |
| **Precision (Critico)** | **75%** | Quando il modello prevede un allarme, ha ragione 3 volte su 4. Bassi falsi positivi. |
| **Recall (Mite)** | **80%** | Il modello identifica ottimamente i giorni sicuri per la manutenzione. |
| **Accuracy** | **74%** | Risultato ottenuto usando **solo** variabili di calendario (senza Meteo). |

> **Conclusione:** Il 74% del comportamento energetico è dettato puramente dalle abitudini sociali e dalla stagionalità. L'integrazione futura di dati meteo potrebbe coprire il gap rimanente.

---

## Tecnologie Utilizzate
* **Python:** Linguaggio principale.
* **Pandas & NumPy:** Manipolazione dati.
* **Matplotlib & Seaborn:** Visualizzazione dati.
* **Scikit-Learn:** Clustering (K-Means) e Classificazione (Random Forest).

---

## Come Eseguire il Progetto
1.  Clona il repository:
    ```bash
    git clone https://github.com/reimici/EnergyConsumptionAnalysis.git
    ```
2.  Installa le dipendenze:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn
    ```
3.  Apri il notebook:
    ```bash
    jupyter notebook notebook.ipynb
    ```

---
