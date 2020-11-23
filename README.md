# Project Title

Gromacs benhmarking

## Gromacs introduction

## Discovery cluster introduction

## Methodology
1. Strong scaling of OpenMP

Intel(R) Xeon(R) Gold 6130 CPU @ 2.10GHz
<figure>
  <img src="https://github.com/hoatrinhusc/Gromacs-benchmark/blob/main/1MPI-OpenMP.png"/>
</figure>

Modern computers have a limited number of threads, but even if the number of threads are unlimited, we don't gain speed up due to strong scaling.

2. Solution: MPI to connect different computing nodes, the price is the communication between MPI ranks

Study the cost of MPI communication
<figure>
  <img src="https://github.com/hoatrinhusc/Gromacs-benchmark/blob/main/MPI_PME.png"/>
</figure>



