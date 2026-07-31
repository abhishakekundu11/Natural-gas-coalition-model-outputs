# A study on coalition formation and bargaining power for the North American natural gas market

**Authors:** Abhishake Kundu, Felipe Feijoo

**Affiliation:** School of Industrial Engineering, Pontificia Universidad Católica de Valparaíso, Chile 2362807

**Paper status:** Under review at Utilities Policy

**Contact:** abhishake.kundu@pucv.cl

## Overview

This repository contains the data which constitute the outputs from the optimization model for the coalition-scenario (Section 2.1 Mathematical Formulation) and data to setup the pairwise-coalition regression analysis (Section 2.5 Linear regression models for coalition scenarios) of the above paper. It includes:

- The full set of coalition-scenario run outputs (production, investment,
  producer surplus, and consumer surplus for each of the 42,298 possible
  pairwise coalition combinations among the 13 producers considered).
- The regression dataset for the the 42,294 possible pairwise coalition 
  combinations used to fit the producer- and consumer-surplus models
  on these outputs (Eq. 3-4 linear regression models).

## Repository structure

```
outputs from optimization model/
    outputX.zip                      Consolidated zipped outputs from the MIQP model for all 
                                    42,294 coalition combinations. One excel file per 
                                    combination; see "Data dictionary" below for terminologies.
                                    Zipped files have been divided and numbered X to accomodate
                                    allowable size for a Github upload.
    DATA_DICTIONARY_README.md        Terminologies and definitions pertaining to the outputs 
                                    from the optimization model,as consolidated in the outputs.zip

regression data/
    coalition_results.xlsx           An excel file that consolidates all the 42,294 coalition 
                                    combinations as put in outputs.zip. The file has 38 indicator 
                                    variables representing the possible combinations of pairwise 
                                    producers if they are in a coalition pair or not. The response 
                                    variable corresponds to the Producer/ Consumer Surplus Difference 
                                    for the given coalition structure minus that from the BAU scenario.

README.md                          This file.
LICENSE                            [MIT / CC-BY-4.0 / etc.]
```

## License

[Code is released under the MIT License (see LICENSE). Data is released
under CC-BY-4.0 — free to use with attribution.]
