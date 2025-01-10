# LLM-Detect-AI-Generated-Text-Silver-Medal-Solution
Novice who participated in the competition for the first time shared my experiences.

Compared with the training set, the experimental set with unpublished specific content has more numbers and more topics.

I generated 2000 texts using the interface of the Great Prophecy Model, and then screened the length and similarity to select the articles that can be used.

At first, I tried the pure traditional machine learning method, that is, using GPC Gaussian classification model to predict the data alone. Although the training prediction speed is very fast, the prediction accuracy is very poor.) bpe byte pairs are encoded to generate token tfidf statistical text features, and the dimensions are reduced by truncating SVD and then input into GPC model for training.
![GPC](https://github.com/user-attachments/assets/2beb10c4-859a-4e59-9be8-b2b9b39c0462)

Training model: set the difference between the category probability predicted by EarlyStoppingCallback and eval_loss model and the real label, and save the checkpoint.

How to forecast multiple models (using preprocessing function to directly segment and tokenize the data collected by me, padding the data, setting fine-tuning parameters, fine-tuning DistilRoBERTa, using the method of saving fine-tuning, and finally directly importing the parameters of fine-tuning model in the competition.

Multi-model stacking mode: integrate the pre-training model with the traditional machine learning model, and combine their characteristics to improve the generalization ability of the model (in fact, it is the idea that three heads are better than one) (DistilRoBERTa, SGDClassifier, LGBMClassifier and RF_model). Through the method of integrated learning, the prediction probability is obtained by training with the method of 50% cross-validation, and the results are stacked and spliced together. Finally, the model is integrated by LGBM and logistic regression.

![Stacking](https://github.com/user-attachments/assets/20362a0c-56e3-41ec-80a9-17da37870949)
