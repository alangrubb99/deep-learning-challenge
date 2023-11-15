Alphabet Soup Charity Optimization

Overview of the analysis:

The nonprofit foundation Alphabet Soup wants a tool that can help it select the applicants for funding with the best chance of success in their ventures. From Alphabet Soup’s business team, we have received a CSV containing more than 34,000 organizations that have received funding from Alphabet Soup over the years.

The features in the provided dataset will be used to create a binary classifier that can predict whether applicants will be successful if funded by Alphabet Soup.

Data Preprocessing

What variable(s) are the target(s) for your model?

The output of the binary model is an accuracy between 0 and 1, representing probability an applicant will be successsful.
A random coin flip would be a .5 accuracy, for example.   The exercise is asking for an accuracy of at least .75.


What variable(s) are the features for your model?

    * EIN and NAME—Identification columns
    * APPLICATION_TYPE—Alphabet Soup application type
    * AFFILIATION—Affiliated sector of industry
    * CLASSIFICATION—Government organization classification
    * USE_CASE—Use case for funding
    * ORGANIZATION—Organization type
    * STATUS—Active status
    * INCOME_AMT—Income classification
    * SPECIAL_CONSIDERATIONS—Special considerations for application
    * ASK_AMT—Funding amount requested
    * IS_SUCCESSFUL—Was the money used effectively

What variable(s) should be removed from the input data because they are neither targets nor features?

EIN and NAME were removed from the initial model.  NAME was later binned in The Alphabet_Soup_Optimized model to increase the 
model's performance, as follows:

                    Other                                           20043
                    PARENT BOOSTER USA INC                           1260
                    TOPS CLUB INC                                     765
                    UNITED STATES BOWLING CONGRESS INC                700
                    WASHINGTON STATE UNIVERSITY                       492
                                                ...  
                    HABITAT FOR HUMANITY INTERNATIONAL                  6
                    DAMAGE PREVENTION COUNCIL OF TEXAS                  6
                    FLEET RESERVE ASSOCIATION                           6
                    HUGH OBRIAN YOUTH LEADERSHIP                        6
                    INTERNATIONAL CONGRESS OF CHURCHES MINISTERS        6
                    Name: NAME, Length: 355, dtype: int64


Compiling, Training, and Evaluating the Model

How many neurons, layers, and activation functions did you select for your neural network model, and why?

Introduction to activation functions:

The idea of activation functions is derived from the neuron-based model of the human brain.  
In the artificial neural network, we have artificial neurons which are nothing but a mathematical unit consisting of
the activation function. It also fires the output based on certain inputs received by the previous neuron.

In this sequential model we used The ReLu activation function which is computationally efficient.  It enables 
networks to converge faster during the training phase. It is both non-linear and differentiable which are good 
characteristics for an activation function.

In the output layer we used The Sigmoid Activation layer of Keras, the formula of Sigmoid
     sigmoid(x) = 1/ (1 + exp(-x))
The sigmoid activation function produces results in the range of 0 to 1 which is interpreted as the probability.
It is a good choice for the output layer for binary classification.

We used dense layers in our hidden layers. Each neuron in the dense layer receives input from all neurons of its 
previous layer. The dense layer is the most commonly used type of hidden layer.

In our original model: Alphabet_Soup.ipynb, we used 2 hidden dense layers and units = 2, and units = 3, 
resulting in an accuracy score below .7.  The same model was then modified to use 3 hidden layers with 
units = 2, 3, and 4.  This version had an accuracy of .7249.  This was still below the .75 requirement
so a new notebook: Alphabet_Soup_Optimized.ipynb was created.

Were you able to achieve the target model performance?  Yes the new model, Alphabet_Soup_Optimized.ipynb,
achieved an accuracy score of .7936.

 Alphabet_Soup_Optimized.ipynb, model accuracy:

    268/268 - 0s - loss: 0.4546 - accuracy: 0.7936 - 345ms/epoch - 1ms/step
    Loss: 0.4546079635620117, Accuracy: 0.793586015701294

What steps did you take in your attempts to increase model performance?

The steps were as follows:
1. Instead of deleting the NAME feature, we binned it for values <= 5.
2. Changed hidden_layer1 to 80 units and hidden_layer2 to 30 units.
3. Left hidden layer 3 at 4 units.
4. Epoch was left at 50.   Tried 100 and it made very little difference.
5. Code was cleaned up to use variables instead of hard coding in the binning and model input sections.

Summary: Summarize the overall results of the deep learning model. Include a recommendation for how a different model could solve this classification problem, and then explain your recommendation.

We recommend use of our optimized model with almost .8 probability for selecting funding.  This is much better
than the probability of .5 without using the model.

We also reeommenbd that we run a model allowing kerastuner to decide number of hidden layers and neurons in hidden layers to
determine if we can improve on our model.

The Random Forest Model could help solve the problem. Random forest is a flexible, easy-to-use machine learning algorithm that produces, without hyper-parameter tuning, a great result most of the time. It is also one of the most-used algorithms, due to its simplicity and diversity.  It is also a good model for binary classification.
