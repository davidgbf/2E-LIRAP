# 🚀 Main Execution Guide (`lirp_lcc_3_phase.py`)

This document provides a step-by-step guide on how to configure and execute the core optimization script of the Decision Intelligence framework. Before running the script, you must configure your solver license, select your desired dataset, and adjust the hardware-specific memory settings.

---

## 1. Gurobi License Configuration (WLS)

The exact tactical and operational models (Phases 2 and 3) rely on the **Gurobi Optimizer**. The script is pre-configured to authenticate using a Web License Service (WLS), which is ideal for cloud environments like Google Colab or Docker containers.

Locate the following block at the beginning of the script and replace the strings with your own Gurobi academic or commercial WLS credentials:

```python
# ==============================================================================
# CONFIGURAÇÃO DA LICENÇA GUROBI WLS
# ==============================================================================
WLS_ACCESS_ID = "your-access-id-here"
WLS_SECRET    = "your-secret-key-here"
LICENSE_ID    = 1234567  # Replace with your Integer License ID
```

---

## 2. Instance and Scenario Selection

The framework evaluates specific spatial instances under distinct macroeconomic and climate-driven scenarios. You must define which environment you want the algorithm to solve.

Scroll down to the `run_full_execution()` function and modify the following variables:

```python
    # 1. Select the Spatial Instance (e.g., Regional clusters, Macro-regions, or the Full State)
    instance = '139_Full.xlsx'  
    # Examples of valid inputs: '9_G103.xlsx', '15_G12.xlsx', '74_Sul.xlsx', '208_U50.xlsx'...

    # 2. Select the Stochastic Scenario
    cenario_base = 'Pessimista' 
    # Valid inputs: 'Otimista' (Optimistic), 'Realista' (Realistic), 'Pessimista' (Pessimistic)
```
*Note: Ensure that the selected `.xlsx` instance file and the `Dist_Full.xlsx` (for Proxy Border Hub calculations) are located in the same root directory as the script.*

---

## 3. Hardware and Memory Management (OOM Prevention)

The Phase 2 Set Partitioning MILP can generate a massive Branch-and-Bound tree. To prevent your machine from crashing due to Out-Of-Memory (OOM) errors, the script forces Gurobi to offload excess nodes from RAM to a Solid State Drive (SSD). 

### A. Defining the SSD Directory
At the very top of the script, define the path where Gurobi will dump its temporary files. **Make sure to change `F:/` to a valid drive on your machine** (e.g., `C:/gurobi_nodes` for Windows or `/tmp/gurobi_nodes` for Linux/Colab):

```python
import os

# Absolute path to your SSD directory
node_dir = 'F:/gurobi_nodes'

if not os.path.exists(node_dir):
    os.makedirs(node_dir)
```

### B. Solver Thread and Memory Limits
Inside the `solve_phase2_milp()` function, locate the `solver.options` block. Adjust these parameters according to your machine's physical hardware (e.g., if you have 64GB of RAM, setting the limit to 24.0GB is highly recommended):

```python
    # Offloads the Branch-and-Bound tree to the SSD once it reaches 24.0 GB of RAM usage
    solver.options['NodefileStart'] = 24.0  
    
    # Must match the directory created at the top of the script
    solver.options['NodefileDir'] = 'F:/gurobi_nodes' 
    
    # Restricts the number of threads. Using all available CPU threads consumes 
    # exponentially more RAM. Limiting it to 8 or 12 threads ensures safety without 
    # significantly compromising solving speed.
    solver.options['Threads'] = 12  
```

---

## 4. Execution Modes (Fast Debug vs. Robust Run)

To facilitate debugging, the script features a `velocidade` (Speed) toggle inside `run_full_execution()`. 

*   `velocidade = True`: Drastically cuts down evaluation limits ($E_{MAX}$) and time limits. Use this to quickly check if the code runs without errors on a new instance (takes a few minutes).
*   `velocidade = False`: Standard execution mode for scientific benchmarking. Runs the metaheuristics for 100,000 evaluations and allows Gurobi enough time to prove optimality gaps (takes several hours depending on the instance size).

---

## 5. Running the Script

Once the configurations are set, simply run the script via terminal or your IDE:

```bash
python lirp_lcc_3_phase.py
```

Upon completion, check the terminal for the analytical summary and the generated `.zip` file containing all routing maps, Excel breakdowns, and convergence plots!
```
