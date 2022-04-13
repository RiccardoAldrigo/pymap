# pymap

A program for describing how different selections of *N* out of *n* degrees of freedom (mappings) affect the amount of information retained about a full data set.

Three quantities are calculated for each low-resolution representation, namely the mapping entropy:

![equ](https://latex.codecogs.com/gif.latex?S_{map}&space;=&space;\sum_{\phi}p(\phi)&space;\ln\left(\frac{p(\phi)}{\overline{p(\phi)}}&space;\right))

the resolution:

![equ](https://latex.codecogs.com/gif.latex?H_{s}&space;=&space;-\sum_{\phi}p(\phi)&space;\ln\left(p(\phi)\right))

and the relevance:

![equ](https://latex.codecogs.com/gif.latex?H_{k}&space;=&space;-\sum_{K}p(k)\ln\left(p(k)\right).)

where K is the set of unique frequencies observed in the sample.

If you use pymap please cite [this paper](https://arxiv.org/abs/2203.00100).


# Setup

A minimal conda environment (see [here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)) to run the calculations can be generated from the .yml file pymap.yml using the following command:

```
conda env create --file pymap.yml
```

Once the environment is correctly created, it must be activated via:

```
conda activate pymap
```

# Testing

Pytest is employed to test the correct installation of pymap. In order to do so, run the following command from the main directory:

```
python -m pytest tests
```

# Usage

The program must be provided with two mandatory command line arguments, namely 1) a (relative) path to a data set 2) a (relative) path to the desired output file. A third, optional argument, *max_binom*, can be given to pymap, specifying the maximum number of mappings that must be generated for each degree of coarse-graining. The default choice is to generate all the coarse-grained mappings for each *N*, a task that becomes prohibitive when *n > 15*. Verbosity can be turned on with the *-v* (*--verbose*) flag. In general, running

```
python pymap -h
```

shows the available command line arguments.

## non-interacting spin system

The first data set described in [this article](https://arxiv.org/abs/2203.00100) contains 20 non-interacting spins. The variables of interest can be calculated with the following command

```
python3 pymap.py data/spins.csv results/results_spins.csv
```

In this context, the mapping space is quite big, and *max_binom* allows one to explore just a portion of it in few minutes: 

```
python3 pymap.py data/spins.csv results/results_spins_m5.csv --max_binom 5
```

## financial market

To obtain the full results for the simple model of the Nasdaq stock market reported [here](https://arxiv.org/abs/2203.00100) one can use the following command:

```
python3 pymap.py data/m1.csv results/results_m1.csv
```

and 

```
python3 pymap.py data/m2.csv results/results_m2.csv
```
