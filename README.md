# CS 323 - Project 3: Secret Sharing
Author: Bach Nguyen

This contains the code and analysis for **Project 3: Secret Sharing** for the course CS 323: Data Privacy

## Project Overview

This project implements and benchmarks secure mean computation methods using **Paillier Homomorphic Encryption** and **Shamir’s Secret Sharing (SSS)**. The goal is to evaluate the computational efficiency of different privacy-preserving approaches compared to a non-encrypted baseline. The analysis measures runtime performance across varying data sizes ($n$) to assess scalability and computational cost. All experiments were conducted under consistent parameter settings, with Paillier encryption using a fixed key pair and Shamir’s scheme configured with a constant party count and threshold.

## Project Structure 
The project consists of 3 files (including this README):
- __cs323_project_3.ipnyb__: The main Jupyter Notebook that contains all of the code needed to run this project.

Additional Files:
- __requirements.txt__: Text file containing names of non-native Python libraries needed to run the code

## How to run the Code

1. Library Installation

In addition to native Python libraries, we are using some additional Python libraries, so please make sure that you got the following libraries installed: **pandas**, **numpy**, **phe**, and **matplotlib**

You can check if you have them installed or not by typing the following command line into your terminal:
```python
pip install pandas numpy phe matplotlib
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
All methods (Baseline - no encryption, Paillier, and Shamir) operate on the same randomly generated integer dataset for each sample size $n$. Values are drawn uniformly between predefined minimum and maximum bounds. A fixed random seed is set before each run to ensure reproducibility of results and consistency across experiments. This ensures every method processes identical input data for fair performance comparison.

**Dynamic Cryptographic Parameters**
Paillier encryption uses a single 3072-bit key pair for all tests to ensure consistent encryption and decryption overhead across varying dataset sizes.
Shamir’s Secret Sharing dynamically adjusts parameters per dataset size:
- The number of parties equals the dataset size ($n$)
- The reconstruction threshold is set to $t=⌊n/2⌋$
- A fixed 3072-bit prime $p$ is generated for share computation