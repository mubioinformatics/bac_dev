## Guide to Run bac_dev Container on a Cluster

Please follow the below steps to run the bac_dev container on a cluster:

1. Remotely access any login node's terminal using the following command:
   ```
   ssh ${USER}@lewis.rnet.missouri.edu

   ssh ${USER}@lewis42.rnet.missouri.edu

   ssh ${USER}@lewis4-dtn.rnet.missouri.edu
   
   ssh ${USER}@lewis4-dtn1.rnet.missouri.edu
   ```

2. Copy the bac_dev.job file to your home directory using the below command:
   ```
   cp /storage/hpc/group/ircf/software/singularity_bac_dev/bac_dev.job ~/bac_dev.job
   ```

3. Navigate to your home directory using the following command:
   ```
   cd
   ```

4. Check for an available node using the below command:
   ```
   sinfo --state=idle
   ```

5. Modify the "bac_dev.job" file as per your requirements based on Partition, Node, Memory, MYDATA, etc.:
   ```
   #!/bin/bash
   ##SBATCH -p r630-hpc3
   ##SBATCH -w lewis4-r630-hpc3-node548
   #SBATCH -p Gpu
   #SBATCH -t 0-02:00  # time (days-hours:minutes)
   #SBATCH --ntasks-per-node=10
   #SBATCH --mem=100G
   #SBATCH --output=/home/%u/log_bac_dev.job.%j
   ##SBATCH --mail-user=youremail@missouri.edu  # email address for notifications
   ##SBATCH --mail-type=END,FAIL  # which type of notifications to send
   #SBATCH -J bac_dev
   ...
   ...
   ...
   MYDATA=/storage/hpc/data/${USER}/mydata
   ...
   ...
   ...
   ```

6. Submit the job to the SLURM scheduler using the below command:
   ```
   sbatch bac_dev.job
   ```

7. Check the job log for instructions by running the below command:
   ```
   cat log_bac_dev.job.*
   ```