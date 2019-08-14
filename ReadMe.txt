Slope is : 2.0455e+13

Simulated Target Movement assuming Target Range as 110m and velocity as -20m. Added a loop to generate beat Signal.

Generated a plot for Range FFT, peak is near to target range (100m)

2DCFAR : getting peak at expected range and velocity (110, -20). All the other noise is suppresed, offset is taken as 10dB.

Selection of Training cells :

Implementation Steps for 2d CFAR :

  1. Initially convert RDM matrix from dB to normal value and store it in seprate var.(this is done outside the loop because inside loop, dBtopow takes lot of time).

  2. Loop through the RDM matrix (exluding the boundaries depending upon training cells and Guard Cells).

  3. Take the average of training cells (to model noise). Add offset to this average.

  4. Check if the RDM value is greater than the average + offset, if so, assign 1 otherwise 0 to the RDM value.


Selection of training Cells:

   The training cells shouldn't be large because it might overlap with the other actual signal and you may get very large offset. In case of dense traffic Scenario, the training cell value should be less. Also in case of larger training cells, you actually miss the borders.

   In this scenario, as there was just one target, I chose the training cell to be Tr = 10, Td = 8. For Selecting this, I visualized the 2D FFt value and I think these values are suitable, also from the optimization point of view, these values seemed to be fine.

   Also, the training cells shouldn't be too small as it may not model the noise properly and also may overlap with the signal if the guard cell value is also less.


Selection of Guard Cells.

  Again I obsereved the 2D FFT and started with smaller values (2,2). I repeated the steps (Change the guard cell value and observe the output) and found (4,4) because further increasing the guarcell number had no significant effect also the peak was more or less around this value.


Steps taken to suppress the non-thresholded cells at the edges.

  I just replaced the values greater than 1 with 0. I think the other better way to this could have been using padding techniques as we do in Image. But I think for this project the replacing of greater values should be fine.

   
