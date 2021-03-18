###########################################
#                                         #
#                                         #
#
#
#
#
#
###########################################
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
  config.vm.synced_folder ".", "/var/www/html"  
config.vm.provider "virtualbox" do |vb|
  vb.memory = "512"  
end
config.vm.provision "shell", inline: <<-SHELL
  # Packages vom lokalen Server holen
  # sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
  sudo apt-get update
  sudo apt-get -y install apache2 
  cd /
  mkdir cronscript
  cd cronscript
  # Script für darstellen der Prozesse schreiben
  #echo "date > /var/www/html/processes
  #"\n" >> /var/www/html/processes
  #ps aux >> /var/www/html/processes"
  #> run-cronjob.sh
  #crontab -l | {  cat; echo "* * * * * /cronscript/run-cronjob.sh"; } | crontab - 
SHELL
end
