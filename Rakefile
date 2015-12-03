REPO = 'git@github.com/dunleav1/puppet.git'

SSH = 'ssh -A -i vertex001.pem -l ubuntu'

desc "Run Puppet on ENV['CLIENT']"
task :apply do
 client = ENV['CLIENT']
 sh "git push"
 sh "#{SSH} #{client} pull-updates"
end


desc "Bootstrap Puppet on ENV['CLIENT'] with
 hostname ENV['HOSTNAME']"
task :bootstrap do
 client = ENV['CLIENT']
 hostname = ENV['HOSTNAME'] || client
 commands = <<BOOTSTRAP
sudo hostname #{hostname} && \
sudo su - c 'echo #{hostname} > /etc/hostname' && \
wget http://apt.puppetlabs.com/puppetlabs-release-precise.deb && \
sudo dpkg -i puppetlabs-release.deb && \
sudo apt-get update && sudo apt-get -y install git puppet && \
git clone #{REPO} puppet && \
sudo puppet apply --modulepath=/home/ubuntu/puppet/modules /home/ubuntu/puppet/manifests/site.pp
BOOTSTRAP
 sh "#{SSH} #{client} '#{commands}'"
end

