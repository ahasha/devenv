BOX_NAME = ENV['BOX_NAME'] || "ubuntu"
BOX_URI = ENV['BOX_URI'] || "http://files.vagrantup.com/precise64.box"

APPS_PATH = ENV['APPS_PATH'] || "~/apps"

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = BOX_NAME
    config.vm.box_url = BOX_URI

    #Mount shared directories
    config.vm.synced_folder APPS_PATH, "/apps"

    #ipython notebook server
    config.vm.network :forwarded_port, :host => 49001, :guest => 8888

    #Build and run ipython notebook server container.
    run_args = "-p 8888:8888 " \
        "-v /apps/notebook/data:/data " \
        "-v /apps/notebook/logs:/logs " \
        "-v /apps/notebook/notebooks:/notebooks " \
        "-e \"PASSWORD=passwd\" " \
        "--name notebook "

    config.vm.provision :docker do |d|
        d.pull_images "ipython/scipyserver"
        d.run "ipython/scipyserver", args: run_args
    end
end