FROM debian:bullseye


RUN apt-get update && apt-get install -y gcc git curl make libncurses-dev flex bison gperf python python-serial

RUN mkdir /root/esp
RUN curl -o /tmp/xtensa.tar.gz https://dl.espressif.com/dl/xtensa-lx106-elf-linux64-1.22.0-100-ge567ec7-5.2.0.tar.gz
RUN tar -xzf /tmp/xtensa.tar.gz -C /root/esp
RUN usermod -aG dialout root

ENV PATH ${PATH}:/root/esp/xtensa-lx106-elf/bin
ENV IDF_PATH /root/esp/ESP8266_RTOS_SDK

RUN git clone --recursive https://github.com/espressif/ESP8266_RTOS_SDK.git ${IDF_PATH}

RUN apt-get install -y python-pip
RUN cd /root/esp && pip install --upgrade pip
RUN pip install --user -r ${IDF_PATH}/requirements.txt
RUN cp -r ${IDF_PATH}/examples/get-started/hello_world ~/esp
