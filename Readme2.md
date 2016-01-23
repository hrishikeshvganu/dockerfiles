
#Run this command to access GPU on g2.2xlarge
sudo docker run -d --device /dev/nvidiactl --device /dev/nvidia-uvm --device /dev/nvidia0  -p 8855:8855  --user root -e GRANT_SUDO=yes  -v /driveB:/home/hrishikg/work cuda-keras-nb8855-352_68
