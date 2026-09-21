# Autoencoders for MNIST

> Two autoencoder architectures in PyTorch — a fully-connected baseline and a convolutional version — trained to compress and reconstruct handwritten digits.

An autoencoder learns to squeeze its input through a narrow bottleneck and
rebuild it on the other side. Nothing supervises it but the reconstruction
error, so whatever survives the bottleneck is what the network decided actually
mattered.

This repo implements both variants on MNIST and compares their reconstructions.

## Run it

Open [`Auto_encoder.ipynb`](Auto_encoder.ipynb).

```bash
pip install torch torchvision matplotlib
```

MNIST downloads automatically via `torchvision.datasets`.

## The two models

### `Autoencoder` — linear

Fully-connected layers compress the flattened 784-pixel image into a
low-dimensional latent vector, then expand it back. The simplest possible
architecture, and the baseline the convolutional version has to beat.

Because it flattens the input first, it has no notion of adjacency — pixel (0,0)
and pixel (0,1) are just two unrelated inputs. It has to learn spatial structure
from scratch, in a representation that makes that hard.

### `ConvAutoencoder` — convolutional

Convolutional layers downsample in the encoder and transposed convolutions
upsample in the decoder. Two properties come for free:

- **Locality** — kernels look at neighbourhoods, so spatial structure is built
  into the architecture rather than learned.
- **Weight sharing** — one kernel slides across the whole image, giving far
  fewer parameters and translation invariance.

The result is sharper reconstructions from a smaller model.

## Training

| Parameter | Value |
|---|---|
| Dataset | MNIST (grayscale, 28×28) |
| `batch_size` | 32 |
| Linear AE | lr 0.001, 10 epochs |
| Conv AE | 20 epochs |
| Loss | Reconstruction error (MSE) |

## What the bottleneck does

The latent layer is the whole point. Make it wide and the network can cheat by
copying the input through. Make it narrow and it's forced to find the underlying
factors — stroke thickness, slant, which digit — because no pixel-level copy
fits through.

That compressed representation is what autoencoders get used for downstream:
dimensionality reduction, denoising, and anomaly detection, where a high
reconstruction error flags input unlike anything in training.

## Related

For the probabilistic version — which learns a *distribution* over the latent
space and can therefore generate new digits rather than only reconstruct
existing ones — see
[Variational-Autoencoder-VAE](https://github.com/Fezzaioussama/-Variational-Autoencoder-VAE-).
