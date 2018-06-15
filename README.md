# Study-09-MachineLearning-C-[Deep Learning]
DeepLearning Intro

----------------------------------------------------------------------------------------------------------------------------------------
> a single perceptron
<img src="https://user-images.githubusercontent.com/31917400/41435071-8fdfdd98-7015-11e8-8984-9237b02a18ec.jpg" />

## But...what if the data is not linearly separable ?
 - We use the Gradient Descent Algorithm??
<img src="https://user-images.githubusercontent.com/31917400/41435452-c25ebfae-7016-11e8-808c-8e740d608806.jpg" />

### Neural Network(Multi-Layer Perceptrons) Architecture
 - How to Combine two linear models into a non-linear model:
   - Each linear model is a whole probability space, which means for every points, it gives us the probability of the point being 'positive'. And we have two linear models, thus we get two probability values.  
   - We add up two probabilities, then pass into the Sigmoid function, which gives us the final probability value!
   - But what if we want to weight this sum? 
     - We take a linear combination of the two linear models(thinking of the **new line** of between the two models)
<img src="https://user-images.githubusercontent.com/31917400/41471198-de1cd444-70aa-11e8-9908-cabaf9373110.jpg" />














































