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

As a study case of MPI communication cost, I consider 20 MPI processes, each MPI process is on a different computing node of xeon-2640v4. 1 OpenMP thread per rank. Then, I varies the number of MPI ranks dedicated for PME work and benchmark MD performance.
<figure>
  <img src="https://github.com/hoatrinhusc/Gromacs-benchmark/blob/main/MPI_PME_xeonv4.png"/>
</figure>

The table below breaks down the computing cost into the cost of each major component ( each accounts for more than 2% of total wall-clock time) . The cost is measured in the total Sum of Giga-Cycles.


| Computing  | 20MPI-0PME | 20MPI-4PME |  20MPI-10PME |
| ------------- | ------------- | ------------- | ------------- |
| Domain decomp. | 72.341  | 48.588 | 40.588 |
| Neighbor search  | 84.652 | 69.198 | 72.632 |
|  Comm. coord. | 297.054 | 207.974 | 148.992 |
| Force | 1887.417 | 1824.295 | 1735.850 |
| Wait + Comm. F | 299.149 | 356.349 | 197.719 |
| PME mesh | 2105.949 | 645.770 | 1136.321 |
| PME wait for PP | 0 | 100.144 | 1219.859 |
| Wait + Recv. PME F | 0 | 288.256 | 7.370 |



