TensorCraft Playbook: CNN Performance across Colab Runtimes

This repository benchmarks a Convolutional Neural Network (CNN) on the CIFAR-10 dataset across different execution environments in Google Colab Pro, focusing on how runtime selection impacts real-world performance.

The project emphasizes practical behavior, including fallback scenarios when TPU initialization is not successful.

Project Overview

The notebook executes the same model and data pipeline across three different runtimes:

CPU
GPU
TPU (with fallback handling)

The objective is to evaluate:

Training time
Throughput (images per second)
Model accuracy
Effective hardware used during execution
Key Concept

The selected runtime is not always the hardware actually used.

This project explicitly logs execution metadata, including:

requested_runtime
effective_hardware
distribution strategy
TPU verification status

This ensures that benchmark results reflect actual execution conditions rather than assumptions.

What the Code Does

The notebook:

Detects available hardware (CPU, GPU, TPU)
Attempts TPU initialization using TPUClusterResolver
Falls back to GPU or CPU if TPU initialization fails
Trains a CNN on CIFAR-10 using TensorFlow/Keras
Measures training time and throughput
Exports structured results to JSON and CSV
Example Results
Scenario	Effective Hardware	Time (s)	Throughput (img/s)
CPU runtime	CPU	~167	~1,489
GPU runtime	GPU	~34	~7,213
TPU runtime	CPU (fallback)	~30	~8,218

Note: TPU runtime may execute on CPU if TPU initialization fails.

TPU Behavior in Colab

During the experiments, the following behavior was observed:

TPU initialization may fail in Colab runtimes
TensorFlow may not be preconfigured in TPU environments
Dependency inconsistencies can prevent TPU usage
Execution may fall back to CPU without explicit indication

The notebook is designed to detect and log these conditions.

Experiment Design

To ensure fair comparison across environments:

The same model architecture is used
The same dataset (CIFAR-10) is used
The same preprocessing pipeline is applied
The same batch size and number of epochs are used

The only variable changed is the runtime environment.

Outputs

Each execution generates:

tensorcraft_cifar10_result.json
tensorcraft_cifar10_result.csv

These files contain:

runtime configuration
execution metadata
training metrics
throughput and timing
Article

A detailed technical explanation is available in the following article:

https://dev.to/ahirtonlopes/tensorcraft-playbook-de-cnns-de-sala-de-aula-a-cloud-tpus-com-keras-2gma

Key Takeaways
GPU provides consistent and expected acceleration
TPU usage in Colab is not always reliable
Infrastructure differences significantly impact performance
Benchmarking requires validation of actual execution hardware
Author

Ahirton Lopes
Senior Manager at Accenture
Google Developer Expert (AI)
Microsoft MVP (AI Platform)

Final Note

Performance in machine learning is not determined only by model design or hardware selection, but by the interaction between model, infrastructure, and execution environment.
