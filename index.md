
## Abstract

Cross-speaker style transfer aims to extract the speech style of the given reference speech, which can be reproduced in the timbre of arbitrary target speakers. Existing methods on this topic have explored utilizing utterance-level style labels to perform style transferring via either global or local scale style representations. However, audiobook datasets are typically characterized by both the local prosody and global genre, and are rarely accompanied by utterance-level style labels. Thus, properly transferring the reading style across different speakers remains a challenging task. This paper aims to introduce a chunk-wise multi-speaker multi-scale style model to capture both the global genre and the local prosody in audiobook speeches. Moreover, by disentangling speaker timbre and style with the proposed switchable adversarial classifiers, the extracted reading style is made adaptable to the timbre of different speakers. Experiment results confirm that the model manages to transfer a given reading style to new target speakers. With the support of local prosody and genre type predictor, the potentiality of the proposed method in multi-speaker audiobook generation is further revealed.

## Cross-speaker reading style transfer

We evaluate the proposed cross-speaker reading style transfer method on the following disjoint datasets:
- **MST-Originbeat**: A _neutral_ Mandarin corpus from the ICASSP 2021 M2VOC challenge [1], with one female and one male speaker.
- **DB**: A private _neutral_ Mandarin dataset with 10,000 utterances from another female Chinese speaker, named DB6.
- **Audiobook_FM**: A private Mandarin audiobook dataset with 8 speakers and 2 types of topics (**Fairy tale/Chinese martial arts fiction**). A female and a male speakers cover both of the 2 topics, each of the other 6 speakers only covers one of the 2 topics. One of the 6 speakers is DB6, who only reads the fairy tale documents.

The proposed cross-speaker reading style transfer method aims to **generate speeches in the timbre of the given target speaker, while preserving both local prosody and global genre of the reference speech from the audiobook dataset.** The cross-speaker reading style transfer results of both baseline model and the proposed model are provided for comparison.
(**Baseline**: An embedding-table-based baseline method with the 2 global branches of the multi-scale style model replaced with a speaker embedding table and a global genre embedding table.Which is similar to [2], except that there is an additional embedding table of the global genre to accommodate the audiobook dataset.)

### Fairy tales

| Reference Speech | Target Speaker | Baseline | Proposed |
|:------------|:------------|:------------|:------------|
|<audio controls><source src="./static/Ref/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Tgt/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Baseline/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Proposed/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|

### Martial arts fiction


| Reference Speech | Target Speaker | Baseline | Proposed |
|:------------|:------------|:------------|:------------|
|<audio controls><source src="./static/Ref/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Tgt/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Baseline/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Proposed/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|


## Ablation study

In order to reveal the functionality of each component of the proposed method, 3 different settings of ablation experiments are conducted:

- **w/o GSE.style**: remove the global genre branch in the style model, leaving the timbre branch as the only global module;
- **w/o Chunk**: replace the chunk-wise GSE extracting method with an ordinary utterance-wise approach;
- **w/o SAC**: employ vanilla adversarial classifiers to disentangle GSE vectors of different branches, instead of the proposed switchable adversarial classifiers (SAC).

### Fairy tales

| Reference Speech | Target Speaker | Proposed | w/o GSE.style | w/o Chunk | w/o SAC |
|:------------|:------------|:------------|:------------|:------------|:------------|
|<audio controls><source src="./static/Ref/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Tgt/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Proposed/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/wo_gse_style/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/wo_chunk/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/wo_sac/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|

### Martial arts fiction

| Reference Speech | Target Speaker | Proposed | w/o GSE.style | w/o Chunk | w/o SAC |
|:------------|:------------|:------------|:------------|:------------|:------------|
|<audio controls><source src="./static/Ref/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Tgt/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/Proposed/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/wo_gse_style/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/wo_chunk/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|<audio controls><source src="./static/wo_sac/sample.wav" type="audio/wav">Your browser does not support the audio element.</audio>|


## References
1. Q. Xie, X. Tian, G. Liu, K. Song, L. Xie, Z. Wu, H. Li, S. Shi, H. Li, F. Hong, H. Bu, and X. Xu, “The multi-speaker multi-style voice cloning challenge 2021,” in ICASSP 2021 - 2021 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP), 2021, pp.8613–8617.
2. Q. Xie, T. Li, X. Wang, Z. Wang, L. Xie, G. Yu, and G. Wan, “Multi-speaker multi-style text-to-speech synthesis with single- speaker single-style training data scenarios,” _arXiv preprint arXiv:2112.12743_, 2021.