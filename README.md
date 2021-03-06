# polgrad-multinoise

## Policy gradient methods for linear systems with multiplicative noise

The code in this repository implements the algorithms and ideas from our two papers:
* [Learning robust control for LQR systems with multiplicative noise via policy gradient](https://arxiv.org/) TBD
* [Sparse optimal control of networks with multiplicative noise via policy gradient](https://arxiv.org/) TBD


## Dependencies
* Python 3.5+ (tested with 3.7.3)
* NumPy
* SciPy
* Matplotlib

## Installing
Currently there is no formal package installation procedure; simply download this repository and run the Python files.

## Examples
There are several example Python files which can be run.

### example_basic.py

Use this file as a "Hello world" for this repository. The program should perform proximal gradient optimization of a small 3-state, 2-input system with multiplicative noise. The program should run for 1000 iterations then terminate and print two gain matrices. The output should be:

```
Iteration | Stop quant / threshold |  Curr obj |  Best obj | Norm of gain delta | Stepsize  | Sparsity
     1000 |  2.405e+00 / 6.000e-02 | 6.004e+00 | 6.004e+00 |          1.609e-06 | 1.000e-03 |  33.33%
Max iterations exceeded, stopping optimization
Policy gradient descent optimization completed after 999 iterations, 1.736 seconds
Optimized sparse gains
[[-0.08948389 -0.22821676 -0.1576331 ]
 [ 0.23967029  0.          0.        ]]
Riccati gains
[[-0.20997456 -0.32374004 -0.31804207]
 [ 0.3765947  -0.07048691  0.14067572]]
 ```


### example_suspension_model_known.py

This file reflects the model-known algorithms which calculate gradients
by solving generalized Lyapunov equations. The standard gradient is used with an
appropriate step size and the optimization terminates when the Frobenius norm
of the gradient falls below a threshold. The system represented is a 4-state,
1-input system with multiplicative noise as described in the paper. Both high
and zero multiplicative noise settings are optimized and the iterates recorded.
Running the routine_gen() function will perform the entire experiment,
while running the routine_load() function will attempt to load existing
experiment result data and generate the plots used in Figure 1 of the main paper.


### example_random_model_known.py

This file reflects the model-known algorithms which calculate gradients
by solving generalized Lyapunov equations. The standard gradient, natural 
gradient, and Gauss-Newton step directions are used with appropriate step sizes
and fixed number of iterations.
Running the routine_gen() function will perform the entire experiment,
while running the routine_load() function will attempt to load existing
experiment result data and generate the plots used in Figure 2 of the main paper.


### example_model_free.py

This file reflects the model-free algorithm which estimates gradients via 
zeroth-order optimization. This code is meant to simply give an idea how the 
algorithm works - the number of sample trajectories needed to estimate the 
gradient to the accuracy limit given in the paper is quite high and might take
a very long time to run, even for a small system. This code does not correspond
to any figure or numerical result given in the main paper.

### example_sparse.py

This file reflects the sparse gain design procedures. Running this script will perform a "sparsity traversal" which iteratively increases the regularization weight in order to find increasingly sparse optimal gains.


## General code structure
Linear time-invariant (LTI) systems are represented by a simple class. For solving linear-quadratic regulator (LQR) optimal control problems additional attributes and methods are provided. Likewise, multiplicative noise is handled by additional attributes and methods. These class definitions are in ltimult.py. Random systems can be generated by the functions in ltimultgen.py. Policy gradient can be performed using policygradient.py.


## Authors
* **Ben Gravell** - [UTDallas](http://www.utdallas.edu/~tyler.summers/)
* **Yi Guo** - [UTDallas](http://www.utdallas.edu/~tyler.summers/)
* **Peyman Esfahani** - [TUDelft](http://www.dcsc.tudelft.nl/~mohajerin/)
* **Tyler Summers** - [UTDallas](http://www.utdallas.edu/~tyler.summers/)
