# CESM

[CESM (Community Earth System Model)](https://www.cesm.ucar.edu/) is a fully coupled global climate model developed by NCAR. It simulates Earth's past, present, and future climate states using interacting components for atmosphere, ocean, land, sea ice, and more.

Keywords: `climate`, `earth system model`, `atmospheric science`, `oceanography`, `coupled model`

---

## Module design

CESM modules on RCC clusters come in **two tiers**, both of which are available for each version:

| Module type | Purpose |
|-------------|---------|
| `cesm/<version>` (base) | Loads the full build environment (compiler, MPI, NetCDF, etc.) and sets `CESMROOT`. Use this to compile any compset of your choice with `create_newcase`. |
| `cesm/<version>-<compset>-<res>-<compiler>-<mpi>` (compset) | Loads the base environment **and** points to a pre-built `cesm.exe` for a specific compset/resolution. Clone with `--keepexe` to skip recompilation entirely. |

If you just want to run one of the standard pre-built compsets, the compset module is all you need.

---

## Available modules

<div class="rcc-tabs" markdown="1">
=== "Midway2"
    ```
    -------------------- /software/modulefiles2 --------------------
    cesm/2.1.5                              cesm/2.2.2
    cesm/2.1.5-BW1850-f19_g17-gnu-openmpi   cesm/2.2.2-F2000climo-f19_g17-gnu-openmpi(default)
    cesm/2.1.5-BWma1850-f19_g17-gnu-openmpi
    ```

===+ "Midway3"
    ```
    -------------------- /software/modulefiles ---------------------
    cesm/2.1.5(default)
    cesm/2.1.5-BW1850-f19_g17-gnu-openmpi
    cesm/2.1.5-BWma1850-f19_g17-gnu-openmpi
    cesm/2.2.2
    cesm/2.2.2-F2000climo-f19_g17-gnu-openmpi
    ```
</div>

To see what a module sets up:
```bash
module show cesm/2.2.2-F2000climo-f19_g17-gnu-openmpi
```

For built-in usage instructions:
```bash
module help cesm/2.1.5-BW1850-f19_g17-gnu-openmpi
```

---

## Quick start — CESM 2.2.2 (F2000climo, atmosphere-only)

This compset runs CAM6 in forced-SST mode. It is the fastest to run and a good starting point.

```bash
module load cesm/2.2.2-F2000climo-f19_g17-gnu-openmpi

# Clone the pre-built template (skips compilation entirely)
python3 $CESMROOT/cime/scripts/create_clone \
    --case /scratch/$USER/my_f2000 \
    --clone $CESM_TEMPLATE_CASE \
    --keepexe

cd /scratch/$USER/my_f2000

# Set output directory and run length
./xmlchange CIME_OUTPUT_ROOT=/scratch/$USER/cesm_output
./xmlchange STOP_N=5,STOP_OPTION=ndays

./case.submit
```

---

## Quick start — CESM 2.1.5 (BW1850 / BWma1850, fully coupled)

These compsets run a fully coupled ocean-atmosphere-land-ice model (BGC + MA variants). They are memory-intensive and require a PE layout adjustment before submitting.

```bash
module load cesm/2.1.5-BW1850-f19_g17-gnu-openmpi

python3 $CESMROOT/cime/scripts/create_clone \
    --case /scratch/$USER/my_bw1850 \
    --clone $CESM_TEMPLATE_CASE \
    --keepexe

cd /scratch/$USER/my_bw1850
```

!!! warning "PE layout fix required for BW1850 and BWma1850"
    CIME's default layout places too many tasks per node (~3.5 GB/task), causing out-of-memory failures on coupled runs. Always apply this fix before submitting:
    ```bash
    sed -i 's/^#SBATCH  --nodes=2$/#SBATCH  --nodes=8/' .case.run
    sed -i 's/^#SBATCH  --ntasks-per-node=28$/#SBATCH  --ntasks-per-node=4/' .case.run
    ```
    This gives ~12.6 GB/task, which is sufficient.

```bash
./xmlchange CIME_OUTPUT_ROOT=/scratch/$USER/cesm_output
./xmlchange STOP_N=5,STOP_OPTION=ndays

./case.submit
```

---

## Example job scripts

### Midway3 (caslake partition)

The SLURM script is generated automatically by `case.submit`. The following shows what a typical CESM 2.2.2 F2000climo job looks like after cloning:

```bash
#!/bin/bash
#SBATCH --job-name=cesm
#SBATCH --account=pi-[cnetid]
#SBATCH --partition=caslake
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=48
#SBATCH --time=02:00:00
#SBATCH --exclusive
#SBATCH --mem=0

module load cesm/2.2.2-F2000climo-f19_g17-gnu-openmpi

cd /scratch/$USER/my_f2000
./cesm.exe
```

!!! note "Job efficiency"
    Use `seff <jobid>` after a run completes to check CPU and memory efficiency. CESM coupled runs on a single caslake node typically achieve >90% CPU efficiency.

### Midway2

For Midway2, the module built-in help is self-contained and includes the full workflow, PE layout settings, and ready-to-run example commands — run:

```bash
module help cesm/2.1.5-BW1850-f19_g17-gnu-openmpi
module help cesm/2.1.5-BWma1850-f19_g17-gnu-openmpi
module help cesm/2.2.2-F2000climo-f19_g17-gnu-openmpi
```

---

## Compiling your own compset

If you want to run a compset not covered by the pre-built modules, use the base module:

```bash
module load cesm/2.2.2

python3 $CESMROOT/cime/scripts/create_newcase \
    --case /scratch/$USER/my_custom_case \
    --compset <COMPSET_LONGNAME> \
    --res <RESOLUTION> \
    --machine simple_linux \
    --compiler gnu

cd /scratch/$USER/my_custom_case
./case.setup
./case.build
./case.submit
```

See the [CIME documentation](https://esmci.github.io/cime/versions/master/html/) for available compsets and resolutions.

---

## Notes

- **Input data**: pre-staged at `$DIN_LOC_ROOT` (set automatically by the module). Do not copy or move this directory.
- **Output**: goes to `CIME_OUTPUT_ROOT`; set this to your `/scratch/$USER/` directory.
- **UCX**: RCC clusters use an OpenMPI UCX bypass for memory-pinning compatibility. This is already set in the module — no action needed.
- **Restart files**: CESM writes restart files at intervals set by `REST_N`/`REST_OPTION`. To continue a run: `./case.submit --no-batch` or resubmit via `case.submit`.
