FROM cicdpipeline/daxeosrtsp

WORKDIR /home/pacat

COPY . .

WORKDIR /home/pacat/RTSP-Stream-Video-Capturer/build

ENV API_KEY ''
ENV SESSION_ID ''
ENV TOKEN ''
ENV RTSP_URL ''

USER root
RUN CC=clang CXX=clang++ cmake .. && make

USER pacat

ENTRYPOINT ["./rtsp_stream_video_capturer"]
