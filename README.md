# Signal Processing Blocks -MATLAB Implementation

> **Note:** You cannot use any built-in functions such as `fft`, `fftshift`, and `freqz`. Analog signals cannot be simulated directly in MATLAB, so to simulate continuous-time signals, sample them with a sufficient frequency using the following approximation (the larger the sampling frequency, the more accurate the approximation):
> $x(t) \approx x(nT_s)$

## Part (a) – Discrete-Time Fourier Transform (DTFT)
The discrete-time Fourier transform (DTFT) of $x[n]$ is given by:
$X(e^{j\omega}) = \sum_{n=-\infty}^{\infty} x[n] e^{-j\omega n}$

### Task
Write a function called `DTFT` that takes the signal $x[n]$ in the range $[n_1, n_2]$ as input and returns $X(e^{j\omega})$ in the range $[-\omega_0, \omega_0]$.

- **Use this function to compute the Fourier transform of:**
  1. $x_1[n] = (0.8)^n, \quad -10 \leq n \leq 20$
  2. $x_2[n] = 1, \quad 0 \leq n \leq 40$

- **Plot the magnitude and phase in the range $[-\omega_0, \omega_0]$.**

## Part (b) – Signal Compression

Write a function `Compressor` that compresses the signal by a factor $M$:
$y[n] = x[nM]$

- **Task:**
  1. Sample the continuous signal $x_c(t) = \sin(2\pi f t$ in the interval $[-4, 4]$ seconds with a frequency of 10 Hz.
  2. Use the `Compressor` function for $M \in \{2, 4\}$.
  3. **Plot** the frequency response of both the compressed and original signals, and analyze the results.

## Part (c) – Signal Expansion

Write a function `Expander` to expand the signal by a factor $L$:

``` math
$$ y[n] = \begin{cases}
    x[n/L], & n = 0, \pm L, \pm 2L, \dots \\
    0, & \text{otherwise}
\end{cases}
$$
```
- **Task:**
  1. Sample the continuous signal $x_c(t) = \sin(2\pi f t)$ over $[-4, 4]$ seconds at 10 Hz.
  2. Expand the signal using `Expander` for $L \in \{2, 4\}$.
  3. **Plot** the frequency response for both the expanded and original signals, and analyze the results.

## Part (d) – Interpolation

An interpolator is a filter with an impulse response \( h[n] \). The filter is used in A/D blocks or after the Expander block.

Write a function `Interpolator` that performs the following interpolations based on a `mode` input:
1. **Ideal Interpolation**:
   
   $H_{\text{ideal}}(e^{j\omega}) = L, \quad |\omega| \leq \frac{\pi}{L}$
   
2. **Linear Interpolation**:

``` math
   $$ h_{\text{lin}}[n] = \begin{cases}
       1 - \frac{|n|}{L}, & |n| \leq L \\
       0, & \text{otherwise}
   \end{cases}
   $$
   ```
3. **Cubic Spline Interpolation**: Use MATLAB’s built-in `spline` function.

- **Task:**
  1. **Explain how each interpolation method works.**
  2. **Why can't the ideal interpolator be used in practice?**
  3. **Sample a continuous signal** $s(t) = \cos(2\pi f t)$ with $f = 10 \, \text{Hz}$ over $[0, 1]$ seconds, and sample it at $f_s = 20 \, \text{Hz}$ to obtain $x[n]$.
   - **Expand** the signal using the `Expander` and `Interpolator` functions for all modes, and convert $x[n]$ to $\hat{x}(t)$.
   - **Plot** the results and explain whether $x(t)$ was recovered accurately.
