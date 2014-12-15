BOX_NAME = ENV['BOX_NAME'] || "ubuntu"
BOX_URI = ENV['BOX_URI'] || "http://files.vagrantup.com/precise64.box"

APPS_PATH = ENV['APPS_PATH'] || "~/apps"
IVY_CONF_PATH = ENV['IVY_CONF_PATH'] || "~/.ivy"
SBT_CONF_PATH = ENV['SBT_CONF_PATH'] || "~/.sbt"

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = BOX_NAME
    config.vm.box_url = BOX_URI

    #Mount shared directories
    config.vm.synced_folder APPS_PATH, "/apps"
    config.vm.synced_folder IVY_CONF_PATH, "/home/vagrant/.ivy"
    config.vm.synced_folder SBT_CONF_PATH, "/home/vagrant/.sbt"

    #ipython notebook server port forwarding
    config.vm.network :forwarded_port, :host => 49001, :guest => 8888

    #Build and run ipython notebook server container.
    ipython_run_args = "-p 8888:8888 " \
        "-v /apps/notebook/data:/data " \
        "-v /apps/notebook/logs:/logs " \
        "-v /apps/notebook/notebooks:/notebooks " \
        "-e \"PASSWORD=passwd\" " \
        "--name notebook "

    scala_run_args = "-v /apps/scala/src:/src " \
                     "-v /home/vagrant/.sbt:/root/.sbt"
                     "-v /home/vagrant/.ivy:/root/.ivy"
                     "--name scala"

    config.vm.provision :docker do |d|
        d.pull_images "ipython/scipyserver"
        d.run "ipython/scipyserver", args: ipython_run_args

        d.build_image "/vagrant/containers/java", args: "-t java"
        d.build_image "/vagrant/containers/scala", args: "-t scala"
    end
end