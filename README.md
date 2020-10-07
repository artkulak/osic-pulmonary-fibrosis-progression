# OSIC Pulmonary Fibrosis Progression 1st place solution

## Introduction

During the [OSIC Pulmonary Fibrosis Progression](https://www.kaggle.com/c/osic-pulmonary-fibrosis-progression) the competitors were asked to predict a patient’s severity of the decline in lung function based on a CT scan of their lungs and some additional tabular data fields.  The challenge was to use machine learning techniques to make a prediction with the image, metadata, and baseline FVC as input. The task wasn't simple. Due to the rather low amount of data available, it was not easy to use traditional Computer Vision approaches to model the dependency between CT scans and patient FVC values. Moreover, the public leaderboard score was based only on 15% of test data and didn't correlate with the validation at all, which made it really hard to select the best models for final submission. 

In general, it is really hard to explain all the subtle points of the competition here, so I recommend to visit the competition link above and read about it yourself if you are really interested!

## Training, models and final solution

I have tried a lot of things, but ironically the backbone to my best solution turned out to be this [kernel](https://www.kaggle.com/khoongweihao/efficientnets-quantile-regression-inference) :)

Speaking about my final solution, here is what I have done to achieve this score. Firstly, I trained both models (Quantile Regression + EfficientNet b5) from scratch. For both models, I lowered the number of epochs. For effnet I decided to train for 30 epochs and for quantile regression for 600 epochs. Then, I changed the architecture of Quantile Regression a bit, because on validation my architecture worked a bit better. Apart from that, I removed all the "Percent" related features for both models, it turned out that it gave a huge boost on private lb for me. The hardest decision was how to choose the weights for the blend. Well, I just decided to give a slightly higher weight to Quantile Regression because for me it seemed to work better. Finally, I did some more improvements for the backbone notebook, for example, there was a part with the quantile selection based on the best loglikelihood score for the EfficientNet models. This part took ages to finish and moreover, for me, it looked like not a good decision, so I have just set the quantile to 0.5 and didn't select anything, this allowed my Inference notebooks to run in just 3 minutes total.

## How to run

`effnet_b5_training_30_epochs.ipynb` - contains training pipeline for the best EfficientNet b5 model <br><br>
`inference-45-55-600-epochs-tuned-effnet-b5-30-ep.ipynb` - contains inference part for the kernel with the highest lb score <br><br>
`simple-logreg.ipynb` - contains naive approach which turned out to be in the bronze zone <br><br>

## Final words

Below I will attach links to my final submission notebooks, along with Medium and Kaggle writeups.

[1st Place notebook]()

[Bronze zone very simple solution]()

[Kaggle writeup]()

[Medium writeup]()
