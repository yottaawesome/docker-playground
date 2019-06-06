# Installing Docker for Ubuntu

The below instructions have been adapated from the [official docs](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce).

1. Update the apt package index: `sudo apt-get update`.
2. Install packages to allow apt to use a repository over HTTPS:
  ```Bash
  sudo apt-get install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg-agent \
  software-properties-common
  ```
3. Add Docker’s official GPG key: `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`.
4. Set up the stable repository:
  ```Bash
  sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
   ```
5. Update the apt package index: `sudo apt-get update`.
6. Install the latest version: `sudo apt-get install docker-ce docker-ce-cli containerd.io`.
