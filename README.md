# CS 323 - Project 4: Secret Sharing
Author: Bach Nguyen

This contains the code and analysis for **Project 4: Secret Sharing** for the course CS 323: Data Privacy

## Project Overview

This project implements and benchmarks secure mean computation methods using **Paillier Homomorphic Encryption** and **Shamir’s Secret Sharing (SSS)** as well as **Differential Privacy**. The goal is to evaluate the computational efficiency of different privacy-preserving approaches compared to a non-encrypted baseline alongside an implementation of differential privacy. The analysis measures runtime performance and accuracy across varying data sizes ($n$) to assess scalability and computational cost. All experiments were conducted under consistent parameter settings, with Paillier encryption using a fixed key pair, Shamir’s scheme configured with a constant party count and threshold, and Differential Privacy with a fixed privacy cost of $1.0$.

## Project Structure 
The project consists of 3 files (including this README):
- __cs323_project_4.ipnyb__: The main Jupyter Notebook that contains all of the code needed to run this project.

Additional Files:
- __requirements.txt__: Text file containing names of non-native Python libraries needed to run the code

## How to run the Code

1. Library Installation

In addition to native Python libraries, we are using some additional Python libraries, so please make sure that you got the following libraries installed: **pandas**, **numpy**, **matplotlib**, **phe**, and **pycryptodome**

You can check if you have them installed or not by typing the following command line into your terminal:
```python
pip install pandas numpy matplotlib phe pycryptodome
```
Or you can use the __requirements.txt__ file:
```python
pip install -r requirements.txt
```
If you don't have the mentioned libraries installed, the system will install them for you.

2. Run all of the Notebook Cells
   
3. Inspect the Output
Results are printed directly in the notebook.

## Major Design Decisions

**Consistent Randomized Input Generation**
- All methods (Baseline - no encryption, Paillier, Shamir, and Differential Privacy) operate on the same randomly generated integer dataset for each sample size $n$. Values are drawn uniformly between predefined minimum and maximum bounds. A fixed random seed is set before each run to ensure reproducibility of results and consistency across experiments. This ensures every method processes identical input data for fair performance comparison.

**Dynamic Cryptographic Parameters**

Paillier encryption uses a single 3072-bit key pair for all tests to ensure consistent encryption and decryption overhead across varying dataset sizes.
Shamir’s Secret Sharing dynamically adjusts parameters per dataset size:
- The number of parties equals the dataset size ($n$)
- The reconstruction threshold is set to $t=⌊n/2⌋$
- A fixed 3072-bit prime $p$ is generated for share computation

**Differential Privacy Implementation**
- The Differential Privacy (DP) approach applies the Laplace mechanism with a fixed privacy budget of ($\epsilon = 1.0$) and with public knowledge of $n$.
- The computation first performs a standard (non-private) sum of the dataset, then adds Laplace noise calibrated to the global sensitivity of the query before averaging. This implementation guarantees that privacy loss is bounded by $\epsilon = 1.0$