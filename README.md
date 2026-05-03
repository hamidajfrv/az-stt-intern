# az-stt-intern — Azərbaycan Dilində Nitq Tanıma (ASR)

## Layihənin İzahatı
Bu layihə Azərbaycan dili üçün avtomatik nitq tanıma (ASR) pipeline-ının 
qurulmasını əhatə edir. OpenAI Whisper modelindən istifadə edilmiş və 
Mozilla Common Voice 25.0 dataseti üzərində test edilmişdir.

## İstifadə Olunan Model və Parametrlər
- **Model:** openai/whisper-small
- **Dataset:** Mozilla Common Voice 25.0 (Azerbaijani)
- **Fine-tuning:** 150 train, 30 validation nümunəsi
- **Epochs:** 8
- **Batch size:** 4
- **Learning rate:** 1e-5
- **Best checkpoint:** Epoch 2 (ən aşağı validation loss)

## WER/CER Nəticələri

### Baza Modeli (Part A)
| Metrika | Nəticə |
|---------|--------|
| WER | 66.56% |
| CER | 21.29% |

### Fine-tuned Model Müqayisəsi (Part B)
| Model | WER |
|-------|-----|
| Baseline | 76.90% |
| Fine-tuned | 55.00% |

## Kodu İşə Salmaq

### Quraşdırma 
pip install -r requirements.txt

## Kodu İşə Salmaq

### Part A — Baza ASR
1. `part_a/asr_baseline.ipynb` faylını Google Colab-da açın
2. T4 GPU aktiv edin
3. Bütün cellləri ardıcıl işə salın

### Part B — Fine-tuning
1. `part_b/finetuning.ipynb` faylını Google Colab-da açın
2. T4 GPU aktiv edin
3. Bütün cellləri ardıcıl işə salın

## Fine-tuning Nəticəsi
Fine-tuning nəticəsində WER 76.90%-dən 55.00%-ə endi — təxminən 22% yaxşılaşma.
Overfitting epoch 3-dən başladı, `load_best_model_at_end=True` sayəsində 
ən yaxşı checkpoint (epoch 2) avtomatik seçildi.
