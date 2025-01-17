# HARP

## Publication

+ Atefeh Sohrabizadeh, Yunsheng Bai, Yizhou Sun, Jason Cong. [Robust GNN-based Representation Learning for HLS](https://ieeexplore.ieee.org/document/10323853). In ICCAD, 2023.

## About
This repo contains the codes for building HARP, an automated framework to be trained to act as the surrogate of the HLS tool. It can be used to expedite the design optimization process. The database used in this repo is built using the AMD/Xilinx HLS tools, but can be replaced by other databases. 

HARP develops a GNN-based model and builds a hierarchical graph to tackle the long range of dependency in programs. It also decouples the representation of program and its transformations (i.e., pragmas), allowing the model to learn the individual impact of each of these components. These optimizations not only enhance the performance of the model and the design space exploration based on it but also improve the model’s transfer learning capability, enabling easier adaptation to new environments.


## Content
1. [Requirements and Dependencies](#requirements-and-dependencies)
2. [Project File Tree](#project-file-tree)
3. [Running the Project](#running-the-project)


## Requirements and Dependencies

### Requirements
You can install the required packages for running this project using:

````bash
sudo apt-get install python3-venv
python3 -m venv venv
source venv/bin/activate
pip3 install --upgrade pip
pip3 install -r requirements.txt
````

### Graph Generation
The graph generation requires [LLVM](https://clang.llvm.org/get_started.html). If you want to expand on the existing graphs, please consider installing it.

This project is built on LLVM 13 that can be installed by:

```
wget https://apt.llvm.org/llvm.sh
chmod +x llvm.sh
sudo ./llvm.sh <version number>
```



### Database Generation
The initial database is generated by [AutoDSE](https://github.com/UCLA-VAST/AutoDSE) which is built on top of the [Merlin Compiler](https://github.com/Xilinx/merlin-compiler). If you want to expand the database, please consider installing them.

For synthesizing the designs, three versions of the AMD/Xilinx HLS tools have been used, SDAccel 2018.3 (denoted with `v18`), Vitis 2020.2 (denoted with `v20`), and Vitis 2021.1 (denoted with `v21`).


## Project File Tree
The project file structure is as below:

````
.
+-- dse_database          # database, graphs, codes to generate/analyze them
    +-- [machsuite/poly]  # the source code, ds config, and database for each of the benchmarks
    +-- generated_graphs  # the generated graphs for each of the kernels
    +-- merlin_prj        # the Merlin project to run each of the kernels
+-- models                # the best trained models along with the initial one-hot encoder
+-- src                   # the source codes for defining and training the model and running the DSE
````


## Running the Project

The `src/config.py` contains all the tunable parameters of the project. The current configuration runs DSE using the trained models for `v21` (Vitis 2021.1). If you want to change the modes of running, please edit this file.

After setting the configurations, run the following command to execute the project:

````bash
cd src
python3 -W ignore main.py
````

You can run the `src/main.py` for training, inference, and design space exploration based on the parameters in `src/config.py`. For generating the graph, run the following command: 

````bash
cd dse_database
python3 -W ignore graph_gen.py 
````


## Citation
If you find any of the ideas/codes useful for your research, please cite our paper:

	@inproceedings{harp2023,
        title={Robust GNN-based Representation Learning for HLS},
        author={Sohrabizadeh, Atefeh and Bai, Yunsheng and Sun, Yizhou and Cong, Jason},
        booktitle={In Proceedings of the 42nd IEEE/ACM International Conference on Computer-Aided Design (ICCAD)},
        year={2023}
    }