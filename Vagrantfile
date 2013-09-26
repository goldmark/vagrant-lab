# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "opscode_centos-5.9_provisionerless"
  config.vm.box_url = "https://opscode-vm-bento.s3.amazonaws.com/vagrant/opscode_centos-5.9_provisionerless.box"
  config.berkshelf.enabled = true
  config.omnibus.chef_version = :latest

  config.vm.define "jenkins", primary: true do |jenkins|
    jenkins.vm.hostname = "build"
    jenkins.vm.network :forwarded_port, guest: 80, host: 8888

    # config.vm.network :private_network, ip: "192.168.33.10"
    jenkins.vm.provision :chef_solo do |chef|
      chef.add_recipe "yum"
      chef.add_recipe "apache2"
      chef.add_recipe "java"
      chef.add_recipe "jenkins::server"
      chef.add_recipe "jenkins::proxy"
      chef.json = {
        :java => {
          :install_flavor => "oracle",
          :jdk => {
            :"6" => {
              :"x66_64" => {
                "url" => "https://ihealthbuild.agilexhealth.com/artifactory/ext-release-local/jdk/jdk/6u45-linux/jdk-6u45-linux-x64.bin",
                "checksum" => "24425cdb69c11e86d6b58757b29e5ba4e4977660"
              }
            }
          },
          :oracle => {
            "accept_oracle_download_terms" => true
          }
        },
        :jenkins => {
          :http_proxy => {
            :variant => "apache2"
          },
          :server => {
            :plugins => [{'name' => 'scm-sync-configuration', 'version' => '0.0.7.3'}, {'name' => 'ssh-agent', 'version' => '1.3'}, {'name' => 'multiple-scms', 'url' => 'http://wiki.jenkins-ci.org/display/JENKINS/Multiple+SCMs+Plugin', }, {'name' => 'fortify360', 'version' => '3.81'}, {'name' => 'extended-choice-parameter', 'version' => '0.28'}, {'name' => 'escaped-markup-plugin', 'version' => '0.1'}, {'name' => 'token-macro', 'version' => '1.8.1'}, {'name' => 'copyartifact', 'version' => '1.27'}, {'name' => 'custom-tools-plugin', 'version' => '0.4'}, {'name' => 'envinject', 'version' => '1.88'}, {'name' => 'ansicolor', 'version' => '0.3.1'}, {'name' => 'groovy', 'version' => '1.14'}, {'name' => 'text-finder', 'version' => '1.9'}, {'name' => 'git-client', 'version' => '1.1.2'}, {'name' => 'port-allocator', 'version' => '1.8'}, {'name' => 'android-emulator', 'version' => '2.10'}, {'name' => 'versioncolumn', 'version' => '0.2'}, {'name' => 'nested-view', 'version' => '1.10'}, {'name' => 'throttle-concurrents', 'version' => '1.7.2'}, {'name' => 'parameterized-trigger', 'version' => '2.20'}, {'name' => 'git', 'version' => '1.5.0'}, {'name' => 'extended-read-permission', 'version' => '1.0'}, {'name' => 'gradle', 'version' => '1.23'}, {'name' => 'embeddable-build-status', 'version' => '1.4'}, {'name' => 'emma', 'version' => '1.29'}, {'name' => 'crowd2', 'version' => '1.5'}, {'name' => 'xcode-plugin', 'version' => '1.3.3'}, {'name' => 'artifactory', 'version' => '2.1.8'}, {'name' => 'email-ext', 'version' => '2.34'}, {'name' => 'jquery', 'version' => '1.7.2-1'}, {'name' => 'build-pipeline-plugin', 'version' => '1.4'}]
          }
        },
        :apache2 => {
          :apache => {
            :default_site_enabled => true
          }
        },
        :git        => {
          :prefix => "/usr/local"
        }
      }
    end
  end

  config.vm.define "nexus" do |nexus|
    nexus.vm.hostname = "nexus"
    nexus.vm.network :forwarded_port, guest: 80, host: 8889

    # config.vm.network :private_network, ip: "192.168.33.10"
    nexus.vm.provision :chef_solo do |chef|
      chef.add_recipe "yum"
      chef.add_recipe "apache2"
      
      chef.add_recipe "java"
      chef.add_recipe "nexus"
      chef.json = {
        :java => {
          :install_flavor => "oracle",
          :oracle => {
            "accept_oracle_download_terms" => true
          }
        }
      }
    end
  end
end
