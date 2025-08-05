FROM ubuntu:22.04

ARG STM32CLT_PATH=/opt/st/stm32cubeclt_1.19.0

ENV PATH="$STM32CLT_PATH/CMake/bin:$STM32CLT_PATH/Ninja/bin:$STM32CLT_PATH/GNU-tools-for-STM32/bin/:$PATH"
ENV OOEDO_STM32_DRIVER_PATH="/usr/local/src/stm32-driver"

RUN apt-get update && \
    apt-get install -y lsb-release wget git

RUN wget "https://drive.usercontent.google.com/download?id=1aG42l0jP8NEuFvZsSWrsI-zthdhDDFY5&export=download&confirm" -O /tmp/install_stm32cubeclt.sh

RUN chmod +x /tmp/install_stm32cubeclt.sh && \
    LICENSE_ALREADY_ACCEPTED=1 /tmp/install_stm32cubeclt.sh

WORKDIR $OOEDO_STM32_DRIVER_PATH

RUN git clone https://github.com/STMicroelectronics/cmsis-core.git -b v5.6.0_cm7 && \
    git clone https://github.com/STMicroelectronics/cmsis-device-h7.git -b v1.10.5 && \
    git clone https://github.com/STMicroelectronics/stm32h7xx-hal-driver.git -b v1.11.4

RUN apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /root
