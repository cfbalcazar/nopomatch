# nopomatch

This repository contains the command ```nopomatch``` for Stata, which estimates the decomposition of a binary treatment using non-parametric matching as described in [Nopo (2008)](https://www.jstor.org/stable/40043147?seq=1). This methodology has been often used to decompose wage gaps and other gaps in outcomes for a binary treatment. In other words, this algorithm is useful to decompose the difference in means between two groups (treated v. control), restricting comparisions to the common support. This is what the original paper refers to as the unexplained gap, $\Delta_0$. 

The program also decomposes the gap in the explanied component ($\Delta_X$), and the components attributables to differences outside of the common support ($\Delta_M$ and $\Delta_F$).

I worked with this methodology many years ago and made an extension of the do-file to compute the difference in means for binary outcomes, which corresponds to the current repository. Useful information about this kind of decomposition methods can be found in [Fortin et al., 2011](https://www.sciencedirect.com/science/article/abs/pii/S0169721811004072).

A relevant byproduct of ```nopomatch``` is: it produces a non-parametric reweighting of the observations in the common support which is stored in the variable ```_match```, which is produced after running the program on a dataset. These weights can be used to carry out non-parametric doubly-robust estimation using the standard regression commants (```reg```, ```xtreg```, ```reghdfe```, ```ivreg2```, etc.), specifing the matching weights as the weights for the regressions (e.g., including ```[aw=_match]``` in the regression). 

Since this is a non-parametric technique, keep in mind that it is subject to the curse of dimensionality; i.e., the size of the common support falls with the number of controls included. It may also be sensitive to the identity of the treatment/control group; e.g., if observations in A (B) are designated as the treatment group, the decomposition may different than if the observations in B (A) are designated as the treatment group.        

To install the package and update it the following command can be used in Stata:
```
net install nopomatch, from (https://raw.githubusercontent.com/cfbalcazar/nopomatch/main/nopomatch/) replace force all
```

Improvements to the code are welcomed.
