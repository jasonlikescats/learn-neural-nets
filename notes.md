Source material: https://www.youtube.com/playlist?list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ

# Lesson 1: Micrograd

## MLP (Multi-Layer Perceptron)
- Made up of neurons:
  - each neuron is evaluated as sum of weighted inputs plus bias: sum(w*x) + b
  - and then a non-linearity tacked onto the end to push this harder toward a clean on/off state (e.g. tanh)
- Basic idea of gradient descent in NNs is that the network is made up of differentiable functions
  - As a result, you can infer the direction and magnitude of changes made to the weights on any node
  - Forward propagation (e.g. just running through the network with an input or set of inputs) lets you evaluate how close
    you are to the expected output (via a "loss" function)
      - Loss function for classification with an MLP is something like mean-squared error (e.g. sum of diffs between actual and expected squared)
  - Backward propagation is where you modify the weights (by some pre-determined step size) based on what you know about the
    derivative of each neuron
- High level idea in code can be seen [here](https://github.com/karpathy/micrograd/tree/master/micrograd)

# Lesson 2: Makemore (pt1)
[Link](https://www.youtube.com/watch?v=PaCmpygFfXo&list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ&index=2)

## Counts model
- n-gram model that simply counts occurences of next character in training set
  - Can represent this as a n-dimensional matrix/tensor
    - e.g. bigram model (1 input char predicts 1 next char) is 2 dimensional matrix
  - Need to normalize counts to a probability matrix (so it sums to 1)
- After training, can walk through matrix with random probabilities to generate text data
- Special character can be used to denote start and end of sequence
  - e.g. in example for generating names, the `.` char can be used
- Example: name "emma" as bigrams:
  ```
  . e
  e m
  m m
  m a
  a .
  ```
- [Notebook here](https://github.com/jasonlikescats/learn-neural-nets/blob/main/text-gen.ipynb)

## Neural Net model
- In practice, should generate equivalent results to counts model
  - Unintuitive, but due to it not having any additional information as compared to counts model (i.e. same training set)
- Can use super dead simple model
  - Simply sum of weights * input) with no non-linearity or bias
  - Single layer
  - One neuron per char in trainings set (27 => 26 alpha plus start/end token)
