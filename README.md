# Firth Bias Reduction in Few-shot Classification
This repository contains the experiments conducted in the [On the Importance of Firth Bias Reduction in Few-Shot Classification](https://openreview.net/pdf?id=DNRADop4ksB) paper.

<details open>
<summary><h2>The Paper in Pictures</h2></summary>

  + <details open>
    <summary><strong>The MLE Bias in Few-shot Classification</strong></summary>
  
    Here is a visualization to help you get the overall context of typical loss minimization (MLE) bias with only a few samples.
    <img src="https://raw.githubusercontent.com/ehsansaleh/code_firth/main/opt/static_figures/mlebiasslide.svg" alt="drawing" width="96%"/>

    </details>
  
  + <details>
    <summary><strong>Firth Bias Reduction in Few Words</strong></summary>
   
    + <details open>
      <summary><strong>For 1-Layer Logistic and Cosine Classifiers with the Cross-Entropy Loss</strong></summary>

      All you need to do, is replace
      
      <p align="center"><img src="https://render.githubusercontent.com/render/math?math=\hat{\beta} = \text{argmin}_{\beta} \quad \frac{1}{N}\sum_{i=1}^{N} \bigg[\text{CE}(\mathbf{P}_i, \mathbf{y}_i)\bigg]" width="35%"></p>
      
      with
  
      <p align="center"><img src="https://render.githubusercontent.com/render/math?math=\hat{\beta}_{\text{Firth}} = \text{argmin}_{\beta} \quad \frac{1}{N}\sum_{i=1}^{N} \bigg[\text{CE}(\mathbf{P}_i, \mathbf{y}_i) %2B \lambda \cdot \text{CE}(\mathbf{P}_i,\mathbf{U}) \bigg]" width="50%"></p>
     
      where U is the uniform distribution over the classes, and lambda is a positive constant. The CE-term with the uniform distribution is basically the sum of the prediction log-probability values over all data points and classes. 
    
      </details>
  
    + <details>
      <summary><strong>General Firth Bias Reduction Form</strong></summary>
  
      Add a log-det of FIM term to your loss minimization problem. That is, replace
      
      <p align="center"><img src="https://render.githubusercontent.com/render/math?math=\hat{\beta} = \text{argmin}_{\beta} \quad \bigg[l(\beta)\bigg]" width="20%"  align="center"></p>
      
      with 
      
      <p align="center"><img src="https://render.githubusercontent.com/render/math?math=\hat{\beta}_{\text{Firth}} = \text{argmin}_{\beta} \quad \bigg[l(\beta) %2B \lambda\cdot \log(\det(F))\bigg]" width="40%" align="center"></p>,
      
      This was proven to reduce the bias of your estimated parameters.
      </details>
    
    </details>
  
  
      

  + <details>
    <summary><strong>Firth Bias Reduction in a Geometric Experiment</strong></summary>
  
    Here is a simple example show-casing average the MLE's bias from the true parameters in a geometric experiment with a fair coin, and the slow rate at which this bias disappears.

    <img src="https://raw.githubusercontent.com/ehsansaleh/code_firth/main/opt/static_figures/avgmle_vs_nsamples_geom.svg" alt="drawing" width="46.5%"/> <img src="https://raw.githubusercontent.com/ehsansaleh/code_firth/main/opt/static_figures/logmlebias_vs_lognsamples_geom.svg" alt="drawing" width="47.5%"/>

    </details>

  + <details>
    <summary><strong>Firth Bias Reduction Improvements in Few-shot Classification Tasks</strong></summary>
  
    Here is the effect of Firth bias reduction campared to typical L2 regularization in 16-way few-shot classification tasks using basic feature backbones and 3-layer logistic classifiers.

    <img src="https://raw.githubusercontent.com/ehsansaleh/code_firth/main/opt/static_figures/dacc_vs_nshots_firth_3layer_mini.svg" alt="drawing" width="48%"/> <img src="https://raw.githubusercontent.com/ehsansaleh/code_firth/main/opt/static_figures/dacc_vs_nshots_l2_3layer_mini.svg" alt="drawing" width="46%"/>
  
    Below is the effect of Firth bias reduction on cosine classifiers and S2M2R features.

    <img src="https://raw.githubusercontent.com/ehsansaleh/code_s2m2rf/main/figures/dacc_vs_nways_miniImagenet.svg" alt="drawing" width="47%"/> <img src="https://raw.githubusercontent.com/ehsansaleh/code_s2m2rf/main/figures/dacc_vs_nways_cifar.svg" alt="drawing" width="47%"/>
    
    <img src="https://raw.githubusercontent.com/ehsansaleh/code_s2m2rf/main/figures/dacc_vs_nways_tieredImagenet.svg" alt="drawing" width="94%"/>

    </details>

</details>

# The Repository Structure

  * To see the Firth regularization code used for the standard ResNet architecture results on the mini-imagenet data set, please open the [`code_firth`](./code_firth) directory.

  * For the WideResNet28 feature stack trained by the S2M2R method, and the results on the mini-imagenet, CIFAR-FS, and tiered-imagenet data sets, please open the [`code_s2m2rf`](./code_s2m2rf) directory.

  * [`code_dcf`](./code_dcf) directory contain the **GPU implementation of [Distribution Calibration (DC)](https://github.com/ShuoYang-1998/Few_Shot_Distribution_Calibration) method** and all the experiments performed on it. Please cite our paper if you use our GPU implementation of the DC method.

## References
* Here is the arxiv link to our paper:
  * The arxiv PDF link: [https://arxiv.org/pdf/2110.02529.pdf](https://arxiv.org/pdf/2110.02529.pdf)
  * The arxiv web-page link: [https://arxiv.org/abs/2110.02529](https://arxiv.org/abs/2110.02529)
* Here is the open-review link to our paper:
  * The open-review PDF link: [https://openreview.net/pdf?id=DNRADop4ksB](https://openreview.net/pdf?id=DNRADop4ksB)
  * The open-review forum link: [https://openreview.net/forum?id=DNRADop4ksB](https://openreview.net/forum?id=DNRADop4ksB)
* Our paper got a spot-light presentation at ICLR 2022.
  * We will update here with links to the presentation video and the web-page on `iclr.cc`.
* Here is the bibtex citation entry for our work:
```
@inproceedings{ghaffari2022fslfirth,
    title={On the Importance of Firth Bias Reduction in Few-Shot Classification},
    author={Saba Ghaffari and Ehsan Saleh and David Forsyth and Yu-Xiong Wang},
    booktitle={International Conference on Learning Representations},
    year={2022},
    url={https://openreview.net/forum?id=DNRADop4ksB}
}
```
