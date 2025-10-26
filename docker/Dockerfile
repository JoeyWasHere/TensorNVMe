FROM runpod/base:1.0.0-cuda1300-ubuntu2404

# install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends liburing2 libaio1t64 libaio-dev cmake && \
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/*

# install pytorch
RUN pip install --upgrade pip && \
    pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu130
    
# # tqdm needed for benchmark_adam.py script 
# # tqdm/colossalai needed for benchmark_cpuadam.py script 
# RUN pip install tqdm --index-url https://download.pytorch.org/whl/cu130 && \
#     pip install colossalai

# set LD_LIBRARY_PATH for torch
ENV LD_LIBRARY_PATH=/usr/local/lib/python3.12/dist-packages/torch/lib:$LD_LIBRARY_PATH

# install tensornvme
RUN git clone https://github.com/hpcaitech/TensorNVMe.git && \
    cd TensorNVMe && \
    pip install -r requirements.txt && \
    python setup.py install 