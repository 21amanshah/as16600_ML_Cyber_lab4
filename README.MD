# ML for Cyber Security Lab 4
## as16600

In this assignment, we have been presented a compromised neural network called BadNet B1. This neural network(sunglasses backdoor) is vulnerable to backbook attacks. We need to repair this NN by pruning on its last pooling layer.

As a result of pruning the validation accuracy will decrease. The goal is to prune the model B1 where the decrease in validation accuracy reaches threshold(X) = 2%, 4% & 10%. We obtain a pruned and modified version of the original BadNet B1, denoted as a "repaired" network G. This repaired network can correctly classify clean inputs while also detecting instances of backdoor attack, which would lead to a different classification(N+1).

### Data <a name='data'></a>

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
