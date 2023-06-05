# A Guide for Running BAC_DEV Container on a Cluster

Please follow these steps:

1. Copy the bac_dev-20230525.job file to your home directory by running this command:
   ```
   cp /storage/hpc/group/ircf/software/bac_dev/bac_dev-20230525.job ~/bac_dev-20230525.job
   ```

2. Go to your home directory by executing:
   ```
   cd
   ```

3. Check for an available node using this command:
   ```
   sinfo --state=idle
   ```

4. Adjust the "bac_dev-20230525.job" file according to your requirements for Partition, Node, Memory, etc.:
    ```
    #!/bin/bash
    ##SBATCH -p r630-hpc3
    ##SBATCH -w lewis4-r630-hpc3-node548
    #SBATCH -p Gpu
    #SBATCH -t 0-02:00  # time (days-hours:minutes)
    #SBATCH --ntasks-per-node=10
    #SBATCH --mem=100G
    #SBATCH --output=/home/%u/log_bac_dev-20230525.job.%j
    ##SBATCH --mail-user=youremail@missouri.edu  # email address for notifications
    ##SBATCH --mail-type=END,FAIL  # which type of notifications to send
    #SBATCH -J bac_dev-20230525
    ```

5. Submit the job to the SLURM scheduler by running:
   ```
   sbatch bac_dev-20230525.job
   ```

6. Check the job log and follow the instructions provided in it:
   ```
   cat log_bac_dev-20230525.job.*
   ```