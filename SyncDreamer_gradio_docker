FROM nvidia/cuda:12.2.0-base-ubuntu22.04
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y && \
	apt-get install -y aria2 wget git git-lfs python3-pip python-is-python3 && \
	pip install -q torch==2.0.1+cu118 torchvision==0.15.2+cu118 torchaudio==2.0.2+cu118 torchtext==0.15.2 torchdata==0.6.1 --extra-index-url https://download.pytorch.org/whl/cu118 && \
	pip install xformers==0.0.20 triton==2.0.0 && \
	pip install -q pytorch_lightning transformers taming-transformers-rom1504 kornia webdataset gradio && \
	pip install -q omegaconf einops pymcubes carvekit-colab open3d trimesh nerfacc fire segment_anything && \
	pip install -q git+https://github.com/openai/CLIP.git && \
	adduser --disabled-password --gecos '' user && \
	mkdir /content && \
	chown -R user:user /content

WORKDIR /content
USER user

RUN cd /content && \
		git clone -b dev https://github.com/camenduru/SyncDreamer-hf && \
		cd /content/SyncDreamer-hf && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/syncdreamer-pretrain.ckpt -d /content/SyncDreamer-hf/ckpt -o syncdreamer-pretrain.ckpt && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/sam_vit_h_4b8939.pth -d /content/SyncDreamer-hf/ckpt -o sam_vit_h_4b8939.pth && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/ViT-L-14.pt -d /content/SyncDreamer-hf/ckpt -o ViT-L-14.pt && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/basket.png -d /content/SyncDreamer-hf/hf_demo/examples -o basket.png && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/cat.png -d /content/SyncDreamer-hf/hf_demo/examples -o cat.png && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/crab.png -d /content/SyncDreamer-hf/hf_demo/examples -o crab.png && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/elephant.png -d /content/SyncDreamer-hf/hf_demo/examples -o elephant.png && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/flower.png -d /content/SyncDreamer-hf/hf_demo/examples -o flower.png && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/forest.png -d /content/SyncDreamer-hf/hf_demo/examples -o forest.png && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/monkey.png -d /content/SyncDreamer-hf/hf_demo/examples -o monkey.png && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/teapot.png -d /content/SyncDreamer-hf/hf_demo/examples -o teapot.png && \
		aria2c --console-log-level=error -c -x 16 -s 16 -k 1M https://huggingface.co/camenduru/SyncDreamer/resolve/main/camera-16.pkl -d /content/SyncDreamer-hf/meta_info -o camera-16.pkl

CMD cd cd /content/SyncDreamer-hf && python app.py