# Adaptive_sampling_for_multi-profile

To replicate the simulation result, one just needs to run the `Int_simulation.R` file. We mainly use the `MASS` and `splines` packages, and also use the `source` function to access the other R files.

## Interpret the Result

The output of the simulation is based on a partial shift pattern. The output from `Model1_simulation.R` corresponds to Fig. 2(a), and `Model2_simulation.R` corresponds to Fig. 2(b). Together, they complete Fig. 2 in the manuscript.

The output will include 6 subplots (3 columns corresponding to available resources r = 8, 6, 4). Each subplot has five lines corresponding to the proposed method, FPCA, and FPCA with Δ = 0.01, 0.05, and 0.1.

The x-axis shows mu-shifts of 0.7, 1.0, 1.4, 2.1, and 2.8, and the y-axis shows the corresponding ARL results. A table of ARL₁ values is also generated in the variable `out_se`, where ARL₁ values are in every odd row and standard errors are in every even row (corresponding to Table A1 in the appendix).

## Modify the Simulation

To change the simulation settings, go to `Model1_simulation.R` and `Model2_simulation.R`. You can switch from partial shift to full shift by editing lines 75–85.

In the demo code, only 100 repetitions are used for estimating ARL to demonstrate functionality (running time is about 1 hour depending on your device). In the actual simulation, 500 repetitions were used.

To increase the number of trials, edit lines 64–70 and 134–138 by changing the loop for `oc_run1` through `oc_run5`.

## Detailed File Layout and Functions

The `Demo` folder contains the following 6 files:

1. **top_delta_ARL.R**: Includes methods required for ARL₁ for FPCA with Δ = 0.01, 0.1, 0.5  
   For FPCA with delta:
   - `ARLi_init_delta`: helper function to initiate CUSUM chart  
   - `Get_ARLi_delta`: get running length  
   - `df_hist_delta`: estimate control limit L  
   - `cusum_df_delta`: helper function for redistribution  

2. **fpca_ARL.R**: Includes methods required for ARL₁ for FPCA chart  
   For FPCA:
   - `dpca_score`: calculate FPC scores from a profile  
   - `dpca_est`: estimate FPCA model and parameters  
   - `ARLi_initial`: helper function to initiate CUSUM chart  
   - `Get_ARLi`: get running length  
   - `df_hist`: estimate control limit L  
   - `cusum_df`: helper function for redistribution  

3. **mfpca_ARL.R**: Includes methods required for ARL₁ for the proposed method  
   For the proposed method:
   - `mfpca_score`: calculate MFPC scores from multi-profile samples  
   - `mfpca_est`: estimate MFPCA model and parameters  
   - `ARL_initial`: initiate CUSUM chart  
   - `Get_ARL`: get running length  
   - `mf_hist`: estimate control limit L  
   - `cusum_stage`: helper function for redistribution  

4. **control limits train.R**  
   - `L_train`: tunes the control limits for all methods  

5. **Model1_simulation.R**  
   - Runs the simulation for Model I (Partial shift)  

6. **Model2_simulation.R**  
   - Runs the simulation for Model II (Partial shift)  

## Reference

The detailed implementation is described in the following paper:  
https://www.tandfonline.com/doi/abs/10.1080/00401706.2023.2166125

## Data for Case Study

https://www.kaggle.com/datasets/podsyp/production-quality?select=data_X.csv

## Citation

If you find this work useful, please consider citing:

```bibtex
@article{yao2023adaptive,
  title={Adaptive sampling for monitoring multi-profile data with within-and-between profile correlation},
  author={Yao, Jinwei and Xian, Xiaochen and Wang, Chao},
  journal={Technometrics},
  volume={65},
  number={3},
  pages={375--387},
  year={2023},
  publisher={Taylor \& Francis}
}


