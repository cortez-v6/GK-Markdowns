### How to set up a TensorFlow environment on Apple Silicon using Miniforge (Apr, 2023)
If you're experienced with making environments and using the command line, follow this version. If not, please visit [this](https://github.com/sangay-cortez/GK-Markdowns/blob/main/Setup%20a%20TensorFlow%20environment%20on%20Apple%20Silicon%20using%20Miniforge/How%20to%20set%20up%20a%20TensorFlow%20environment%20on%20Apple%20Silicon%20using%20Miniforge%20-%20Extended%20(Apr%2C%202023).md) and continue after creating an environment.

1. Download and install Homebrew from https://brew.sh. Follow the steps it prompts you to go through after installation.
2. Download [Miniforge3](https://github.com/conda-forge/miniforge) for macOS arm64 chips (M1, M1 Pro, M1 Max, M1 Ultra, M2).
3. Install Miniforge3 into home directory.

    > **Note:** _If you already have a version of Anaconda installed, it may cause conflicts when installing Miniforge (if you're using M1/Pro/Max/Ultra/M2, favour Miniforge because it's specifically designed for arm64 chips)._

    ```sh
    chmod +x ~/Downloads/Miniforge3-MacOSX-arm64.sh &&
    sh ~/Downloads/Miniforge3-MacOSX-arm64.sh &&
    source ~/miniconda3/bin/activate
    ```
4. Restart terminal.

5. [Create a directory to set up TensorFlow environment](https://github.com/sangay-cortez/GK-Markdowns/blob/main/Setup%20a%20TensorFlow%20environment%20on%20Apple%20Silicon%20using%20Miniforge/How%20to%20set%20up%20a%20TensorFlow%20environment%20on%20Apple%20Silicon%20using%20Miniforge%20-%20Extended%20(Apr%2C%202023).md).
    ```sh
    mkdir tensorflow-test && cd tensorflow-test
    ```
6. Make and activate Conda environment with Python 3.10.10 (Python 3.10.11 is the most stable with M1/TensorFlow in my experience, though you could try with Python 3.x).
    ```sh
    conda create --prefix ./env python=3.10 && conda activate ./env
    ```
7. After activating the environment, install TensorFlow dependencies from Apple Conda channel.
   ```sh
   conda install -c apple tensorflow-deps
   ```
8. Install base TensorFlow (Apple's fork of TensorFlow is called tensorflow-macos).
    ```sh
    python -m pip install tensorflow-macos
    ```
9. Install Apple's tensorflow-metal to leverage Apple Metal (Apple's GPU framework) for M1, M1 Pro, M1 Max, M1 Ultra, M2 GPU acceleration.
    ```sh
    python -m pip install tensorflow-metal
    ```
10. _**[Optional*]**_ Install TensorFlow Datasets to run benchmarks included in this repo.
    ```sh
    python -m pip install tensorflow-datasets
    ```
11. Install common data science packages.
    ```sh
    conda install jupyter pandas numpy matplotlib scikit-learn
    ```
12. Start Jupyter Notebook.
    ```sh
    jupyter notebook
    ```
13. Import dependencies and check TensorFlow version/GPU access.
    ```sh
    import numpy as np
    import pandas as pd
    import sklearn
    import tensorflow as tf
    import matplotlib.pyplot as plt
    
    # Check for TensorFlow GPU access
    print(f"TensorFlow has access to the following devices:\n{tf.config.list_physical_devices()}")
    
    # See TensorFlow version
    print(f"TensorFlow version: {tf.__version__}")
    ```
    
    If it all worked, you should see something like:
    ```sh
    TensorFlow has access to the following devices:
    [PhysicalDevice(name='/physical_device:CPU:0', device_type='CPU'),
    PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
    TensorFlow version: 2.8.0
    ```
