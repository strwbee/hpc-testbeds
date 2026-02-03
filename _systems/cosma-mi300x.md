---
name: "COSMA MI300X"
status: in-service
category: testbed
focus: discipline
focus-detail: "Astronomy and Cosmology"
grouping: "COSMA"
funders:
- STFC
- DiRAC
- ExCALIBUR
nodes: 1
accelerators:
- "AMD MI300X (192GB)"
accelerator-count: 8
manufacturer: "AMD"
scheduler: "Slurm"
interconnects:
reference: https://cosma.readthedocs.io/en/latest/gpu.html#mi300x 
---

## COSMA MI300X

COSMA (The Compute Optimised System for Modelling and Analysis) is a High Performance Computing facility hosted at Durham University, operated by the Institute for Computational Cosmology on behalf of DiRAC.

The MI300X node is a GPU testbed within COSMA.

| Node | RAM | CPU | Access |
|------|-----|-----|--------|
| ga007 | 2TB | 96 cores (Intel Xeon Platinum 8468) | Slurm (`mi300x`) |

The MI300X is AMD's data center GPU, optimised for LLM and genAI training and inference.

The MI300X node has 8x GPUs.  

### Documentation

- <https://cosma.readthedocs.io/en/latest/gpu.html#mi300x>
- <https://www.amd.com/en/products/accelerators/instinct/mi300/mi300x.html>

### Gaining access

Access requires a COSMA account, obtained via the [DiRAC SAFE portal](https://safe.epcc.ed.ac.uk/dirac/).

1. Create a SAFE account with an institutional email.
2. Upload an SSH public key on SAFE. If you do not have one, generate with `ssh-keygen -t ed25519`.
2. Request a login account. This requires selecting a project, either:
- Project `do018` for AMD GPY testbed access.
- A DiRAC project code for a given allocation (provided by a supervisor).
3. **Wait** for the account to be approved by the project manager. Keep an eye on your email!
4. Connect to COSMA via SSH: `ssh username@login8.cosma.dur.ac.uk` (Note: On first login you will be asked to change the password provided in your email)

Visit <https://cosma.readthedocs.io/en/latest/account.html> for more details.
Contact cosma-support@durham.ac.uk for any questions.

### Usage

Jobs are submitted via Slurm to the `mi300x` partition:
```bash
#!/bin/bash
#SBATCH --partition=mi300x
#SBATCH --account=do018
#SBATCH --time=01:00:00

rocm-smi # checks existence of GPU
./gpu_program_to_run
```

For interactive access:
```bash
srun -p mi300x -A do018 -t 10 --pty /bin/bash
```

### Restrictions

- Maximum wall time: 6 hours
- The AMD ROCm software stack is installed. ROCm 6.3.0 is available at `/opt/rocm-6.3.0/bin/hipcc`
- Any existing CUDA code needs to be HIP-ified with the hipify script provided as part of ROCm