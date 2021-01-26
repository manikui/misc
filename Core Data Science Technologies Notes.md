# Core Data Science Technologies Notes

## Evaluation Metrics

- True Positive (TP): Model $\theta$ correctly predicts entry is part of a class $\theta(X) = 1, Y  = 1$
- True Negative (TN): Model correctly predicts entry is not part of a class $\theta(X) = 0, Y  = 0$
- False Positive (FP): Model incorrectly predicts entry is part of a class when it is not $\theta(X) = 1, Y  = 0$
- False Negative (FN): Model incorrectly predicts entry is not part of a class when it is $\theta(X) = 0, Y  = 1$
- Confusion Matrix:

|            |   | Reality  |    |
|------------|---|----------|----|
|            |   | 0        | 1  |
| Prediction | 0 | TN       | FP |
|            | 1 | FN       | TP |

- Confusion Matrix construction:
  - Numbers along diagonals tells how many entities were correctly classified
  - Numbers off diagonal are numbers of entities incorrectly classified
  - Can be scaled to multi-class classification by having 1 row and column per class
- True Positive Rate (TPR) = Sensitivity = Recall = Power = $\dfrac{\text{TP}}{\text{FN + TP}} = 1 - \text{FNR} \rightarrow$ what fraction of true cases are actually being detected, how sensitive is the test to the actual outcome?
  - Tells us what % of people inside the class in the sample were correctly identified
  - Measure of accurately predicting positives
  - Given the alternative, what fraction of times do I reject?
  - Approximates $P(\text{Decision} = 1 | \text{Reality} = 1)$
  - Look at column where Reality = 1
- True Negative Rate (TNR) = Specificity = Selectivity = $\dfrac{\text{TN}}{\text{TN + FP}} = 1 - \text{FPR}\rightarrow$ what fraction of false cases are actually being classified as such
  - Tells us what % of people outside the class in the sample were correctly identified
  - Measure of accurately predicting negatives
  - Approximates $P(\text{Decision} = 0 | \text{Reality} = 0)$
  - Look at column where Reality = 0
- They are both independent on prevalence: the probabilities of the two states of reality in the population
- Want high sensitivity if identifying positives correctly was very important
- Want high specificity if identifying negatives correctly was very important
- Miss rate = False Negative Rate (FNR) = $\dfrac{\text{FN}}{\text{FN + TP}} = 1 - \text{TPR}$
- Fall-out = False Positive Rate (FPR) = $\dfrac{\text{FP}}{\text{TN + FP}} = 1 - \text{TNR}$
- Positive Predictive Value (PPV) = Precision = $\dfrac{\text{TP}}{\text{TP + FP}} = 1 - \text{FDR}$
  - Looking at all predicted inclusions in class, what proportion were predicted correctly
  - How many selected items are relevant?
- Negative Predictive Value (NPV) = $\dfrac{\text{TN}}{\text{TN + FN}} = 1 - \text{FOR}$
  - Looking at all predicted exclusions in class, what proportion were predicted correctly
- False Omission Rate (FOR) = $\dfrac{\text{FN}}{\text{TN + FN}} = 1 - \text{NPV} \rightarrow$ what fraction of predicted negatives are actually positive
  - Looking at row predicting exclusion in class, what proportion were predicted incorrectly
- False Discovery Rate (FDR) = $\dfrac{\text{FP}}{\text{TP + FP}} = 1 - \text{PPV} \rightarrow$ what fraction of predicted positives are actually positive
  - Looking at row predicting inclusion in class, what proportion were predicted incorrectly
- Prevalence = $\dfrac{\text{TP + FN}}{\text{Population}}$
  - Prevalence of inclusion in class
- Accuracy = $\dfrac{\text{TP + TN}}{\text{Population}}$
- Type 1 error rate: probability of rejecting the null hypothesis given it is true = $P(\text{FP}) = P(\delta(X) = 1 | \theta = 0)$
- Type 2 error rate: probability of accepting a null hypothesis given it is false $P(\text{FN}) = P(\delta(X) = 0 | \theta = 1)$

## Amazon RedShift

- Data warehouse that is compatible with existing business intelligent tools
- Great to use if database is overloaded due to OLAP (online analytical processing) transactions
- Column-based database designed for OLAP, allowing you to combine multiple complex queries to find answers
- Note: SQL, Pandas are row-based: ![ ](https://i.imgur.com/O4TmEDl.png)
- Redshift is column-based: ![ ](https://i.imgur.com/DAUdpys.png)
- Columnar data is stored sequentially, requiring less reads to get all the data as OLAP queries tend to operate over columns instead of rows (i.e. tend to analyze columns of data instead of individual records)
- Easier to compress data as all data within the same column should have the same data type and they are stored sequentially
- Row-based compression is more difficult as row elements may have different data types
- Furthermore, row-based storage is less efficient for OLAP queries as the DBMS will have to do more reads to collect all data within a column (but row-based storage is more efficient for OLTP - online transaction processing queries)
- Redshift Warehouse is a collection of computing resources called "nodes". They are organized into a group called a "cluster". Each cluster runs an Amazon Redshift engine that runs one or more databases
- Starting node = 160GB
- As you add nodes, you can take advantage of massive parallel processing
- With many nodes you can operate in multi mode: Leader node that manages all client connections and Compute nodes that store data and complete computations
- Can use Redshift's Query Editor or connect SQL workbench to Redshift using its driver
- Uses S3 buckets to store data

## Docker

- Aims to package and containerize applications, allowing them to be shipped and run anywhere
- Operating Systems consist of two things: a kernel and software
  - OS kernel: Interacting with the underlying hardware
  - Software: What makes the operating system different. It includes different UIs, drivers, compilers, file managers, etc.
  - Common Linux/Ubuntu/etc. kernel shared across all OS and custom software that differentiate OS from each other
- Docker can run any type of OS on top of it as long as they're all based on the same kernel
- Containers vs. Virtual Machines
  - Containers: a standard unit of software that packages up code and all its dependencies so the application runs reliably from one computing environment to another
    - It includes everything needed to run an application: code, runtime, system tools, system libraries and settings
    - Does not contain an OS kernel but instead shares the underlying OS kernel on the machine itself with other containers, each running as isolated processes in user space
  - Virtual Machines: An abstraction of physical hardware that includes a full copy of an operating system, the application and necessary binaries and libraries
    - Built on top of a hypervisor that allows multiple VMs o run on a single machine
    - Much larger than containers (typically GB in size vs. MB) as it includes an operating system, and also takes time to boot
    - Higher utilization of hardware
    - Can run apps based on different OS within the same machine as each VM has its own OS
- Many applications are available publicly as Docker images
- Image: A package or template used to create one or more containers
- Containers: Run instances of images that are isolated and have their own environments/processes
- ```docker run [name of image]``` - Run latest version of image, will download from Hub if not done so already
  - ```docker run [name of image]:[version]``` - Run specific version of image
  - ```docker run -i [name of image]```
  - ```docker run -it [name of image]``` - Attached to pseudo-terminal in interactive mode
  - ```docker run -v [folder in docker host]:[folder in docker container]``` - Maps data contained in directory within container to directory outside so that data will persist even when container is destroyed
- ```docker inspect [container name]``` - Detailed properties of container returned as a JSON
- ```docker ps``` - Lists what containers are running and their status
- ```docker ps -a``` - Lists all containers, both running and stopped
- ```docker stop [container ID]``` - Stops running container but it's still present consuming space
- ```docker rm [container name]``` - Removes a stopped container
- ```docker images``` - List of available images stored on host
- ```docker rmi [container name]``` - Removes image from hub, that image must not have a running instance
- ```docker pull [container name]``` - Pulls image from Docker Hub but does not run it
- ```docker logs [container name/ID]``` - Prints out logs/STDOUT of ran container

## Flask/FastAPI

- Can download and install virtualenv to work within a virtual environment, keeping directiories and dependencies local to the environment, making project easier to collaborate on
- ```pip install flask flash-sqlalchemy```

```
from flask import Flask, render_template
app = Flask(__name__)

@app.route("/") # Pass in url string
def index():
  return render_template("index.html")

if __name__ == "__main__":
  app.run(debug=True)
```

## StreamLit

## PyTorch + Lighting

- A Python-based scientific computing package aimed at:
  - Replacing Numpy that uses the power of GPUs
  - A deep learning research platform that provides maximum flexibility and spped
- Tensors
  - Similar to Numpy's ndarrays except Tensors can also be used on a GPU to accelerate computing
  
  ```
  from __future__ import print_function
  import torch

  x = torch.empty(5, 3) # Creates a 5x3 tensor matrix using (small) values in allocated memory

  x = torch.rand(5, 3) # Creates a 5x3 tensor matrix of random values from 0 to 1

  x = torch.zeros(5, 3, dytpe=torch.long)

  x = torch.tensor([5.5, 3]) # Creates a tensor directly from data

  x = x.new_ones(5, 3, dtype=torch.double) # Creates a 5x3 matrix that reuses properties of the input tensor x, including its dtype (longs)

  x = torch.randn_like(x, dtype=torch.float) # Same as above except overrides dtype, but has same size as x

  x.size() # Returns torch.Size object containing tuple
  ```

- Addition
```
# Alternative 1
y = torch.rand(5, 3)
z = x + y # Of course x and y need to have the same dimension

# Alternative 2
z = torch.add(x, y)

# Alternative 3
z = torch.empty(5, 3)
torch.add(x, y, out=z) # Specifies output tensor as argument

# Alternative 4
z = y.add_(x) # In-place
```

- Any operation that mutates a tensor in-place is post-fixed with an ```_```. E.g. ```x.copy_(y)```, ```x.t_()``` changes ```x```
- Resizing: if you want to resize/reshape a tensor, use ```torch.view```

```
x = torch.randn(4, 4)
y = x.view(16) # Converts x's values into length 16 tensor
z = x.view(-1, 8) # Converts x's values into 2x8 matrix, inferring dimension when -1 is passed in
```

- If you have a one element tensor, use ```.item()``` to return a Python number

- NumPy $\iff$ PyTorch

  - The Torch Tensor and NumPy array will share their underlying memory locations if the Torch Tensor is on CPU, and changing one will change the other
  
- Converting Tensor to Array:

```
a = torch.ones(5)
b = a.numpy() # Converts a to NumPy array

a.add_(1) # tensor([2, 2, 2, 2, 2])
b # [2. 2. 2. 2. 2.]
```

- Converting Array to Tensor:

```
a = np.ones(5)
b = torch.from_numpy(a)
np.add(a, 1, out=a) # In-place NumPy array addition
```

- All tensors on the CPU except a CharTensor support converting to NumPy and back

- CUDA Tensors
  - Tensors can be moved onto any device using the .to method, provided that device is available

```
if torch.cuda.is_available():
  device = torch.device("cuda") # a CUDA device object
  y = torch.ones_like(x, device=device) # directly create a tensor on GPU
  x = x.to(device) # Or move already created tensors onto device
  z = x + y
  z.to("cpu", torch.double) # Can move back to cpu and change dtype at the same time
```

- Autograd: Automatic Differentiation
  - ```autograd``` package provides automatic differentiation for all operations on Tensors
  - It is a define-by-run framework, which means that your backprop is defined by how your code is run, and that every single iteration can be different

## NoSQL $\iff$ MongoDB

- NoSQL world:
  - Collections make up a database, not tables
  - Documents within collections, which are the rows of a table
  - They don't have to use the same schema, they can have different fields (not just nullable fields)
  - No schema implied by collection
  - Flexible solution where you can easily add data without needing much pre-processing
  - Data is typically merged/nested in a few collections
  - Have less relation merging and instead have efficient queries, but will have duplicate data
  - Works well with horizontal scaling as data can be split across muliple servers, stand-alone collections mean they can be distributed
  - Can have poor performance if multiple reads require updating data spread across multiple collections
- Horizontal scaling: add more servers and merge data into one database
- Vertical scaling: improve server capacity/hardware, limited by computing power
- SQL world:
  - Uses schema, has predictable structure
  - Relations ensure there is no duplicate data, only one place to update data as it's only stored in one place
  - Data distributed across multiple tables requiring costly joins
  - Maybe worse performance on reads spanning multiple tables
  - Does not support horizontal scaling as it is hard to split database across multiple servers while ensuring preservation in case of loss
  - Vertical scaling has limits

## Nvidia RAPIDS, Dask

<https://developer.download.nvidia.com/video/gputechconf/gtc/2019/presentation/s9797-dask-extensions-and-new-developments-with-rapids.pdf>
