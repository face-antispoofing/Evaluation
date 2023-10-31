> **HTER Improvement Techniques Result**

  ----------------------------------------------------------------------------------
           Method                   Train    Test           Train          Test
  -------- ------------------------ -------- -------------- -------------- ---------
                                    CASIA    ReplayAttack   ReplayAttack   CASIA

  \(1\)    Original CNN model       0.5025                  0.45           

  \(2\)    RandomAutocontrast       0.5632                  0.4263         

  \(3\)    RandomSolarize           0.5736                  0.4876         

  \(4\)    RandomAdjustSharpness    0.5348                  0.5983         

  \(5\)    RandomRotation           0.521                   0.5053         

  \(6\)    Gaussian Blur            0.5478                  0.5108         

  \(7\)    Learning rate 0.02       0.5897                  0.5059         

  \(8\)    Learning rate 0.01       0.4781                  0.4963         

  \(9\)    Learning rate 0.001      0.4876                  0.5132              

  \(10\)   CNN model with adding    0.5126                  0.5578         
           layers                                                          
  ----------------------------------------------------------------------------------

Notes and observations

\(1\) Model is overfitting. The accuracy reaches 100%
after a few epochs.

\(10\) CNN model added 2 more layers
