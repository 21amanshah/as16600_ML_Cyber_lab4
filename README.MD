# ML for Cyber Security Lab 4
### - as16600

In this assignment, we have been presented a compromised neural network called BadNet B1. This neural network(sunglasses backdoor) is vulnerable to backbook attacks. We need to repair this NN by pruning on its last pooling layer.

As a result of pruning the validation accuracy will decrease. The goal is to prune the model B1 where the decrease in validation accuracy reaches threshold(X) = 2%, 4% & 10%. We obtain a pruned and modified version of the original BadNet B1, denoted as a "repaired" network G. This repaired network can correctly classify clean inputs while also detecting instances of backdoor attack, which would lead to a different classification(N+1).

## Data <a name='data'></a>

The data, consisting of images from the YouTube Aligned Face Dataset, is obtained from <https://github.com/csaw-hackml/CSAW-HackML-2020/tree/master/lab3> . These datasets include images of 1283 individuals that are split into validation and test datasets.It also contains 'bd_valid.h5' and 'bd_test.h5' i.e. validation and test images with sunglasses trigger respectively, that activates the backdoor for the neural network stored in 'bd_net.h5'.

```bash
├── data 
    └── cl
        └── valid.h5 //This is clean validation data used to design the defense
        └── test.h5  //This is clean test data used to evaluate the BadNet
    └── bd
        └── bd_valid.h5 //This is sunglasses-poisoned validation data
        └── bd_test.h5  //This is sunglasses-poisoned test data
├── models
    └── bd_net.h5
    └── bd_weights.h5
├── architecture.py
└── eval.py //This is the evaluation script
```
p.s. These files are not uploaded because of size constraints. Please, update the appropriate paths before running the code.

## Methodology and Findings <a name='methodology'></a>
- #### Baseline BadNet B1 evaluation 

First we evaluate clean classification accuracy on clean validation data & attack success rate on adversarial validation data for compromised B1.

B1 has Clean Classification accuracy of '98.649%' & Attack Success Rate of '100%'. \
B1 has '1283 'output classes (N).

- #### Pruning
First we observe attack success rate as a function of the fraction of channels pruned. It reveals that a substantial number of neurons can be eliminated without compromising classification accuracy as shown in the figure below. It progresses in three distinct phases: initially, the removed neurons not responsive to either clean or backdoored inputs have no impact on dataset accuracy or the success of the backdoor attack. Next, neurons exclusively activated by the backdoor are pruned, reducing the backdoor attack success while preserving the accuracy of clean data. This process culminates by pruning neurons sensitive to clean inputs, resulting in reduced accuracy for the clean dataset. Consequently, the defense stops, and models are saved based on decreased accuracy levels of 2%, 4%, and 10%, labeled as model2%.h5, model4%.h5, and model10%.h5, respectively.


![fig]()

Performance of Repaired network B'
|        Model |  Classification Accuracy  | Attack Success Rate |
|-------------:|----------:|------------:|
|  repaired_2% | 95.900234 |  100.000000 |
|  repaired_4% | 92.291504 |   99.984412 |
| repaired_10% | 84.544037 |   77.209665 |

 ![fig2]()

 GoodNet(G):
 To improve the model's capabilities, we merged the compromised BadNet B1 and the above improved model B'. The goal was to produce an enhanced combined model G.

Performance of GoodNet G:

|        Model |  Classification Accuracy  | Attack Success Rate |
|-------------:|----------:|------------:|
|  G_2% | 95.900234 |  100.000000 |
|  G_4% | 92.291504 |   99.984412 |
| G_10% | 84.544037 |   77.209665 |

![fig3]()
