# libpmsynth
This library provides core functions for phase modulation (PM)
synthesis, commonly marketed as FM synthesis.  These include fixed-point
sinusoidal computations and waveform generators, LFOs, hooks for EGs,
and so forth.

# Phase Modulation

Unlike FM synthesis, which adjusts the frequency of a carrier based on
the amplitude of a modulator, PM synthesis adds a modulator `m(t)` to
the phase of a carrier `c(t)`, producing `c(t + m(t))`.  The function
`m(t)` retains its shape, shifted in the time axis by `Δm(t)`.  For
example, when `Δm(t)` is positive, `c(t)` increases in frequency; when
negative, `c(t)` decreases in frequency; and when constant, `c(t)`
remains at its fundamental frequency, phase shifted by `m(t)`.

Because `Δm(t)` controls the phase shift, the magnitude of `m(t)`
has a strong effect on the modulated signal.  The function for PM
synthesis, when the waveform is a sine wave, is as follows:

`ω(t) = A×sin(t + B×m(t))`

Where `A` is the carrier's gain, `B` is the modulator's gain, and
the carrier is a sine wave.  In PM synthesis, this equation gets
much more complex:  gain is multiplied by an envelope and by an AM
LFO; a vibrato LFO is added to the phase; self-feedback multiplies
the previous output by a feedback gain value and adds it to the
phase; and some PM synthesizers, such as the OPL3, use alternate
carrier functions such as `|sin(t)|` or square waves.

This library assembles all of these into a framework for quickly
developing synthesizers with different attributes.
