# Absolute molecular Entropies for flexible molecules
This is a collection of input geometries used in https://doi.org/10.26434/chemrxiv.13626083.v1

The project utilized the freely available `crest` program, which can be obtained from https://github.com/grimme-lab/crest

## Entropy calculations with `crest`

As written in the manuscript there are only a couple of steps necessary for the calculation of absolute molecular entropies:

1. Find the best minimum energy conformer, e.g. by running `crest coord --gfnff` and subsequent DFT geometry optimizations using `censo` (https://github.com/grimme-lab/CENSO)

2. For the minimum conformer calculate frequencies (at DFT level) and from the frequencies calculate S<sub>msRRHO</sub>. Frequency scaling factors and the rigid-rotor/harmonic oscillator interpolation parameter τ have to be adjusted in the respective programs, e.g. `thermo`. `crest` provides a standalone `thermo` implementation with a default τ = 25.0 cm^-1 and adjustable frequency scaling factors, but at the time of writing is only able to read frequencies in `xtb`'s and Turbomoles `vibspectrum` format. The respective command is: `crest --thermo coord [optional: --fscal <scaling-factor>, --sthr <τ>]` which requires a `vibspectrum` file to be present.

3. Calculate S<sub>conf</sub> with `crest`. We strongly recommend GFN-FF as default due to the high computational cost: `crest coord --entropy --gfnff`

4. Calculate S<sub>abs</sub> = S<sub>msRRHO</sub> + S<sub>conf</sub>
