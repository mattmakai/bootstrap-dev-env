# Bootstrap Development Environment

Creates a Python development environment on a base image of Ubuntu 14.04.


## Bootstrap steps
Set up ~/.ssh directory, Git and basic system packages.

    mkdir ~/.ssh
    sudo apt-get install git python-virtualenv python-dev ssh
    git config --global user.email "makaimc@gmail.com"
    git config --global user.name "Matthew Makai"

Copy public and private keys to ~/.ssh.

Execute rest of steps to get Ansible working.

    cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys
    sudo sed 's/#_PasswordAuthentication_yes/PasswordAuthentication_no/' \
    /etc/ssh/sshd_config > ~/sshd_config; sudo mv ~/sshd_config /etc/ssh/
    mkdir ~/Envs; cd ~/Envs
    virtualenv bootstrap_dev_env
    source ~/Envs/bootstrap_dev_env/bin/activate
    pip install ansible
    mkdir ~/devel; cd ~/devel
    git clone git@github.com:makaimc/bootstrap_dev_env.git
    cd ~/devel/bootstrap_dev_env

Execute Ansible playbook.

    ansible-playbook bootstrap.yml -K -i ./hosts
