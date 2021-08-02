---
title: Neural Network Project
summary: implementation of an Artificial Intelligence Neural Network from scratch using Python programming language.
tags:
- Machine Learning
- Python
date: "2021-06-09T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart

links:
url_code: "https://github.com/mimmo96/ML_PROJECT"
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

The aim of the project was to create a Neural Network that learn from training data using the
best configuration of hyperparameters. To finds the hyperparameters we use a grid search with
5-fold cross validation and then we tested the models on internal test set (used only for testing
phase), during the training phase, models uses the classic backpropagation algorithm. The
correctness of network implementation was tested on “Monk’s problem” and then we used
ML-CUP20-TR to train models. We selected the 8 best models and deployed an ensamble to
predict the outputs of ML-CUP20-TS. The Neural Network can resolve both classification and
regression problem. 
We implemented the software using Python programming language. We used some
mathematics and data manipulation tools such as: numpy, sklen, pandas, matplotlib and math.
No machine learning tool was used. We implemented a multi-layer feed forward neural
network that learns through back-propagation algorithm using Stochastic Gradient Descent
technique. The network can learn using different activation function, momentum, thikonov
regularization, learning rate schedules (constant, variable), different weight update policies
(online, mini-batch, batch), early stopping. 
We divided ML-CUP20-TR in development set and test set. The development set contains
80% of ML-CUP20-TR while test set contains 20%. Development set was split in training set
and validation set that contains 80% and 20% of development set. Hyper-parameters are
inserted by hand and then we performed a grid search. Validation set is used to evaluate the
generated model at each epoch and we kept epoch t in which we obtained the lowest error on
validation set, this epoch t is used to stop retraining of the model. We also used early stopping
to arrest the training phase when validation error start to increase according to Generalization
Loss explained by Lutz Prechelt . We selected the best models by looking at the metric
reported in terms of Mean Euclidean Error on validation set and its standard deviation. Then
we applied a random perturbation to the parameters of 8 best models, so we create 8 new
models with these perturbated parameters and trained them from scratch. The final 8 best
models are chosen from models with perturbated parameters and the 8 best models came out
of previous grid search. The 8 best configurations are retraining on the entire development set
and then ensembled creating an instance of the class Ensable. The ensamble performs its
predictions by averaging the predictions of its constituent models. We used test set only to
evaluate each of the 8 model and ensabled model, we had never used test set during model
selection or other previous phases.
We started with a preliminary analysis of hyper parameters to understand the behaviour of the
network on data set, and then we selected best hyper parameters to perform the final grid
search. An interval of all parameters used are reported in Table 2. In total, we tested about
1500 different configurations respecting the general rules [1]. The hardware components used
are AMD Ryzen 5 3600 4,20 GHz Six-Core processor which completes the model selection
phase approximately in 30 hours. In the preliminary analysis we noticed that more than 50
units led to the instability of the learning curve, while a high learning rate (more than 0.1) led
the learning curve to diverge. We also implemented a variable learning rate [2] but we obtain
better result with a fixed learning rate. Another important property that allowed us to avoid
overfitting was the Early Stopping technique (of chapter 2.3) that arrest the training when
Generalization Loss exceeds the threshold of 2%, in this case we returned the best model
found so far otherwise the training go ahead until maximum epoch (that we set to 500). This
technique allowed to accelerate and control the model selection process. We realized that many
layers were not very functional, the models we found had a good error with one or two layers.
Very high hidden units such as 100 or more units did not bring good results and sometimes the
model was overfitted, indeed we chose not to exceed 50 units. We adopted only regularization
L2 during training phase and a low value was sufficient to stable learning curves. Since we are
in the case of regression we have chosen a linear activation function for output layer, while for
hidden layer functions we tried tanh, sigmoidal, relu, leaky_relu; preferring tanh, sigmoidal
for stability and results of the models. As we said, we perform a 5-fold cross validation which
returned the mean over the 5 folds of Mean Euclidean Error and Mean Squared Error for both
training and validation and their respective standard deviations. Also, for each of 5 folds we
tried 5 random starting configuration and we take the mean error of them. The best models
were selected considering their MEE and its standard deviation. We used 8 best models came
out of grid search to create 8 models with random perturbation of hyperparameters, the values
for learning_rate, lambda, momentum, were randomly generated from a normal distribution
centered at their base value, instead, the batch_size was generated by randomly varying its
value within a range of 15 and each layer within a range of 3 units. The final 8 best models are
chosen from models with perturbated parameters and the 8 best models came out of previous
grid search. These models are retrained on all development set until epoch t in which we
obtained the lower validation error. In Table 4 we represented 8 best models selected. After
we performed an ensemble of the 8 models which results on development set and unseen
internal test set are reported in Table 3. We used internal test only at the end of model selection
phase and we used it only to provide an error evaluate on final model fit on development set.
Figure 2 shows learning curves of 8 best models on training and validation set.