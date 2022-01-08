# Mixed Integer Quadratic Programming

# Objective
Model selection and feature selection play a significant role in developing an optimized model that can capture the true signal while achieving low bias. There are multiple ways to implement feature selection. One way to implement this requirement is to *model this whole problem into an optimization problem and use Gurobi to solve that problem*.

# Gurobi - MIQP
The feature selection problem can be modelled in the form of Mixed Integer Quadratic Programming problem. First, let's look at the objective function in matrix format:

<img width="656" alt="image" src="https://user-images.githubusercontent.com/12545194/148633263-27b32d28-606a-4342-bdcb-87cf9b943478.png">

The mixed integer quadratic problem can be modelled in the following manner:

<img width="408" alt="image" src="https://user-images.githubusercontent.com/12545194/148633284-763cddd5-5e31-440f-bdf2-426606c0df67.png">

* The first equation represents the objective function that should be minimized.
* To implement the feature selection, a new set of decision variables has been added – zj , which can take on the value 0 or 1 (binary variable) indicates whether the feature j was selected in the model. The sum of all values of  zj is constrained to reflect the total number of variables to be allowed in the optimization. Thus, βj should be equal to zero if jth feature is not picked. In other words, βj should be zero if zj is 0. This constraint has been implemented using big M technique (equation 2 illustrates the same). Based on hit and trial methods an M value of 20 was chosen. Please refer to the code snippet below for example.

# Comparison between sklearn and Gurobi Model
* The number of features picked by lasso regression is greater than the Gurobi model (k=10). 
* In comparison to sklearn’s lasso regression (Test MSE = 2.36), *the model created by Gurobi’s is performing almost similar, if not better* (Test MSE = 2.34). 

This could be simply due to the fact at the gurobi model’s has fewer variables in comparison to lasso model. The fewer number of variables might be preventing the model from overfitting and reducing the variance of model. 
