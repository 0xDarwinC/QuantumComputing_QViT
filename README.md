# QViT_FIRE298
Experimentation for QViT technology. Goal is to reproduce results, and expand upon the original quantum circuit to observe higher accuracies/speedups in computation.

Based on https://github.com/EyupBunlu/QViT_HEP_ML4Sci


# CIRCUITS INFO
The script installs necessary quantum computing libraries using the commands !pip install tensorcircuit and !pip install pennylane, which are essential for implementing quantum machine learning functions. It imports the QViT (Quantum Vision Transformer) module from the cloned repository in Google Colab or from a local path, depending on the execution environment. These components set up the groundwork for integrating quantum circuits into the machine learning workflows.


| Function Name  | Description | Example Input  | Example Output |
| ------------- | ------------- |------------- | ------------- |
| QLayer.circuit_to_func()  | Turns a a quantum circuit into a function that's compatible with Pytorch | Takes a quantum circuit, an input tensor ([batch_size, dim] for batch_size number of samples with dim features), and parameters ([K, nqubits] for K layers on nqubits qubits)| Returns a PyTorch function that evaluates the quantum circuit for multiple inputs simultaneously  |
| QLayer.forward  | Computes the forward pass of the quantum layer using inputs and stored parameters | input1 (shape: [batch_size, dim]) | output (shape: [batch_size, dim_out]) |

Hybrid Encoder Layer Info: 
| **Process**               | **Description**                                                                                   | **Input**                                                   | **Output**                                                  |  
|---------------------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------|------------------------------------------------------------|  
| **Data**                  | The initial data like words or images is converted into numerical vectors to be processed.        | Raw data like text or images                              | Numerical vectors representing the data                    |  
| **LayerNorm**             | Normalizes the data to make the model more stable and efficient by standardizing feature values.  | Numerical vectors from the data phase                      | Normalized vectors with mean 0 and standard deviation 1    |  
| **Hybrid Multi-Head Attention** | Combines quantum and classical methods to focus on important parts of the data while processing multiple perspectives simultaneously. | Normalized vectors and attention parameters                | Updated vectors highlighting important relationships       |  
| **MLP (Multi-Layer Perceptron)** | A neural network that refines the updated vectors, extracting deeper patterns.        | Updated vectors from the attention phase                   | Final refined vectors    |  

# ML FUNCTIONS INFO
Data preparation begins with downloading and preparing the MNIST dataset using mnist_trainset = MNIST(root='./data', train=True, download=True). The dataset is then transformed, applying resizing and normalization to the images through a composed transformation pipeline. Two different models, a classical model and a hybrid model, are initialized with specific configurations, using the command classical_model = HViT(...).to(device) and hybrid2_model = HViT(...).to(device).

Training configurations are set up with optimization algorithms using Adam and a cross-entropy loss function specified by loss_fn = nn.CrossEntropyLoss(reduction='none'). The training procedure is encapsulated in a function defined as def train(model, tr_dl, val_dl, loss_fn, optim, n_epochs, device='cuda'), which manages forward passes, loss calculation, and parameter updates. The training function is executed for both models, capturing their performance histories.

Finally, the script visualizes the training results by plotting the training and validation loss and accuracy for both models, allowing for a clear comparison of their performances over the training epochs.

# OBSERVATIONS WHILE PRODUCING RESULTS
Saloni: I noticed that the code took a while to run, mostly because I am using my CPU rather than a GPU. The classical model took about 7 minutes to train 80 epochs, while the hybrid (with the quantum circuit) took around an hour. For this reason, I was hesitant to increase the number of epochs simply due to the time it takes. The code takes a significantly shorter amount of time to run on Darwin's machine, so he is taking care of a lot of the graphs. With 80 epochs, I was able to achieve about a 70% accuracy.

# POTENTIAL AREAS OF QUANTUM CIRCUIT TO BE IMPROVED
- n/a
