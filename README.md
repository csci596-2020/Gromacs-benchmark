# Project Title

Adaptive Neural Networks for electronic structure calculations.

## Abstract

Finding the exact solution to the Schrodinger equations of correlated fermionic systems has remained as a challenging problem due to the exponential growth in the dimension of the Hillbert space with the number of particles in the system. Only ground state energies of small molecules have been solved exactly (to chemical accuracy). Due to the Universal approximation theorem (Cybenko, 89; Hornik, 91) which states that A feedforward neural network with a single hidden layer can approximate any continuous functions, machine learning has emerged as a promissing tool to study complex fermionic systems. In the paper "Solving the quantum many-body problem with artificial neural networks" [1], Carleo et al shows that the same Restricted Boltzmann Machine can be used to represent the wavefunction for both Ising and Heisenberg models with high accuray. Also, in the paper "Machine learning phases of matter" [2], Juan et al shows that the neural network trained on a square-lattice ferromagnetic Ising model can surprisingly provide accurate prediction for triangular lattice. The evidence puts the question: How universal a neural network can actually be? In particular, the goal of this project is to  train an adaptive neural network which can be used to approximate the ground state energies and the wave functions for real physics system like small molecules to chemical accuracy. 

## Hypothesis
A well-trained adaptive neural network can be used universally to approximate the wavefunctions of small molecules to chemical accuracy (~ 1kcal/mol). 

## Methodology
<figure>
  <img src="https://github.com/hoatrinhusc/Adaptive-Neural-Networks-for-electronic-structure-calculation./blob/master/p3.png" alt="the picture is adopted from [5]"/>
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
