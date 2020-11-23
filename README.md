# Project Title : Gromacs benchmarking

## Gromacs introduction
https://zenodo.org/record/3923644#.X7vessKIYaw

## Discovery cluster introduction
https://carc.usc.edu/user-information/user-guides/high-performance-computing/discovery-resources?fbclid=IwAR3nNkJvUiTvLwBNyOsBtJD01cyuoDreeLG_GDIC-bAOSSrno6xCo_CvSMY

## Methodology
Study system: TRP-Cage, a protein with only 20 amino acids (PDB ID = 1L2Y).
<figure>
  <img src="https://github.com/hoatrinhusc/Gromacs-benchmark/blob/main/trp_vmd.png"/>
</figure>


Using Gromacs version 2020.3 installed on Discovery cluster.

| MD System  | Trp-Cage |
| ------------- | ------------- |
| # atoms | 3809  |
| System size (nm)  |  3.39x3.39x3.39 |
| Time step (fs) | 2 |
| Cut-off radii(nm) | 1 |
| PME grid spacing(nm) | 0.16 |
| Neighbor searching frequency | 10|
| Benchmark steps | 500000 |


**1. Strong scaling of OpenMP**

Intel(R) Xeon(R) Gold 6130 CPU @ 2.10GHz
<figure>
  <img src="https://github.com/hoatrinhusc/Gromacs-benchmark/blob/main/1MPI-OpenMP.png"/>
</figure>

Modern computers have a limited number of threads, but even if the number of threads are unlimited, we don't gain speed up due to strong scaling.

**2. MPI as a solution**

To overcome strong scaling of OpenMP and gain speed up, MPI is used to connect different computing nodes. However, the price is the communication between MPI processes.

Gromacs uses the particle-mesh Ewald (PME) algorithms to treat the long-ranged component of the non-bonded interaction. Because the algorithm uses a 3D FFT that requires global communication, its parallel efficiency gets worse as more ranks participate. 

To study the cost of MPI communication, I varies the number of MPI ranks dedicated for PME work and benchmark the cost of PME calculation.

| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |


As a study case, I consider 20 MPI processes, each MPI process is on a different computing node. 
<figure>
  <img src="https://github.com/hoatrinhusc/Gromacs-benchmark/blob/main/MPI_PME.png"/>
</figure>



