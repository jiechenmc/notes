Every job has tasks and steps and every step has tasks

Jobs
\
Steps
\
Tasks

`--ntasks-per-node` for MPI
`--cpus-per-task` for OpenMP

The parameters `cpus-per-task` x `ntasks-per-node` cannot exceed the number of cores on a node.

Each `srun` call is like a step and if  `ntasks-per-node`  is not explicitly stated then it will inherit the parent `salloc` or `sbatch` resource allocation as the default arguments.