Pipeline Description: This pipeline is designed for ancient Spanish text detection and transcription using a combination of LLMs and a fine-tuned vision–language model.

Approach: Florence-2 was used for primary text detection and segmentation. The segmented text regions were then passed to a fine-tuned Qwen2-VL (2B) model optimized for line-level recognition. In parallel, the original image was processed by Gemini using a custom prompt, and the outputs from both models were stored.
After image preprocessing—specifically Sauvola thresholding and skeletonization—the preprocessed image, Gemini’s prediction, and Qwen’s prediction were provided to a final Judge LLM. This ensemble step resolves discrepancies between the models, improving spelling accuracy and overall transcription reliability.

```
Input Image
   │
   ▼
Florence-2 (Text Detection & Segmentation)
   │
   ▼
Text Lines → Qwen2-VL (Line Recognition)
   │
Original Image → Gemini (Prediction)
   │
Preprocessing (Sauvola + Skeletonization)
   │
   ▼
Judge LLM (Combine Qwen + Gemini + Image)
   │
   ▼
Final Transcription
```

Evaluation Metrics:
    1.Cer score: 8.92% (pg.no 20) 
    <img width="643" height="67" alt="answer1" src="https://github.com/user-attachments/assets/03222e3e-29b1-47f6-a538-c0c349900b10" />
    2.Bert score: 91% (pg.no 20)
    <img width="263" height="100" alt="bert_score" src="https://github.com/user-attachments/assets/9b5e9b49-95b8-458d-b265-89983644de9b" />
    3.Wer score:30% (pg.no 21)
    The higher WER is mainly due to word-level mismatches.
    
    








