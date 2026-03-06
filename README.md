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

## Evaluation Metrics

1. **CER Score:** 8.92% (pg. 20)

<img width="206" height="75" alt="cer_score" src="https://github.com/user-attachments/assets/03c448f9-1c0c-49ff-a143-1d759a6e1d24" />


2. **BERTScore:** 91% (pg. 20)

<img width="263" height="100" alt="bert_score" src="https://github.com/user-attachments/assets/9b5e9b49-95b8-458d-b265-89983644de9b" />

3. **WER Score:** 30% (pg. 21)

The higher WER is mainly due to word-level mismatches.
    








