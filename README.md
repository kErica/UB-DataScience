# 2025UB-Data Science HPC
```
Contact: erica.bianco@hpcnow.com
Contact: danilo.gonzalez@hpcnow.com
```
The content of this folder was tested on Feb 2023 on the purpose to fulfill the HPC best practices Hands-on for the
Ciencia de los Datos (Data Science), Aplicaciones en Biología y Medicina con Python y R
UB IL-3 course

## List of command to run the hands-on #

### Access CSUC and transfer files

### Check the docu

[CSUC HPC Portal](https://confluence.csuc.cat/display/HPCKB/CSUC+HPC+Portal)

#### How to login
Your username is `curs$NUM` and your initial password will be provided online. 

Check the docu: [How to connect to Pirineus III](https://confluence.csuc.cat/display/HPCKB/How+to+connect+to+Pirineus+III)

NUM=[1..23].

At the first access you have set a new password with the following rules:
* 8 characters
* 1 upper case
* 1 lower case
* 1 number
* 1 special character

```
CSUC_USER=curs<INSERT YOUR NUM HERE>
ssh -p2122 $CURS_USER@pirineus3.csuc.cat
```

1. Insert the temporary password.
2. Insert the new password - remember it!!!
3. Insert again the new password.


#### How to move data
```
git clone https://github.com/kErica/UB-DataScience.git

scp -rp -P 2122 UB-DataScience-master $CSUC_USER@pirineus3.csuc.cat:/home/curs<insert number here>

## or
cd UB-DataScience
sftp –oPort=2122 $CSUC_USER@hpc.csuc.cat
mput -R *
```

Then ssh to the system
```
ssh -p2122 $CURS_USER@pirineus3.csuc.cat
```

### Explore the environment
```
pwd
df -h
ls
ls -ld .
ls -l /
```

#### SLURM basic commands
```
sacct	## Displays accounting data for all jobs.
salloc	## Allocate resources for interactive use.
sbatch	## Submit a job script to a queue
scancel	## Signal jobs or job steps that are under the control of SLURM (cancel jobs or job steps)
scontrol	## View SLURM configuration and state
sinfo	## View information about SLURM nodes and partitions
sjstat	## Display statistics of jobs ( data from sinfo, squeue and scontrol).
smap	## Graphically view information about SLURM jobs, partitions, and set config. param
squeue	## View information about jobs located in the SLURM scheduling queue.
srun	## Run a parallel job
```
## How to initiate an interactive session
> **_NOTE:_**  This is not going to work as your user cannot allocate resources.
```
salloc --time 4:00:00 srun --pty bash
```


> **_NOTE:_**  You can open a second terminal and have a current view of your queue jobs. `watch squeue -u $USER`

### Launch a serial job
```
cd UB-DataScience-master/01-Serial
sbatch serial.sh
## check your jobs and outputs
ls -lthr
```

### Launch an array of jobs
```
sbatch --array=0-9 serial-array.sh
```

### Launch an OpenMP job
```
cd ../02-OpenMP
ls
sbatch openmp.sh
cat hello.log
```

### OpenMP, Hybrid and MPI jobs
```
cd ../03-gmx/

## OpenMP job
sbatch gmx_omp_8.sh

## hybrid job
sbatch gmx_hyb_8.sh

## MPI job
sbatch gmx_mpi_8.sh
```





