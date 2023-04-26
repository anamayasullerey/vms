# video_pipe_base
video_pipe_base is docker image will have basic tools for video pipeline creation.
This includes (key parts):
   - ffmpeg
   - cv4
   - python3
   - v4l-utils

# Building the image

```
make build
```

# Running the image

```
make run
```

# Attaching a bash shell

```
make attach
```

# Testing the image
Run basic camera capture application (press 'q' to quit)
## C++
```
cmake .
make
./DisplayVideo
```
python3 display_video.py
```
