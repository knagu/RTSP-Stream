#RTSP-Stream-Video-Capturer 

## To build the Docker image:

```bash
docker build -t <username/repository>:<tag> -f docker/Dockerfile.
```

## To run the Docker image:

```bash
docker run -it -e PULSE_SERVER=unix:/run/user/1000/pulse/native -e DISPLAY=unix$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /run/user/1000/pulse:/run/user/1000/pulse -e API_KEY=<API_KEY> -e SESSION_ID=<SESSION_ID> -e TOKEN=<TOKEN> -e RTSP_URL=<RTSP_URL> <image_name>:<tag> 
```

