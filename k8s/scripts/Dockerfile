# BUILDER
FROM 763104351884.dkr.ecr.us-west-2.amazonaws.com/pytorch-inference-neuronx:2.1.1-neuronx-py310-sdk2.17.0-ubuntu20.04

COPY . /home/app/text-generation-webui
RUN apt update && apt install net-tools
RUN pip install -U pip && \
    pip3 config set global.extra-index-url https://pip.repos.neuron.amazonaws.com && \
    pip3 install sentencepiece && \
    pip3 install transformers-neuronx==0.9.474
RUN pip config unset global.extra-index-url && \
    pip3 install -r /home/app/text-generation-webui/requirements_neuron.txt
# pip3 install -r /home/app/text-generation-webui/extensions/openai/requirements.txt
WORKDIR /home/app/text-generation-webui
EXPOSE ${CONTAINER_PORT:-7860} ${CONTAINER_API_PORT:-5000} ${CONTAINER_API_STREAM_PORT:-5005}

ENTRYPOINT [ "/home/app/text-generation-webui/k8s/scripts/start.sh" ]