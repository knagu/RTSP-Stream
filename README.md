#RTSP-Stream-Video-Capturer 

## To build the Docker image:

```bash
cd docker
docker build -t <username/repository>:<tag> .
```

## To run the Docker image:

```bash
docker run -it -e PULSE_SERVER=unix:/run/user/1000/pulse/native -e DISPLAY=unix$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /run/user/1000/pulse:/run/user/1000/pulse <image_name>:<tag> <API_KEY> <SESSION_ID> <TOKEN> <RTSP_URL>
```

