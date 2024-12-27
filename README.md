sudo useradd -m -s /bin/bash frappe
sudo passwd frappe
sudo usermod -aG sudo frappe
su frappe

nano ~/.bashrc
# Add end of file
PATH=$PATH:~/.local/bin/
# Finish end of file

source ~/.bashrc

sudo apt-get install git
sudo apt-get install libffi-dev python3-pip python3-dev python3-testresources libssl-dev wkhtmltopdf gcc g++ make -y
sudo apt-get install mariadb-server mariadb-client -y
sudo mysql_secure_installation
sudo service mysql restart
sudo mysql -u root -p
# Inside MySQL
use mysql;
UPDATE user SET plugin='mysql_native_password' WHERE user='root';
FLUSH PRIVILEGES;
EXIT;
# Exit MySQL

sudo nano /etc/mysql/my.cnf
# Inside end editor my.cnf

[mysqld]

character-set-client-handshake = FALSE

character-set-server = utf8mb4

collation-server = utf8mb4_unicode_ci

[mysql]

default-character-set = utf8mb4

# End editor

sudo service mysql restart
sudo apt-get install redis-server
sudo apt-get install curl

curl -sL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install -g yarn

sudo apt-get install xvfb libfontconfig wkhtmltopdf

sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python3-openssl

curl https://pyenv.run | bash

nano ~/.bashrc
# Inside file

export PATH="$HOME/.pyenv/bin:$PATH"

eval "$(pyenv init -)"

eval "$(pyenv virtualenv-init -)"

# End file

source ~/.bashrc

pyenv install 3.11.9

sudo pip3 install frappe-bench
bench init frappe-bench --frappe-branch version-15 --python ~/.pyenv/versions/3.11.9/bin/python

cd frappe-bench/
bench new-site next.lan

bench get-app erpnext --branch version-15
bench get-app hrms --branch version-15
bench --site next.lan install-app erpnext
bench --site next.lan install-app hrms

bench setup nginx

sudo bench setup production frappe


sudo supervisorctl restart all






sudo snap install--classic certbot
sudo ln-s /snap/bin/certbot /usr/bin/certbot
sudo certbot–nginx
