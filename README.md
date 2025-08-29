# HackTive
Mental health chat analysis

bit.ly/Hacktive_Classification (Link Gdrive untuk dataset, code, PPT)

PROJECT OVERVIEW & ANALYSIS PROCESS
LATAR BELAKANG

Kesehatan mental menjadi isu krusial di era digital, terutama di kalangan anak muda dan pekerja. Banyak individu mengekspresikan perasaan stres, cemas, hingga depresi melalui media sosial atau platform diskusi daring.
Sayangnya, jumlah percakapan yang sangat besar membuat psikolog dan konselor sulit memantau serta merespons secara cepat. Hal ini dapat menimbulkan risiko keterlambatan dalam memberikan dukungan, bahkan meningkatkan potensi tindakan berbahaya seperti self-harm.

TUJUAN


Mengklasifikasikan percakapan/chat berdasarkan kategori kesehatan mental (normal, stres ringan, depresi, suicidal risk).

Summarization pada percakapan panjang agar konselor/psikolog dapat memahami inti masalah dengan cepat.

Insight mengenai pola bahasa, kata kunci, serta tren komunikasi sebagai indikator kondisi mental seseorang.

PERMASALAHAN

Sulitnya deteksi dini tanda depresi dari ribuan percakapan.

Keterbatasan waktu tenaga profesional dalam membaca teks panjang.

Kurangnya sistem otomatis yang membantu memprioritaskan kasus serius.

PENDEKATAN

Pengumpulan Data: dataset Kaggle + scraping dari X dengan kata kunci depresi.

Preprocessing: membersihkan teks, normalisasi, stopwords removal, tokenisasi.

Klasifikasi: SVM, Random Forest, BERT, DistilBERT.

Summarization: extractive (TextRank), abstractive (T5/BART).

Evaluasi: akurasi, precision, recall, F1, ROUGE.

RELEVANSI

Industri: integrasi chatbot konseling/online.

Sosial: deteksi dini masalah mental.

Akademik: kombinasi classification + summarization dengan AI/LLM.


PRE-PROCESSING

Pembersihan teks (lowercase, hapus URL, simbol, angka).

Data kosong dihapus.

Pelabelan numerik: suicide = 1, non-suicide = 0.

FEATURE ENGINEERING

Fitur panjang teks (jumlah kata/karakter).

Analisis sentimen dengan VADER.

Identifikasi kata kunci: bunuh, mati, sakit, putus asa.

Hitung pronoun (aku, saya, diriku).

PERSIAPAN MODEL BERT

Split data: 80% train, 20% test (stratifikasi).

Tokenisasi: [CLS], [SEP], max_length=128, attention mask.

DataLoader: batch untuk GPU.

PELATIHAN MODEL

Model: BertForSequenceClassification (bert-base-uncased).

Optimizer: AdamW + scheduler.

Proses: forward pass → loss → backward pass → update weight.

EVALUASI MODEL

Akurasi: 0.9692

Precision: 0.9692

Recall: 0.9692

F1: 0.9692

Risk Factors: Suicide 13.854 (49.1%), Non-Suicide 14.361.

AI SUPPORT & EXPLANATION

Embedding kontekstual: BERT memahami kata berdasarkan konteks.

Attention mechanism: fokus pada kata kunci.

Transfer learning: manfaatkan pre-trained knowledge.

HASIL UJI BERT

Accuracy: 96.29%

Precision: 96.97%

Recall: 96.9%

F1: tinggi & seimbang

BAGAIMANA MODEL BEKERJA?

Tokenisasi (WordPiece, max_length=128).

Fine-tuning classification head di atas [CLS].

Inferensi → softmax → probabilitas.

Fitur tambahan: VADER, keywords, pronouns (analisis forensik).

“You are more than your mood.”

CARA KERJA SISTEM

Prediksi dengan BERT → probabilitas suicidal vs non-suicidal.

Explainability Layer: panjang teks, pronoun, sentiment, keywords.

Output: Risk Level (Low, Medium, High).

Cara Menggunakan Sistem

Load model (./model_save/).

Input teks → suicide_risk_assessment_system().

Output: prediksi + probabilitas + risk level + analisis detail.

INSIGHT & FINDINGS
INTERPRETASI

Medium Risk: “I don’t know if I can keep going anymore…” → Prob suicidal 0.724.

Medium-High Risk: “I can’t take this pain anymore…” → Prob suicidal ≈ 0.78.

Low Risk: “I’ve been feeling down…” → Non-suicidal dominan.

PERFORMA MODEL

Akurasi: 96.92%

Precision & Recall: 96.92%

F1: 96.92%

POLA LINGUISTIK

Kata kunci: pain, want, end, hope, help.

Pronoun “I, me, my” lebih sering pada suicidal text.

Teks suicidal lebih panjang.

KEMAMPUAN

Deteksi pola halus.

Respons instan.

Konsistensi tinggi.

BATASAN

Error rate 3% → signifikan di kasus high-risk.

Variasi confidence 53–86% → perlu human review.

False negatives berbahaya.

Sulit dengan sarkasme & nuansa budaya.

bit.ly/Hacktive_Classification

https://www.kaggle.com/datasets/nikhileswarkomati/suicide-watch/data
