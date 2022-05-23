# nopomatch

This repository contains the command ```nopomatch``` for Stata, which estimates the decomposition of a binary treatment using non-parametric matching as described in [Nopo (2008)](https://www.jstor.org/stable/40043147?seq=1). This methodology has often been used to decompose wage gaps and other gaps in outcomes for a binary treatment. In other words, this algorithm is useful to decompose the difference in means between two groups (treated v. control) controlling for covariates, restricting comparisions to the common support. This is what the original paper refers to as the unexplained gap, $\Delta_0$. 

The program also decomposes the gap in the explanied component ($\Delta_X$), and the components attributable to differences outside of the common support for treatment and control groups ($\Delta_F$ and $\Delta_M$).

I worked with this methodology many years ago and made an extension of offical do-file to allow the user computing the difference in means for binary outcomes as well, which the official do-file couldn't do properly. Useful information about this kind of decomposition methods can be found in [Fortin et al. (2011)](https://www.sciencedirect.com/science/article/abs/pii/S0169721811004072), [Kline (2011)](https://www.jstor.org/stable/29783802?seq=1) and [Sloczynski (2014)](https://onlinelibrary.wiley.com/doi/10.1111/obes.12075).

To install the package and update it the following command can be used in Stata:
```
net install nopomatch, from (https://raw.githubusercontent.com/cfbalcazar/nopomatch/main/nopomatch/) replace force all
```

Improvements to the code are welcomed.

---

A relevant byproduct of ```nopomatch``` is the variable ```_match```, which is produced after running the program on a dataset. This variable containes the non-parametric reweighting of the observations in the common support; i.e., a new set of weights. These weights can be used to carry out non-parametric doubly-robust estimation using the standard regression commants (```reg```, ```xtreg```, ```reghdfe```, ```ivreg2```, etc.), specifying the matching weights as the weights for the regressions (e.g., including ```[aw=_match]``` in the regression command). 

Since this is a non-parametric technique, keep in mind that it is subject to the curse of dimensionality; i.e., the size of the common support falls with the number of controls included. It may also be sensitive to the identity of the treatment/control group: if observations in A (B) are designated as the treatment (control) group, the decomposition may different than if the observations in B (A) are designated as the treatment (control) group; this occurs as a result of the reweighting.        
