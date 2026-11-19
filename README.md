Attacks Detector using Kernel Functional Subspaces Theory

** kernel-embedded functional subspace detector (KEFSD) **

** Implementation was done in MATLAB R2024a and requires matpower**

** Author: Andrew Omiloli ** Date: 6/16/2026

    Generate clean residuals (attack free) from estimator or physical plant modelled in Simulink and save as mat file e.g 'residual_nominal.mat'

        comment the detector, attack input and run the model 'Model_with_Detector.slx' to generate the clean residuals

    Set number of training samples (n) and number of functional basis elements (n_basis) in the run file, 'Run_file.m' > n = 200; n_basis = 20;

        Note: n_basis <= n

    Set window length (Window), thresholds (tau_KEFSD and tau_norm) in 'Run_file.m' > Window = 20; > tau_KEFSD = 0.03 > tau_norm = 0.01;

        Note1: 'tau_norm' is the 2norm residual detector used before window samples is full while 'tau_KEFSD' is the threshold used after full window samples Note2: These thresholds should be tuned for each system to obtain reasonable detector performance metrics

    Optional: Other parameters used for learning the principal functional basis elements can be changed in the run file, for example > gamma_min = 1e-6 > gamma_max = 10 > n_gamma = 30 > lambda_pca = 1e-3

    Run the file 'Run_file.m'

    open the model 'Model_with_Detector.slx' and uncomment the detector blocks and attack blocks and click run, if successfully run, the following signals gets logged in the workspace
    > detector_output > alarm > ground_truth

        Note1: the attacks should be enabled at x duty cycle.

    Run the file 'Detector_Performance.m' to see detector performance scores, if undesirable, change thresholds to improve performance

%% How to tune thresholds

    Test with random attacks enabled at x duty cycle
    Examine the detector output signal at the region the detector energy flattens
    Choose desired threshold before the flat occurs
    Update thresholds in 'Run_file.m' and click run
    Run 'Detector_Performance.m'
    Repeat as necessary.
