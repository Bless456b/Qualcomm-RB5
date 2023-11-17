# Pull ubuntu base image
FROM ubuntu:18.04

# Update
RUN apt-get update -y && apt-get install -y

# Install dependencies
RUN apt-get install -y unzip && apt-get install -y wget && apt-get install -y build-essential checkinstall && apt-get install -y sudo
RUN apt-get install -y openssh-server usbutils
RUN sudo apt-get install -y adb coreutils=8.28* coreutils fakechroot=2.19*  fakeroot=1.22* kmod libc6-arm64-cross qemu-user-static udev

# Install tc-sdkmanager
COPY tc-sdkmanager-v4.0.0_amd64.deb /mnt/tc-sdkmanager-v4.0.0_amd64.deb
RUN sudo dpkg -i /mnt/tc-sdkmanager-v4.0.0_amd64.deb

# Home directory setup
RUN sudo useradd -rm hostPC -d /home/hostPC -s /bin/bash -u 1000
RUN echo 'hostPC:123456' | chpasswd
RUN sudo usermod -aG sudo hostPC
RUN sudo usermod -aG plugdev hostPC
WORKDIR /home/hostPC/

# SSH setup
RUN service ssh start
EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]
