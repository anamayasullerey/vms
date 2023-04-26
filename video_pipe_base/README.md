# video_pipe_base
video_pipe_base is docker image will have basic tools for video pipeline creation.
This includes (key parts):
   - ffmpeg
   - cv4
   - python3
   - v4l-utils

# Building the image

```
sudo make build
```

# Running the image

```
sudo make run
```

# Attaching a bash shell

```
sudo make attach
```

# Testing the image
Run basic camera capture application (press 'q' to quit)
## C++
```
cd /proj/test_video/cpp
cmake .
make
./DisplayVideo
```
## Python
```
cd /proj/test_video/python
python3 display_video.py
```
