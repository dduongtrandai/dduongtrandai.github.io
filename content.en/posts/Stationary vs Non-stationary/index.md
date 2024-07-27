---
author: "duongtd"
date: 2024-07-26
title: Stationary vs Non-stationary
tags: [
    ""
]
categories: [
    "Signal Processing"
]
---

In signal processing, the concepts of **stationary** and **non-stationary** are used to describe the properties of a signal over time.

## Stationary Signal
A signal is called stationary if its statistical properties do not change over time. These statistical properties include mean, variance, and correlation functions. There are two types of stationarity:

1. **Weak Stationarity (or Wide-Sense Stationarity)**: The signal has a constant mean and variance over time, and the correlation function depends only on the time difference between two points, not on the specific time points themselves.
   
2. **Strong Stationarity (or Strict-Sense Stationarity)**: All probability distributions of the signal do not change over time.

## Non-Stationary Signal
A signal is called non-stationary if its statistical properties change over time. This means the mean, variance, or correlation functions of the signal change over time. Non-stationary signals often appear in systems where characteristics change over time, such as audio signals, medical signals (heart rate, brain waves), and many other real-world data.

## Applications and Processing
1. **Processing Stationary Signals**: Methods like Fourier Transform (FT) and Fast Fourier Transform (FFT) are commonly applied because they assume the signal is stationary.
   
2. **Processing Non-Stationary Signals**: Time-frequency analysis methods such as Short-Time Fourier Transform (STFT), Wavelet Transform, and Empirical Mode Decomposition (EMD) are often used to analyze and process non-stationary signals.

Understanding the difference between stationary and non-stationary signals is crucial in choosing the appropriate signal processing methods to achieve accurate and efficient results.
