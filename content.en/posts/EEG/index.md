---
author: "duongtd"
date: 2024-07-26
title: Basic Electrophysiology
tags: [
    ""
]
categories: [
    "EEG"
]
---
## EEG measures summated activity

Neurons communicate through a combination of chemical neurotransmitters and electrical gradients, and electroencephalography, or EEG, detects those electrical gradients to provide insight into the activity of the brain. Realize, however, that any single neuron's electrical activity is far too miniscule to be detected by scalp EEG, and thus what we see on EEG is actually a summation of many neurons' activity; in fact, we require at least 6 square centimeters of synchronized cortical activity for anything to be detected on scalp EEG. Here we'll review the basics of neural signals and how those are converted to the tracings you'll read on EEG.

## Resting & action potentials

Neuronal membranes have a multitude of ion channels that maintain order and control signals in and around themselves. Perhaps the most important of these is the sodium potassium channel, which maintains the basal resting potential of the neuron by pumping three Na+ ions out of the cell for every two K+ ions it pumps into the cell. Because there are relatively more positive ions outside the cell, this creates an electrical gradient with a **resting potential inside the cell of -70mV.**
![alt](EEG_1.png)

## Characteristics of EEG signal

In general, biosignals are '3N' – Nonstationary, Nonlinear, Noisy

### Stationary

Nonstationarity means that signal's statistical characteristics change with time. The brain activity is essentially nonstationary. Quasi-stationary segments in EEG have duration about 0.25 sec. The basic source of the observed nonstationarity in EEG signal is not due to the casual influences of the external stimuli on the brain mechanisms but rather it is a reflection of switching of the inherent metastable states of neural assemblies during brain functioning. EEG-signal recorded from a scalp electrode is influenced by different deeper brain structures, each 'transmitting' with different and changeable intensity; so, in a fraction of a second the main source of the registered signal often moves from one brain structures to another. And if source of a signal changes with time then the signal is obviously nonstationary. Nonstationarity arises also because of different time scales involved in the dynamical process – dynamical parameters are sensitive to the time scales and hence in the study of brain one must identify all relevant time scales involved in the process to get an insight in the working of brain. It is extremely important that fractal methods easily detect nonstationarities in the analyzed signals, nonstationarities that are not easily detectable by linear methods like FFT. Nonstationarities in EEG are also due to pathological changes, for example epileptic seizures, or to changes of the physiological state, for example passing from one sleep stage to another. [^1] 

## References

[^1]: "Everything you wanted to ask about EEG but were afraid to get the right answer." *Wlodzimierz Klonowski*, 2009.
