FROM cicdpipeline/daxeosrtsp

WORKDIR /home/pacat

COPY . .

WORKDIR /home/pacat/RTSP-Stream-Video-Capturer/build

USER root
RUN CC=clang CXX=clang++ cmake .. && make

USER pacat

ENTRYPOINT ["./rtsp_stream_video_capturer"]
