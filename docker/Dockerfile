# This Dockerfile sets up a iSDF environment with PyTorch (GPU).
# This Dockerfile sets up a torch-ngp environment with GPU support.

FROM nvidia/cuda:11.3.1-cudnn8-devel-ubuntu20.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && \
    apt install -y \
        wget git net-tools vim curl build-essential x11vnc zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev \
        libreadline-dev libffi-dev libsqlite3-dev libbz2-dev liblzma-dev freeglut3-dev && \
        # following is for opencv-python (uncomment if not needed)
        apt install -y --no-install-recommends libglib2.0-0 libxrender1 libxext6 libsm6 libgl1-mesa-glx && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

ENV PATH="/root/miniconda3/bin:${PATH}"
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    mkdir /root/.conda && \
    bash Miniconda3-latest-Linux-x86_64.sh -b && \
    rm -f Miniconda3-latest-Linux-x86_64.sh && \
    echo "Running $(conda --version)"

RUN git clone https://github.com/stalhabukhari/iSDF.git && \
    conda init bash && . /root/.bashrc && conda env create -f iSDF/environment.yml && rm -rf iSDF && \
    conda activate isdf && pip install torch --extra-index-url https://download.pytorch.org/whl/cu113

RUN echo "source activate isdf" >> ~/.bashrc
WORKDIR /isdf-wkdir