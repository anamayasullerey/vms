build: Dockerfile
	docker build -t video_pipe_base .

run:
	docker run \
		-p 8888:8888 \
		--rm \
		-ti \
		--shm-size=1g \
		-e DISPLAY=${DISPLAY} \
		-v /tmp/.X11-unix:/tmp/.X11-unix \
		--device=/dev/video0:/dev/video0 \
		--device=/dev/video1:/dev/video1 \
		--device=/dev/media0:/dev/media0 \
		--device=/dev/v4l/by-id/usb-4K_USB_CAMERA_HD_USB_CAMERA_01.00.00-video-index0:/dev/v4l/by-id/usb-4K_USB_CAMERA_HD_USB_CAMERA_01.00.00-video-index0 \
		--device=/dev/v4l/by-id/usb-4K_USB_CAMERA_HD_USB_CAMERA_01.00.00-video-index1:/dev/v4l/by-id/usb-4K_USB_CAMERA_HD_USB_CAMERA_01.00.00-video-index1 \
		-v ${HOME}/.ssh:/root/.ssh:ro \
		-v ${HOME}/.gitconfig:/root/.gitconfig:ro \
		--name video_pipe_base \
		video_pipe_base:latest \
		/bin/bash

attach:
	docker exec -it video_pipe_base /bin/bash
