# Cache_Replacement_Policy
Counter based cache replacement policy to evict expired lines in L2 cache.


Below commands needs to be run from gem5/ folder

1. Apply gem5_v2 patch.

 To access program counter in the policy apply patch to fresh gem5 folder by using the following command.
 
 patch -p5 -i gem5_v2.patch
 
------------------------------------------------------------------------------------------------------------------------
1. Generating  a patch file

After implementing the cache replacement policy successfully, generate another patch for the created policy using diff command between 
-> freshly downloaded gem5 folder and applied gem5_v2.patch
-> gem 5 folder in which we implemented the replacement policy

>> Go to gem5 folder (diff -Naur <old_folder> <new_folder>

>> diff -Naur /home/neo/finalWorkRefCnt/gem5/src/   /home/neo/myRefCount/gem5/src/ > gem5_myrfc.patch

Note that we only make changes in src folder of gem5 to implement our policy

-------------------------------------------------------------------------------------------------------------------------

2. Apply patch

>> Go to gem5 folder. Assuming that gem5_v2.patch is already applied, run the below mentioned command on gem5 root folder

>> patch -p5 -i gem5_myrfc.patch
-------------------------------------------------------------------------------------------------------------------------
3. Build gem to run simulation

scons -j4 build/X86/gem5.opt
--------------------------------------------------------------------------------------------------------------
4. To run Fluidanimate and bodytrack (1MB and 4MB) with LRU and RefCount

### FluidAnimate : 1MB : LRU

>> ./build/X86/gem5.opt --outdir=fluidanimate_LRU_1MB configs/example/se.py --cpu-type=AtomicSimpleCPU -n 6 --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=1MB --l2_assoc=16 --l2_rpp="LRURP()" -c /home/neo/Assignment_2/fluidanimate/fluidanimate -o "4 5 /home/neo/Assignment_2/fluidanimate/in_5K.fluid"

### FluidAnimate : 4MB : LRU
>> ./build/X86/gem5.opt --outdir=fluidanimate_LRU_4MB configs/example/se.py --cpu-type=AtomicSimpleCPU -n 6 --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=4MB --l2_assoc=16 --l2_rpp="LRURP()" -c /home/neo/Assignment_2/fluidanimate/fluidanimate -o "4 5 /home/neo/Assignment_2/fluidanimate/in_5K.fluid"

### FluidAnimate : 1MB : RefCount
>> ./build/X86/gem5.opt --outdir=fluidanimate_RefCount_1MB configs/example/se.py --cpu-type=AtomicSimpleCPU -n 6 --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=1MB --l2_assoc=16 --l2_rpp="RefCount()" -c /home/neo/Assignment_2/fluidanimate/fluidanimate -o "4 5 /home/neo/Assignment_2/fluidanimate/in_5K.fluid"

### FluidAnimate : 4MB : RefCount
>> ./build/X86/gem5.opt --outdir=fluidanimate_RefCount_1MB configs/example/se.py --cpu-type=AtomicSimpleCPU -n 6 --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=4MB --l2_assoc=16 --l2_rpp="RefCount()" -c /home/neo/Assignment_2/fluidanimate/fluidanimate -o "4 5 /home/neo/Assignment_2/fluidanimate/in_5K.fluid"

### BodyTrack : 1MB : LRU
>> ./build/X86/gem5.opt --outdir=bodytrack_LRU_1MB configs/example/se.py --cpu-type=AtomicSimpleCPU -n 6 --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=1MB --l2_assoc=16 --l2_rpp="LRURP()" --mem-size=8192MB -c /home/neo/Assignment_2/bodytrack/bodytrack -o "/home/neo/Assignment_2/bodytrack/sequenceB_1 4 1 100 5 2 4"

### BodyTrack : 4MB : LRU
>> ./build/X86/gem5.opt --outdir=bodytrack_LRU_4MB configs/example/se.py --cpu-type=AtomicSimpleCPU -n 6 --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=4MB --l2_assoc=16 --l2_rpp="LRURP()" --mem-size=8192MB -c /home/neo/Assignment_2/bodytrack/bodytrack -o "/home/neo/Assignment_2/bodytrack/sequenceB_1 4 1 100 5 2 4"

### BodyTrack : 1MB : RefCount
>> ./build/X86/gem5.opt --outdir=bodytrack_RefCount_1MB configs/example/se.py --cpu-type=AtomicSimpleCPU -n 6 --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=1MB --l2_assoc=16 --l2_rpp="RefCount()" --mem-size=8192MB -c /home/neo/Assignment_2/bodytrack/bodytrack -o "/home/neo/Assignment_2/bodytrack/sequenceB_1 4 1 100 5 2 4"

### BodyTrack : 4MB : RefCount
>> ./build/X86/gem5.opt --outdir=bodytrack_RefCount_4MB configs/example/se.py --cpu-type=AtomicSimpleCPU -n 6 --caches --l1i_size=32kB --l1d_size=32kB --l2cache --l2_size=4MB --l2_assoc=16 --l2_rpp="RefCount()" --mem-size=8192MB -c /home/neo/Assignment_2/bodytrack/bodytrack -o "/home/neo/Assignment_2/bodytrack/sequenceB_1 4 1 100 5 2 4"




