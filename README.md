# Project Title

Adaptive Neural Networks for electronic structure calculations.

## Abstract


## Methodology
<figure>
  <img src="https://github.com/hoatrinhusc/Gromacs-benchmark/blob/main/1MPI-OpenMP.png"/>
</figure>

[The figure is adopted from [5]](https://www.nature.com/articles/s41467-018-07520-3)

* A deep neural network which is similar to the one in [5] will be built. In particular, the wave function will be represented as an exponential of the neural network parameters (i.e, weight and bias) and the input spin quantum numbers, sigma_z, which can be either +1 or -1.
* To take into account the sign problem of fermionic systems [4], an addditional layer will be added as described in [3].
* Write the Hamiltonian of molecules in second quantization, then use Bravyi-Kiteav transformation to convert creation and annihilation operators to Pauli operators.
* Once we have Hamiltonian in Pauli-operator forms, we can use the same strategy as Variational Quantum Monte Carlo method to estimate the Expectation value of energy corresponding to the wave function described by our neural network. Sampling the wave function can be used by Metropolis technique or by quantum computers as proposed recently [3].
* Stochastic gradient descent or other optimization methods will be used to optimize the parameters of the neural network.
* Nodes within a layer will be selectively active to adapt with feedback from calculation of energy with respect to a set of network parameter.
* The neural network will be implemented by using TensorFlow.

## Initial Calculations
- Use the software OpenFermion to transfrom the Hamiltonian of H2 molecule to the spin form. Results obtained:
![alt text](https://github.com/hoatrinhusc/Adaptive-Neural-Networks-for-electronic-structure-calculation./blob/master/p1.png)

- Use the method discribed in [7] to rewrite the above Hamiltonian in sigma_z form and then solve the equation by searching over all possible solutions. The energy surface of H2 molecule obtain by this method agrees very well with Full-configuration-interaction calculation done by using the software OpenFermion 
![alt text](https://github.com/hoatrinhusc/Adaptive-Neural-Networks-for-electronic-structure-calculation./blob/master/p2.png)

## Future work and expected results
The next step is to test the sigma_z Hamiltonain of H2 molecules with the neural networks described in [1]. The authors have made the code available on Github. 
I expected that the neural network will not be able to solve energy surface for molecules and further modifications are needed. 

## Author

Hoa Trinh

## Reference

[1] Solving the quantum many-body problem with artificial neural networks, Carleo et al, Science 355, 602-606(2017) <br />
[2] Machine learning phases of matter, Juan et al, Nature Physics, Vol 12 (2017) <br />
[3] Quantum machine learning for electronic structure calculations, Rongxin et al, Nature Communication (2018) <br />
[4] Computational Complexity and Fundamental Limitations to Fermionic Quantum Monte Carlo Simulations, Troyer et al, Physical Review Letters (2005) <br />
[5] Constructing exact representations of quantum many-body systems with deep neural networks, Carleo, et al, Nature Communication (2018) <br />
[6] Electronic Structure Calculations and the Ising Hamiltonian, Rongxin Xia et al, The Journal of Physical Chemistry (2017)
