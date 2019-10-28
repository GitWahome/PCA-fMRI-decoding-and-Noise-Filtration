
Article URL: https://medium.com/@brianwahome254/pca-fmri-data-haxby-noise-filtration-fbc39259f472?sk=f06913d902801da7abaea1b950618ba0

Introduction

FMRI data collection entails exposing subjects to magnetic flux and monitoring the variability of the signal on exposure to some stimuli. This variability is what we call activation/signal. The overarching goal is usually mapping stimulus to regions of the brains that are activated when they are induced. Now all this sounds simple and straight forward, but the devil lies in the details. FMRI data is muddied with noise. The noise comes from a wide range of sources ranging from basic head movements, the body’s background activation to perform basic body functions like breathing among others and even if we have a dead subject (Shout out to the Salmon experiment), Noise can come from outside interference and end up distorting the signal.

Preprocessing
One of the purposes of preprocessing is to tackle the noise problem. Some methods include slice timing correction, realignment, smoothing and alignment and normalization. Different approaches can be used to perform these steps including threshold setting for signals and Principal Component Analysis - PCA) This article will focus on PCA as a Noise Reduction tool.

Principal Component Analysis - PCA
Principal component analysis (PCA) is a statistical procedure that uses an orthogonal transformation to convert a set of observations of possibly correlated variables (entities each of which takes on various numerical values) into a set of values of linearly uncorrelated variables called principal components. This transformation is defined in such a way that the first principal component has the largest possible variance (that is, accounts for as much of the variability in the data as possible), and each succeeding component, in turn, has the highest variance possible under the constraint that it is orthogonal to the preceding components. The resulting vectors (each being a linear combination of the variables and containing n observations) are an uncorrelated orthogonal basis set. PCA is sensitive to the relative scaling of the original variables.

Simply put, we project data to a different, lower dimension. As is expected with lower dimension projection, we lose data but, we usually retain most of the information as the order of the components is by variance, where the first component explains the most variance, and the subsequent components explain less variance. This makes PCA superb for data compression and dimensionality reduction which really speeds up our process of performing Machine Learning Analysis. 


PCA for Noise Reduction
Now how could we apply PCA for Noise reduction? It has already been shown that using PCA to reduce the dimensionality of data entails information loss. Given that in Its raw format, most of the data collected from FMRI scans are usually Noise, simply performing PCA presents the risk that we will lose the true signal especially since the variance explained by the Signal is very little relative to the Noise. Now, what do we do about this? A key statement we have already made is the fact that the first principal component is usually the most significant, the second more significant and so on. What if we looked at the components that are less significant and Ignore the loud mouth components explaining most of the Variance?

While crude, this is the principle behind PCA for Noise reduction. Depending on what proportion of Noise you want to filter for, you organize your components by the variance they explain and then reconstruct your original data. Most true signal is usually weak and will not stand out in the face of the Noise thus by removing the most significant portion of the raw data, we are left with ‘more concentrated soup’ of data with the true signal being more visible.
Illustration Assumptions
To illustrate this application, we will demonstrate PCA’s potential as a Noise clean up tool. It should, however, be noted that some assumptions we make do not necessarily hold in real life, while some do. These include the following

We already know the amount of Noise we have. In real data, we tend not to know the exact amount of variance accounted for by the noise. To filter out the noise, we tend to rely on a lot of experimentation, fitting in a number of parameters and testing different thresholds until we achieve a level we are satisfied with. With PCA, this might entail including a various number of components.
We assume our data is  Gaussian. For our demo, we will randomly sample noise from a gaussian distribution. In real data too, noise tends to be normally distributed and the net noise signal is assumed to be 0 as positive and negative signals cancel out. Positive signals are spikes which may be similar to our activations albeit not induced by stimuli while negative signals.

