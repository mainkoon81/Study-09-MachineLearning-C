# Study-09-MachineLearning-C-[Deep Learning]
DeepLearning Intro

----------------------------------------------------------------------------------------------------------------------------------------
## What if the data is not linearly separable ?
<img src="https://user-images.githubusercontent.com/31917400/41435452-c25ebfae-7016-11e8-808c-8e740d608806.jpg" />

**How to Combine two linear models into a non-linear model?**: Each linear model is a whole probability space, which means for every points, it gives us **the probability of the point being 'positive'**. And we have two linear models, thus we get two probability values.  
 - Example01: We add up two probabilities, then pass into the Sigmoid function, which gives us the final probability value!
 - Example02: But what if we need to weight this sum? 
   - We take a linear combination of the two linear models(thinking of the **new line** of between the two models)
<img src="https://user-images.githubusercontent.com/31917400/41471198-de1cd444-70aa-11e8-9908-cabaf9373110.jpg" />

### Neural Network(Multi-Layer Perceptrons) Architecture
 - Deep Neural Network(More complex network and multiple layers):
   - Layers
     - Input-layer: input values(from field_A, field_B,..or from the Sigmoid_A, Sigmoid_B..) that constitute each datapoint.  
     - Hidden-layer: a set of linear models generated by the Input-layer, and probabilities from the Sigmoid(). 
     - Output-layer: where the two linear models(two Sigmoid-outputs) get combined to obtain a non-linear model.
   - If adding more **nodes** to the input, hidden, and output layers?
     - What happens if the Hidden-layer has more nodes?
       - We combine more linear models and obtain a triangular boundary in the Output-layer. 
     - What happens if the Input-layer has more nodes?
       - our linear models become planes..and our output-layer bounds a nonlinear region.
     - What if the Output-layer has more nodes?
       - We get more outputs. This is when we have a multiclass classification model. We'll have each node in the Output-layer outputting a score for each one of the classes(one for A, one for B...)
   - If adding more **layers**?
     - Our linear models combine to create non-linare models, then these combine to create even more non-linear models.
     - In this way, the network will split the n-dimensional space with a highly non-linear boundary as the output.  
<img src="https://user-images.githubusercontent.com/31917400/41473766-1f9e9f9a-70b2-11e8-8839-e1e67a215c09.jpg" />
     
 - Multiclass Classification: If our neural network needs to model data with more than one output?
   - Simply add more nodes in the Output-layer!
   - We take the scores and apply the **softmax()** function to obtain well-defined probabilities.  
<img src="https://user-images.githubusercontent.com/31917400/41475409-a2493d70-70b6-11e8-80b1-dc178c478fdf.jpg" />












































