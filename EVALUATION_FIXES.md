# ViT Intermediate evaluation-label corrections

This branch adds a corrected, **source-only** copy of the ViT + BanglaBERT Intermediate Fusion notebook. The original `Fake_Photocards_detection.zip` on `main` is **unchanged**.

## Small, deliberate corrections

- Compute confusion matrices with `labels=[1, 0]` and label both axes `Real (1), Fake (0)`.
- Fix explanation class mapping to `0 = Fake News Card`, `1 = Real News Card`, and correct the true-label display.
- Use `average='macro'` for precision, recall, and F1 to match the research report. With 150 samples from each class, macro and weighted averages coincide for this test set.
- Label XAI graphics accurately as **ViT input-gradient saliency** and **Integrated Gradients**. The notebook does not implement Grad-CAM or SHAP.
- Display missing image IDs instead of only reporting the number found.

## Deliberately unchanged

Model architecture, training loop, augmentation, random seed, dataset records, weights, and historical measurements. Historical notebook outputs were cleared in the corrected **copy**, because stored plots show pre-correction labels; rerun evaluation to regenerate them. This commit **does not** retrain the model or alter measured accuracy.

### Expected class-order correction for this model

Rows = actual; columns = predicted, in **Real, Fake** order:

```
[[146, 4],
 [  1,149]]
```

Total correct = 295/300 = **98.33%**. Macro precision **0.9835**, macro recall **0.9833**, macro F1 **0.9833**. Confirm these values against the original saved predictions before editing report figures.

**Report follow-up:** This reverses the old Real-to-Fake versus Fake-to-Real error interpretation for this *one* notebook. Correct only the relevant entry in Figure 4.3, Figure 4.4, and Table 4.2; do not silently apply it to the other six models. Review the research write-up's Grad-CAM/SHAP claims separately.

### How to use

1. Open `notebooks/ViT_BanglaBERT_Intermediate_corrected.ipynb` in Kaggle or Jupyter.
2. Point dataset paths at your training files.
3. Rerun the evaluation and XAI cells on the existing trained model, if available.
4. Compare regenerated plots and labels with this note; commit fresh results only after verification.
