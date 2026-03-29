# Prerequisite
- [Singularity](https://docs.sylabs.io/guides/3.5/user-guide/quick_start.html#quick-installation-steps)

# Instructions

1. Clone this repo
```
git clone https://github.com/Team-Robo/the-barn-challenge-mlda.git
cd the-barn-challenge-mlda
```

2. Build singularity image
- ROS Melodic
```
singularity build --fakeroot melodic.sif Singularity_melodic.def
```
- ROS Noetic
```
singularity build --fakeroot noetic.sif Singularity_noetic.def
```

3. Start interactive session, binding this repo root as writable host directory to `/workspace` in Singularity container
> Note: Binding host directory is to ensure `run.py` can write `out.txt` without error
```
singularity shell -B $(pwd):/workspace melodic.sif
```

4. Set up environment
```
source /opt/ros/melodic/setup.bash
source /jackal_ws/devel/setup.bash
cd /workspace
```

5. Run
- Test navigation stack in world index 0
```
python3 run.py
```
- Benchmark on predefined world set
```
./test.sh
```
- Report metrics
```
python3 report_test.py --out_path out.txt
```

