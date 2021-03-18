###########################################
#                   TBZ                   #
#                                         #
#              Sergio Normani             #
#                   LB2                   # 
#                18.03.2021               #
#                                         #
#                                         #
###########################################

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
  config.vm.synced_folder ".", "/var/www/html"  
config.vm.provider "virtualbox" do |vb|
  vb.memory = "512"  
end
config.vm.provision "shell", inline: <<-SHELL
  # Packages werden vom lokalen Server geholt
  # sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
  sudo apt-get update
  sudo apt-get -y install apache2 
  cd /
  mkdir cronscript
  cd cronscript
  # Dieser Teil vom Script ist für das Darstellen der Prozesse zuständig
  touch run-cronjob.sh
  echo "env TZ=Zuerich-1 date > /var/www/html/prozesse" > run-cronjob.sh
  echo "ps aux >> /var/www/html/prozesse" >> run-cronjob.sh
  chmod +x /cronscript/run-cronjob.sh
  crontab -l | {  cat; echo "* * * * * /cronscript/run-cronjob.sh"; } | crontab - 
SHELL
end