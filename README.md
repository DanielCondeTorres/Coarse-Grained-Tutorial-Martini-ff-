# Coarse-Grain-Tutorial
This is a short tutorial on how to perform a peptide-membrane interaction simulation using the Martini force field, together with the Gromacs package.

<p align="center">
  <img src="https://user-images.githubusercontent.com/117435891/199940424-2ad7347e-bbcb-4425-bfc6-bb7a3fca7413.gif" alt="animated"  />
</p>

# Getting started
The first step is to create our simulation box, which will have the following study system:

- Membrane simulating: bacteria (10% POPG and 90% POPE).
- Magainin-2 ETP

The membrane can be created directly with the free software [Charmm-gui](https://www.charmm-gui.org/), all you need to do is register. However, to save time I have moved the work forward and we will be able to download it directly from this repository at the following link:

Magainin-2 will obtain its atomistic representation from the [Protein Data Bank](https://www.rcsb.org/structure/2MAG), if someone is lost, you can get the pdb directly from this repository.
# Load modules that are needed to run and visualize the simulation
In order to use [Gromacs package](https://www.gromacs.org/) 

```
module load gcc/system openmpi/4.0.5 gromacs/2021-PLUMED-2.7.1 mdanalysis/1.1.1
```
and in order to visualize the systems we will use [VMD](https://www.ks.uiuc.edu/Research/vmd/):

```
module load vmd
```
# Atomistic to Coarse-Grain resolution

In this case the representation to be used will be Coarse-Grained, where instead of representing all the atoms in an explicit way we group them in a structure called 'bead' that groups four of these atoms. This way we reduce the number of particles in the system and we can perform computational simulations of larger systems because the computational cost is lower.

To begin with we will use the [Martini] (http://www.cgmartini.nl/force) field, as it allows us to perform this type of simulations, our membrane is already in CG resolution, to transform the peptide (atomistic resolution) to CG we can use the python script provided in Martini's own web page: marinize.py


```
python3 martinize.py -f 2mag(3).pdb -ss HHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHHH -x MAG_CG.pdb -o topol.top -merge all
```
- -ss indicates the secondary structure that we want, in this casa \alpha helix 
