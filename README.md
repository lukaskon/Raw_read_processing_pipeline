# Raw_read_processing_pipeline
Steps for cleaning/trimming, indexing, and aligning Botrytis raw reads



# Run FastQC on raw reads first

more runFastQC.sb

#!/bin/bash --login
########## Define Resources Needed with SBATCH Lines ##########

#SBATCH --time=24:00:00             # limit of wall clock time - how long the job will run (sam
e as -t)
#SBATCH --ntasks=1                  # number of tasks - how many tasks (nodes) that you require
 (same as -n)
#SBATCH --cpus-per-task=1           # number of CPUs (or cores) per task (same as -c)
#SBATCH --mem=60G                    # memory required per node - amount of memory (in bytes)
#SBATCH --job-name runFastQC     # you can give your job a name for easier identification (same
 as -J)


########## Command Lines to Run ##########

module load fastqc                   ### load necessary modules, e.g.

cd /mnt/research/Hausbeck_group/Lukasko/BotrytisRNASeq/RawReadsRNA/20211109_mRNASeq_PE150


fastqc *fastq.gz -o MultiQC/



scontrol show job $SLURM_JOB_ID     ### write job information to output file

# Exit vi and submit job
sbatch runFastQC.sb

# Run MultiQC to see all samples together

more runMultiQC.sb

#!/bin/bash --login
########## Define Resources Needed with SBATCH Lines ##########

#SBATCH --time=24:00:00             # limit of wall clock time - how long the job will run (same as -t)
#SBATCH --ntasks=1                  # number of tasks - how many tasks (nodes) that you require (same as -n)
#SBATCH --cpus-per-task=1           # number of CPUs (or cores) per task (same as -c)
#SBATCH --mem=60G                    # memory required per node - amount of memory (in bytes)
#SBATCH --job-name runMultiQC     # you can give your job a name for easier identification (same as -J)


########## Command Lines to Run ##########


module load GCC/7.3.0-2.30  OpenMPI/3.1.1
module load MultiQC                   ### load necessary modules, e.g.

cd /mnt/research/Hausbeck_group/Lukasko/BotrytisRNASeq/RawReadsRNA/20211109_mRNASeq_PE150/MultiQC

multiqc .


scontrol show job $SLURM_JOB_ID     ### write job information to output file

# Exit and submit job
sbatch runMultiQC.sb


