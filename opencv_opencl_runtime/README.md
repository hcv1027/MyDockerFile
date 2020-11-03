```bash
docker build -t opencv_opencl_runtime .
docker run -it --gpus all --name opencv_opencl_runtime -v $PWD:/root/workspace opencv_opencl_runtime /bin/bash 
```