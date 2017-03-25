# Audio Stream Example

A simple example that streams your mic input into the temporal pooler (TP), 
and outputs an anomaly score, based on how familiar the TP has become to that
particular mic input sequence. Think of it as being able to recognize a song,
or become more familiar with your speech pattern.

This is forked from htm-community/nupic-example-code. 

## Requirements

- Ubuntu  Ubuntu 16.04.2 LTS
- [matplotlib](http://matplotlib.org/)
- [pyaudio](http://people.csail.mit.edu/hubert/pyaudio/)

## Configuration
- input_device_index should be selected according to the configuration of target system

## Usage

    python audiostream.py

This script will run automatically & forever.
To stop it, use KeyboardInterrupt (CRTL+C).

## General algorithm:

1. Mic input is received (voltages in the time domain)
2. Mic input is transformed into the frequency domain, using fast fourier transform
3. The few strongest frequencies (in Hz) are identified
4. Those frequencies are encoded into an SDR
5. That SDR is passed to the temporal pooler
6. The temporal pooler provides a prediction
7. An anomaly score is calculated off that prediction against the next input
    A low anomaly score means that the temporal pooler is properly predicting 
    the next frequency pattern.

## Print outs include:

1. An array comparing the actual and predicted TP inputs
	A - actual
	P - predicted
	E - expected (both A & P)
2. A hashbar representing the anomaly score
3. Plot of the frequency domain in real-time   
