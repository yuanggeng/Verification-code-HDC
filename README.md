# Verification-code-for-bridging-gap

# Step-by-step instructions to reproduce the paper "Bridging dimensions: confident reachability for high-dimensional controllers"


## Case study 1: Inverted pendulum

To run the the single inverted pendulum case study:
* Step 1: we enter into the corresponding inverted pendulum folder to start. 

Open command window from root: 

```python
cd /home/ubuntu/POLAR_Tool/ARCH-COMP22/Single_Pendulum
```
Activate our virtual environment that contains all the packages and dependencies.

```
source ~/venv/bin/activate
```

* Step 2: Calculate the two types of statistical discrepancies: action- and trajectory-based discrepancy.

```
python calculate_discrepancy_NoNoise.py 95
```

The 95 means that this code returns the perfect mapping discrepancies with 95% confidence.

```
python calculate_discrepancy_Noise.py 95
```

This code returns noise-mapping statistical discrepancy results with 95% confidence. In our case, we have two standard deviations 0.1, 0.01 zero-mean Gaussian noise added into the mapping.

* Step 3: Run the reachability analysis with two types of discrepancies.
  
This is the core part of our paper, where the overall verification takes more than 50 hours on our initial set. Therefore, we recommend committee run reachability analysis on a subset of our initial set, namely [1, 1.2]x[-1.2, 1],

This is the command for nosied mapping for action-based discrepancy, which takes a couple of minutes.
```
make && ./single_pendulum 1 1.2 -1.2 1
```

This is the command for nosied mapping for trajectory-based discrepancy, which takes a couple of minutes.
```
make && ./single_pendulum_noised_traj 1 1.2 -1.2 1
```

This is the command for perfect mapping for action-based discrepancy, which takes a couple of minutes.
```
make && ./single_pendulum_perfect_action 1 1.2 -1.2 1
```

This is the command for perfect mapping for trajectory-based discrepancy, which takes a couple of minutes.
```
make && ./single_pendulum_perfect_traj 1 1.2 -1.2 1
```

(Optional) If you want to run the verification on the whole initial set [0,2]x[-2,0], you can simply change the initial set by typing, make && ./single_pendulum 0 2 -2 0


The results will be in the folder outputs



* Step 4: Calculate the confusion matrix for both perfect mapping and noised mapping. 

```
python confusion_matrix.py
```
These are the final results that match the Table 1 "Inverted pendulum (IP)" part in the paper. More details will be displayed in the command window.

```
python confusion_matrix_noised.py
```
These are the final results that match the Table 2 "Inverted pendulum (IP)" part in the paper. More details will be displayed in the command window.

Then you can close the command window.

If there is a very tiny deviation from our paper (e.g., true positive rate from 0.4662 to 0.4665), that's because we don't sample exactly the same points every time, which could cause a tiny deviation in discrepancies. But this is acceptable.

## Case study 2: Mountain car
Next, open another new command window from the root. 

* Step 1: Enter into the correct folder:
```
cd /home/ubuntu/POLAR_Tool/examples/Mountain_Car
```
and then activate the same environment:
```
source ~/venv/bin/activate
```

* Step 2: Calculate two types of statistical discrepancies: action- and trajectory-based discrepancy.

```
python MC_calculate_discrepancy_NoNoise.py 95
```

The 95 means that this code returns the perfect mapping discrepancies with 95% confidence.

```
python MC_calculate_discrepancy_Noise.py 95
```

This code returns noised mapping statistical discrepancy results with 95% confidence. In our case, we have two standard deviations 0.01, 0.1 zero-mean Gaussian noise added into the mapping

* Step 3: Run the Reachability analysis with two types of statistical discrepancies.
  
This is the core part of our paper, where the overall verification takes more than 40 hours on the whole initial set. Therefore, we recommend committee run reachability analysis on a subset of our initial set, namely [-0.6 -0.58] x [0.01 0.015],

This is the command for nosied mapping for action-based discrepancy, which takes approximately 10 minutes.
```
make && ./mountain_car 0.6 -0.58 0.01 0.015
```

This is the command for nosied mapping for the trajectory-based discrepancy, which takes 10 approximately minutes.
```
make && ./mountain_car_noised_traj 0.6 -0.58 0.01 0.015
```

This is the command for perfect mapping for action-based discrepancy, which takes approximately 10 minutes.
```
make && ./mountain_car_perfect_act 0.6 -0.58 0.01 0.015
```

This is the command for perfect mapping for trajectory-based discrepancy, which takes approximately 10 minutes.
```
make && ./mountain_car_perfect_traj 0.6 -0.58 0.01 0.015
```

(Optional) If you want to run the verification on the whole initial set [-0.6 -0.4] x [-0.02, 0.05], you can simply change the initial set by typing, make && ./single_pendulum -0.6 -0.4 -0.02, 0.05


The results will be in the folder outputs.

* Step 4: Calculate the confusion matrix for both perfect mapping and noised mapping.

```
python MC_confusion_matrix.py
```
These are the final results that match the Table 1 "Mountain Car (MC)" part in the paper. More details assisting you to compare will be displayed in the command window.
```
python MC_confusion_matrix_noised.py
```
These are the final results that match the Table 2 "Mountain Car (MC)" part in the paper. More details will be displayed in the command window.

Then you can close the command window.

If there is a very tiny deviation from our paper (e.g., true positive rate from 0.7225 to 0.7220), that's because we don't sample exactly the same points every time, which could cause a tiny deviation in discrepancies. But this is acceptable.

## Case study 3: Cartpole
Next, open another new command window in the root system. 

* Step 1: Enter into the correct folder.
```
cd /home/ubuntu/POLAR_Tool/ARCH-COMP22/cartpole
```
Then activate the same environment
```
source ~/venv/bin/activate
```

* Step 2: Calculate the two types of statistical discrepancies: action- and trajectory-based discrepancy.

```
python CP_calculate_discrepancy_NoNoise.py 95
```

The 95 means that this code returns the perfect mapping discrepancies with 95% confidence.

```
python CP_calculate_discrepancy_Noise.py 95
```

This code returns noised mapping statistical discrepancy results with 95% confidence. In this case, we have two standard deviations 0.03, 0.1 zero-mean Gaussian noises added into the mapping.

* Step 3: Run the Reachability analysis with two types of discrepancies.
  
This is the core part of our paper, where the overall verification takes more than 40 hours on the whole initial set. Therefore, we recommend committee run reachability analysis on a subset of our initial set. Note that cartpole takes 4 dimensional inputs, more complex than mountain car and inverted pendulum.

This is the command for nosied mapping for action-based discrepancy, which takes approximately 8 minutes. 
```
make && ./double_pendulum_more 0 0.05 0 0.05 0.05 0.08 -0.4 -0.37
```

This is the command for nosied mapping for trajectory-based discrepancy, which takes approximately 8 minutes.
```
make && ./double_pendulum_noised_perfect 0 0.05 0 0.05 0.05 0.08 -0.4 -0.37
```

This is the command for perfect mapping for action-based discrepancy, which takes approximately 8 minutes.
```
make && ./double_pendulum_perfect_act 0 0.05 0 0.05 0.05 0.08 -0.4 -0.37
```

This is the command for perfect mapping for trajectory-based discrepancy, which takes approximately 8 minutes.
```
make && ./double_pendulum_perfect_traj 0 0.05 0 0.05 0.05 0.08 -0.4 -0.37
```

(Optional) If you want to run the verification on the whole initial set [0, 0.1] x [0, 0.1] x[0.05, 0.15] x[-0.4, -0.35], you can simply change the initial set to be bigger by typing, make && ./double_pendulum_more 0 0.1 0 0.1 0.05 0.15 -0.4 -0.35


The results will be in the folder outputs.

* Calculate the confusion matrix for both perfect mapping and noised mapping. This is the final results that we display in the paper. Please compare these results with 

```
python CP_confusion_matrix.py
```
These are the final results that match the Table 1 "Cartpole (CP)" part of the paper. More details assisting you to compare will be displayed in the command window.

```
python CP_confusion_matrix_noised.py
```

These are the final results that match the Table 2 "Cartpole (CP)" part of the paper. More details assisting you to compare will be displayed in the command window.

Also, the tiny deviation can still happen (e.g., true positive rate from 0.7225 to 0.7227), but it is still acceptable.
