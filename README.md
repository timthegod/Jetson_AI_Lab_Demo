# Jetson AI Lab Demo
The demo and note for Jetson AI Lab from Nvidia.

## Process Note for Jetson Orin Nano (Jetpack 6.2)
### nanoowl_demo(https://www.jetson-ai-lab.com/vit/tutorial_nanoowl.html)
#### Trouble Shooting 

```python
ModuleNotFoundError: No module named 'aiohttp'
# pip install aiohttp - inside the container
# NOTE: you have to reinstall everytime unless you persist the change, however, this will need to rebuild the docker image
```


```python
FileExistsError: [Errno 17] File exists: '/root/.cache/clip'
# rm /root/.cache/clip - inside the container : it tries to download a file to the cache folder as the file is existed already.
```

### agent studio(https://www.jetson-ai-lab.com/agent_studio.html)
#### Trouble Shooting 
##### No enough swap when quantisizing model (https://github.com/dusty-nv/NanoLLM/issues/53)
1. You have to mount a swap to your ssd, my ssd is mount to /ssd
```linux
sudo systemctl disable nvzramconfig
sudo fallocate -l 16G /ssd/16GB.swap
sudo mkswap /ssd/16GB.swap
sudo swapon /ssd/16GB.swap
sudo nano /etc/fstab
```
2. Add this at the end of your `/etc/fstab`-> /mnt/16GB.swap  none  swap  sw 0  0
3. Reboot
4. Verify
```linux
swapon --show
```
The output should list `/ssd/16GB.swap`
5. After these you will have enough swap for quantization 

##### No enough memory when using Efficient-Large-Model/VILA1.5-3b
1. Try run with Efficient-Large-Model/VILA-2.7b 
2. Make sure the model needs to be MLC LLM supported small-scale vision-language model