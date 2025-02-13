# nanoowl_demo
The core code to run tree example using nanoowl which is obtained from Nvidia.

## Process Note 
### Trouble Shooting

```python
ModuleNotFoundError: No module named 'aiohttp'
# pip install aiohttp - inside the container
```

```python
FileExistsError: [Errno 17] File exists: '/root/.cache/clip'
# rm /root/.cache/clip - inside the container : it tries to download a file to the cache folder as the file is existed already.
```
