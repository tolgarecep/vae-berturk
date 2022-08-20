SVM performance and t-SNE result for representations of samples in [Turkish sentiment analysis dataset](https://www.kaggle.com/datasets/burhanbilenn/duygu-analizi-icin-urun-yorumlari) (class "Tarafsız" (en. neutral) has been ignored) extracted with three different methods have been compared. 
# BERTurk
- `berturk.ipynb` saves the computed [CLS] token for each sentence. Computation was done 1000 samples at a run for hardware convenience. In `berturk_svm_tsne.ipynb`, SVM has been used for predicting sentiment of a sentence by its BERTurk representation and 2-dimensional t-SNE results have been visualized. 
# VAE
- `vae_oscar.ipynb` trains [VAE](https://github.com/shentianxiao/text-autoencoders) on a small portion of OSCAR's `unshuffled_deduplicated_tr`. `vae_svm_tsne.ipynb` tests representations in the same way as before.
# TF-IDF
- `tf-idf.ipynb` implements TF-IDF and provides most successful representations in SVM and t-SNE.

| method | representation space | f1 score |
| ------------- | ------------- | ------------- |
| BERTurk | 768-dim | 0.89 |
| VAE | 128-dim | ? |
| TD-IDF | 6945-dim | 0.91 |
