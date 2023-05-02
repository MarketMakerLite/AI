FROM ubuntu:focal-20230412

ENV DISTRO=ubuntu2004
ENV NV_CUDA_CUDART_VERSION=11.6.55-1
ENV NV_CUDA_COMPAT_PACKAGE=cuda-compat-11-6
ENV LD_LIBRARY_PATH=/usr/local/nvidia/lib:/usr/local/nvidia/lib64
ENV CUDA_VERSION=11.6.2
ENV NVIDIA_VISIBLE_DEVICES=all
ENV NVIDIA_DRIVER_CAPABILITIES=compute,utility
ENV NV_LIBNPP_VERSION=11.6.3.124-1
ENV NV_LIBCUBLAS_VERSION=11.9.2.110-1
ENV NV_LIBNCCL_PACKAGE_VERSION=2.12.10-1
ENV NV_LIBNPP_DEV_VERSION=11.6.3.124-1
ENV NV_LIBCUBLAS_DEV_VERSION=11.9.2.110-1
ENV NV_NVPROF_VERSION=11.6.124-1
ENV NV_LIBNCCL_DEV_PACKAGE_VERSION=2.12.10-1
ENV NV_CUDNN_VERSION=8.4.0.27
ENV DEBIAN_FRONTEND=noninteractive SHELL=/bin/bash

ENV NVARCH=x86_64
ENV NVIDIA_REQUIRE_CUDA=cuda>=11.6 brand=tesla,driver>=418,driver<419 brand=tesla,driver>=450,driver<451 brand=tesla,driver>=470,driver<471 brand=unknown,driver>=470,driver<471 brand=nvidia,driver>=470,driver<471 brand=nvidiartx,driver>=470,driver<471 brand=quadrortx,driver>=470,driver<471

CMD ["bash"]
ARG TARGETARCH=amd64
RUN apt-get update && apt-get install -y --no-install-recommends gnupg2 curl ca-certificates && curl -fsSL https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/${NVARCH}/3bf863cc.pub | apt-key add - && echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/${NVARCH} /" > /etc/apt/sources.list.d/cuda.list && apt-get purge --autoremove -y curl && rm -rf /var/lib/apt/lists/*
RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf
ENV PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ENV NV_CUDA_LIB_VERSION=11.6.2-1
ENV NV_NVTX_VERSION=11.6.124-1
ENV NV_LIBNPP_PACKAGE=libnpp-11-6=11.6.3.124-1
ENV NV_LIBCUSPARSE_VERSION=11.7.2.124-1
ENV NV_LIBCUBLAS_PACKAGE_NAME=libcublas-11-6
ENV NV_LIBCUBLAS_PACKAGE=libcublas-11-6=11.9.2.110-1
ENV NV_LIBNCCL_PACKAGE_NAME=libnccl2
ENV NCCL_VERSION=2.12.10-1
ENV NV_LIBNCCL_PACKAGE=libnccl2=2.12.10-1+cuda11.6
ENV NVIDIA_PRODUCT_NAME=CUDA
ENV NV_CUDA_CUDART_DEV_VERSION=11.6.55-1
ENV NV_NVML_DEV_VERSION=11.6.55-1
ENV NV_LIBCUSPARSE_DEV_VERSION=11.7.2.124-1
ENV NV_LIBNPP_DEV_PACKAGE=libnpp-dev-11-6=11.6.3.124-1
ENV NV_LIBCUBLAS_DEV_PACKAGE_NAME=libcublas-dev-11-6
ENV NV_LIBCUBLAS_DEV_PACKAGE=libcublas-dev-11-6=11.9.2.110-1
ENV NV_NVPROF_DEV_PACKAGE=cuda-nvprof-11-6=11.6.124-1
ENV NV_LIBNCCL_DEV_PACKAGE_NAME=libnccl-dev
ENV NV_LIBNCCL_DEV_PACKAGE=libnccl-dev=2.12.10-1+cuda11.6
ENV LIBRARY_PATH=/usr/local/cuda/lib64/stubs
ENV NV_CUDNN_PACKAGE_NAME=libcudnn8
ENV NV_CUDNN_PACKAGE=libcudnn8=8.4.0.27-1+cuda11.6
ENV NV_CUDNN_PACKAGE_DEV=libcudnn8-dev=8.4.0.27-1+cuda11.6

RUN apt-get update && apt-get install -y --no-install-recommends cuda-libraries-11-6=${NV_CUDA_LIB_VERSION} ${NV_LIBNPP_PACKAGE} cuda-nvtx-11-6=${NV_NVTX_VERSION} libcusparse-11-6=${NV_LIBCUSPARSE_VERSION} ${NV_LIBCUBLAS_PACKAGE} ${NV_LIBNCCL_PACKAGE} && rm -rf /var/lib/apt/lists/*
RUN apt-mark hold ${NV_LIBCUBLAS_PACKAGE_NAME} ${NV_LIBNCCL_PACKAGE_NAME}
RUN apt-get update && apt-get install -y --no-install-recommends libtinfo5 libncursesw5 cuda-cudart-dev-11-6=${NV_CUDA_CUDART_DEV_VERSION} cuda-command-line-tools-11-6=${NV_CUDA_LIB_VERSION} cuda-minimal-build-11-6=${NV_CUDA_LIB_VERSION} cuda-libraries-dev-11-6=${NV_CUDA_LIB_VERSION} cuda-nvml-dev-11-6=${NV_NVML_DEV_VERSION} ${NV_NVPROF_DEV_PACKAGE} ${NV_LIBNPP_DEV_PACKAGE} libcusparse-dev-11-6=${NV_LIBCUSPARSE_DEV_VERSION} ${NV_LIBCUBLAS_DEV_PACKAGE} ${NV_LIBNCCL_DEV_PACKAGE} && rm -rf /var/lib/apt/lists/*
RUN apt-mark hold ${NV_LIBCUBLAS_DEV_PACKAGE_NAME} ${NV_LIBNCCL_DEV_PACKAGE_NAME}
RUN apt-get update && apt-get install -y --no-install-recommends ${NV_CUDNN_PACKAGE} ${NV_CUDNN_PACKAGE_DEV} && apt-mark hold ${NV_CUDNN_PACKAGE_NAME} && rm -rf /var/lib/apt/lists/*

WORKDIR /workspace
RUN apt-get update && apt-get install -y python3-pip apt-utils git wget curl nodejs npm openssh-server zip unzip ffmpeg && apt-get clean && rm -rf /var/lib/apt/lists/* && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
RUN curl -sL https://deb.nodesource.com/setup_16.x -o /tmp/nodesource_setup.sh
RUN bash /tmp/nodesource_setup.sh
RUN ln -s /usr/bin/python3 /usr/bin/python
RUN apt-get install python3.8-venv

WORKDIR /workspace
RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git

WORKDIR /workspace/stable-diffusion-webui
RUN python -m venv /workspace/stable-diffusion-webui/venv
ENV PATH="/workspace/stable-diffusion-webui/venv/bin:$PATH"
RUN pip install -U jupyterlab ipywidgets jupyter-archive gdown
RUN jupyter nbextension enable --py widgetsnbextension

WORKDIR /workspace/stable-diffusion-webui
ADD install.py .
RUN python -m install --skip-torch-cuda-test
RUN pip install --upgrade --force-reinstall xformers==0.0.18 torch torchvision torchaudio

RUN apt clean && rm -rf /var/lib/apt/lists/* &&  echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && apt update

RUN wget https://civitai.com/api/download/models/29460 --content-disposition -P /workspace/stable-diffusion-webui/models/Stable-diffusion/realisticVisionV20_v20.safetensors

WORKDIR /workspace/stable-diffusion-webui
ADD relauncher.py .
ADD webui-user.sh .
ADD start.sh /start.sh
RUN chmod a+x /start.sh

SHELL ["/bin/bash", "--login", "-c"]
CMD [ "/start.sh" ]
