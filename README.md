# Alzheimer's Disease Classification using Inception V3

Questo progetto implementa una **Convolutional Neural Network (CNN)** per la diagnosi automatica della malattia di Alzheimer a partire da immagini di risonanza magnetica (MRI). Il sistema sfrutta l'architettura **Inception V3** tramite **Transfer Learning** per classificare il livello di demenza.

## Dataset

Il modello è stato addestrato sul dataset **OASIS 1**, convertendo le scansioni 3D (NiFTI) in immagini 2D (JPG) e selezionando le slice centrali più significative.
Le immagini sono classificate in 4 stadi di gravità:
1. **Non Demented** (Sano)
2. **Very Mild Demented** (Molto lieve)
3. **Mild Demented** (Lieve)
4. **Moderate Demented** (Moderata)

## Architettura e Pipeline

### 1. Preprocessing
* **Undersampling:** Bilanciamento delle classi maggioritarie.
* **Data Augmentation:** Zoom, rotazioni e shift per arricchire il dataset.
* **Rescaling:** Normalizzazione dei pixel nel range [0, 1].

### 2. Modello
* **Base:** Inception V3 (pesi pre-addestrati su ImageNet, top rimosso).
* **Head Personalizzata:**
    * Global Average Pooling
    * Dropout (0.5) per ridurre l'overfitting
    * Dense Output Layer (4 neuroni, attivazione Softmax)

### 3. Training
* **Ottimizzatore:** Adamax.
* **Loss Function:** Categorical Crossentropy.
* **Callbacks:** Early Stopping e ReduceLROnPlateau per ottimizzare la convergenza.

## Risultati

Il modello ha raggiunto un'accuratezza del **94.4%** sul test set. Di seguito le metriche principali:

| Metrica | Valore |
| :--- | :--- |
| **Accuratezza** | 94.40% |
| **F1-Score** | 97.52% |
| **Sensibilità Media** | 96.13% |
| **Specificità Media** | 98.95% |

Il sistema si è dimostrato particolarmente efficace nell'individuare gli stadi precoci (*Very Mild* e *Mild*), cruciali per una diagnosi tempestiva.
