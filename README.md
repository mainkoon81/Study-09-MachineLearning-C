# Study-09-MachineLearning-C-[Deep Learning]
DeepLearning Intro

----------------------------------------------------------------------------------------------------------------------------------------
## What if the data is not linearly separable ?
<img src="https://user-images.githubusercontent.com/31917400/41435452-c25ebfae-7016-11e8-808c-8e740d608806.jpg" />

**How to Combine two linear models into a non-linear model?**: Each linear model is a whole probability space, which means for every points, it gives us **the probability of the point being 'positive'**. And we have two linear models, thus we get two probability values.  
 - Example01: We add up two probabilities, then pass into the Sigmoid function, which gives us the final probability value!
 - Example02: But what if we need to weight this sum? 
   - We take a **[LINEAR-COMBINATION]** of the two linear models(thinking of the **new line** of between the two models)
<img src="https://user-images.githubusercontent.com/31917400/41471198-de1cd444-70aa-11e8-9908-cabaf9373110.jpg" />

### Deep Neural Network(More complex network and multiple layers):
   - Basic 3 Layers
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
<img src="https://user-images.githubusercontent.com/31917400/41533886-49e55b1a-72f4-11e8-8313-12ec22f57952.jpg" />
<img src="https://user-images.githubusercontent.com/31917400/41535449-446184f6-72fa-11e8-9b38-95b8439c72fa.jpg" />

### How do neural networks process the input to obtain an output? 
### 1.Feedforward
What parameters(W,b) should they have on the edges(x1, x2) in order to model our data well? 
 - The perceptron(the simplist NN) here is defined by a linear model where W1 > W2.
 - Then the perceptron plots the points(x1, x2) and outputs the odds that the point is positive.
<img src="https://user-images.githubusercontent.com/31917400/41541346-1e378cac-730a-11e8-90e5-fe82148dbaf9.jpg" />
     
 - Error-Function(How badly each point is being classified? How far from the line?)
<img src="https://user-images.githubusercontent.com/31917400/41541969-af95ec10-730b-11e8-9eda-194d5e58301a.jpg" />

### 2.Backpropagation
 - 1. Doing a feedforward operation
 - 2. Comparing the **output** of the model with the **desired output**.
 - 3. Calculating the error.
 - 4. Running the feedforward operation backwards (backpropagation) to spread the error to each of the weights.
 - 5. Use this to update the weights, and get a better model.
 - 6. Continue this until we have a model that is good.

[GradientDescentAlgorithm & Backpropagation]
> Single Perceptron
 - We calculate the `Gradient` of the Error-Function E(W)
   - What the misclassified-point want: the **boundary** to come closer to it then, the boundary get closer to it by updating (W,b).
   - We continue doing this to minimize the error. 
> Multi-layer Perceptron
 - The Error-Function is more complicated, thus we do `Backpropagation`:
   - What the misclassified-point want: the **(+) region** to come closer to it then, 
     - when looking at the two linear models in the hidden-layer, we can see which one is doing better.
     - so we care the better linear model more than the other.
       - Reduce the `W` coming from the loser and increase the `W` coming from the winner.
     - or we go back to the hidden layer and for the loser model, we have its boundary get closer to the point by updating (W,b), and for the winner model, we have its boundery move farther away from the point by updating (W,b).    
<img src="https://user-images.githubusercontent.com/31917400/41565629-73289c8e-734f-11e8-8a7c-28ab563b0141.jpg" />

 - Example
<img src="https://user-images.githubusercontent.com/31917400/41567175-dc114618-7356-11e8-8454-d463b158f2f0.jpg" />
 
### Building a Neural Network in Keras
```
from keras.models import Sequential
model = Sequential()
```
 - The `keras.models.Sequential` class is a wrapper for the neural network model that treats the network as a **sequence of layers**. 
 - It implements the Keras model interface with common methods like `compile()`, `fit()`, and `evaluate()` that are used to train and run the model. 
 - **Layers**: The `keras.layers` class provides a common interface for a variety of standard neural network layers: 
   - fully connected layers
   - max pool layers
   - activation layers, and more. 
   - We can add a layer to a model using the model's `add()` method.
   - Keras requires the **input shape** to be specified in the **first layer**, then it will automatically infer the shape of all other layers. This means we only have to explicitly set the input dimensions for the first layer.

For example, a simple model with a single hidden layer might look like this:
 - X has shape (num_rows, num_cols), where the training data are stored as row vectors. 
 - y must have an output vector for each input vector. 
```
import numpy as np
from keras.models import Sequential
from keras.layers.core import Dense, Activation

X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]], dtype=np.float32)
y = np.array([[0], [0], [0], [1]], dtype=np.float32)


# Create the Sequential model
model = Sequential()

# 1st Layer - Add an input layer of 32 nodes with the same input shape as the training samples in X
model.add(Dense(32, input_dim=X.shape[1]))

# Add a softmax activation layer
model.add(Activation('softmax'))

# 2nd Layer - Add a fully connected output layer
model.add(Dense(1))

# Add a sigmoid activation layer
model.add(Activation('sigmoid'))
```
The first(hidden) layer `model.add(Dense(32, input_dim=X.shape[1]))`: creates **32 nodes** which each expect to receive 2-element vectors(shape[1] is two columns) as inputs. 

Each layer takes the outputs from the previous layer as inputs and pipes through to the next layer. This chain of passing output to the next layer continues until the last layer, which is the output of the model. We can see that the output has dimension 1.

The **activation layers** are equivalent to specifying an activation function in the Dense layers. For example, `model.add(Dense(128)); model.add(Activation('softmax'))` is computationally equivalent to `model.add(Dense(128, activation="softmax"))`, but it is common to explicitly separate the **activation layers** because it allows direct access to the outputs of each layer before the activation is applied (which is useful in some model architectures).

Once we have our model built, we need to **compile it** before it can be run. Compiling the Keras model calls the **backend** (tensorflow, theano, etc.) and binds the optimizer, loss function, and other parameters required before the model can be run on any input data. 
```
model.compile(loss="categorical_crossentropy", optimizer="adam", metrics = ["accuracy"])
```
We'll specify the loss function to be `categorical_crossentropy` which can be used when there are only **two classes**, and specify `adam` as the optimizer (which is a reasonable default when speed is a priority). And finally, we can specify what **metrics** we want to evaluate the model with. Here we'll use `accuracy`. 

The model is trained with the `fit()`. `vervose` is the message level(how much information we want displayed on the screen during training).
```
model.fit(X, y, epochs=1000, verbose=0)
model.evaluate()
```

------------------------------------------------------------------------------------------------------------------------------------
### Perceptron Example(logical operator)
 - Application example: Perceptron can be a logical operator: AND, OR, NOT, XOR...
   - Take two inputs then returns an output.
 - Interestingly, perceptron can classify the data that is not linearly separable. 
<img src="https://user-images.githubusercontent.com/31917400/39961806-b1513700-5635-11e8-9edf-f3cde879577c.jpg" />

```
import pandas as pd

test_inputs = [(0, 0), (0, 1), (1, 0), (1, 1)]
correct_outputs = [False, False, False, True]
outputs = []

for test_input, correct_output in zip(test_inputs, correct_outputs):
    linear_combination = weight1 * test_input[0] + weight2 * test_input[1] + bias
    output = int(linear_combination >= 0)
    is_correct_string = 'Yes' if output == correct_output else 'No'
    outputs.append([test_input[0], test_input[1], linear_combination, output, is_correct_string])

num_wrong = len([output[4] for output in outputs if output[4] == 'No'])
output_frame = pd.DataFrame(outputs, columns=['Input 1', '  Input 2', '  Linear Combination', '  Activation Output', '  Is Correct'])
if not num_wrong:
    print('Nice!  You got it all correct.\n')
else:
    print('You got {} wrong.  Keep trying!\n'.format(num_wrong))
print(output_frame.to_string(index=False))
```
1) **AND** Perceptron: weights and bias ?
```
weight1 = 1.0
weight2 = 1.0
bias = -2.0
```
2) **OR** Perceptron: weights and bias ?
 - two ways to go from an AND perceptron to an OR perceptron.
   - increase the weights
   - decrease the magnitude of the bias
```
weight1 = 2.0
weight2 = 2.0
bias = -2.0

weight1 = 1.0
weight2 = 1.0
bias = -1.0
```
3) **NOT** Perceptron: weights and bias ? 
 - the NOT operation only cares about one input. 
   - The operation returns a '0' **if the input is 1**.  
   - The operation returns a '1' **if it's a 0**. 
   - The other inputs to the perceptron are ignored. If we ignore the first input, then...
```
weight1 = 0.0
weight2 = -2.0
bias = 1.0
```
4) **XOR** Multi-Layer Perceptron(cross-OR ?)
 - [**What if it's impossible to build the decision surface ?**]
   - Combine perceptions: "the output of one = the input of another one"...'Neural Network'
<img src="https://user-images.githubusercontent.com/31917400/39961747-d552235e-5634-11e8-99ce-aed8a2aae548.jpg" />




















