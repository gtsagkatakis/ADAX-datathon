# ADAX-datathon
This repository contains the dataset and code for baseline models for ADA-X datathon

## Dataset
The simulated dataset used is modeled after the Euclid satellite galaxy survey. 
When generating a large, realistic, simulated spectroscopic dataset, we need to ensure that it is representative of the expected quality of the Euclid data. 
The first requirement is to have a realistic distribution of galaxies in several photometric observational parameters. 
We want the simulated data to follow representative redshift, color, magnitude, and spectral type distributions. These quantities depend on each other in intricate ways, and correctly capturing the correlations is important if we want to have a realistic assessment of the accuracy of our proposed method. 

We define a master catalog for the analyses with the COSMOSSNAP simulation pipeline , which calibrates property distributions with real data from the COSMOS survey. The generated COSMOS mock Catalog (CMC) is based on the 30-band COSMOS photometric redshift catalogue with magnitudes, colors, shapes and photometric redshifts for $538.000$ galaxies on an effective area of $1.24 \ deg^ 2$ in the sky, down to an $i$-band magnitude of $\sim 24.5$ . The idea behind the simulation is to convert these real properties into simulated properties. Based on the fluxes of each galaxy, it is possible to select the best-matching SED from a library of predefined spectroscopic templates. With a ``true" redshift and an SED associated to each galaxy, any of their observational properties can then be forward-simulated, ensuring that their properties correspond to what is observed in the real Universe.

For the specific purposes of this analysis, we require realistic SEDs and emission line strengths. Euclid will observe approximately 50 million spectra in the wavelength range $11000 - 20000\,\mathrm{\AA}$ with a mean resolution $R = 250$, where $R =  \frac{\lambda}{\Delta\lambda}$. To obtain realistic spectral templates, we start by selecting a $50\%$ random subset of the galaxies that are below redshift $z=1$ with H$\alpha$ flux above $10^{-16} \,erg\, cm^{-2} \,s^{-1}$, and bring them to rest-frame values ($z=0$). We then resample and integrate the flux of the best-fit SEDs at a resolution of $\Delta\lambda = 5\mathrm{\AA}$. This corresponds to  $R=\frac{\lambda}{\Delta\lambda} = 250$ at an observed wavelength of $11000\,\mathrm{\AA}$, if interpreted in rest-frame wavelength at $z = 2$. For the purpose of our analysis, we will retain this choice, even though it implies higher resolution at larger wavelengths. Lastly, we redshift the SEDs to the expected Euclid range. In the particular case where we wish to vary the number of training samples, we generate more than one copy per rest-frame SED at different random redshifts. We will refer to the resampled, integrated, redshifted SEDs as ``clean spectra" for the rest of the analysis.

## Code

The [ADAX_datathon_classification.ipynb](https://github.com/gtsagkatakis/ADAX-datathon/blob/main/ADAX_datathon_classification.ipynb) is jupyter notebook provides an easy-to-follow example for analyzing the data as a classification problem.

Specifically, the code demonstrates the design and training of a 1-dimensional Convolutional Neural Network.
Input: spectroscopic profile (SED)
Output: label indicating estimated redshift (rounded)

Use the "open on Colab" to execute the code online.

## More details
R. Stivaktakis, G. Tsagkatakis, B. Moares, F. Abdalla, J. L. Starck, and P. Tsakalides, "Convolutional Neural Networks for Spectroscopic Redshift Estimation on Euclid Data," IEEE Transactions on Big Data, vol. 6, no. 3, pp. 460-476, September 2020, doi: 10.1109/TBDATA.2019.2934475. 
[arxiv](https://arxiv.org/abs/1809.09622)
