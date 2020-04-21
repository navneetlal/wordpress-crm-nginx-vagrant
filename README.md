# Running wordpress.org CRM on virtual machine

### Prerequisite:
1. Vagrant
1. Oracle VirtualBox (or other)
1. docker & docker-compose

### Steps
Start the virtual machine using vagrant. This uses `Vagrantfile`, so make sure you are the root directory.
```bash
  $ vagrant up 
```
This will provision `docker` and `docker-compose` and will also sync folder `./files/` to `/vagrant_data` in guest machine.

Next after the virtual machine is up and running, ssh into virtual machine using vagrant and use docker-compose to start the server at port 80.

```bash
  $ vagrant ssh
    Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-177-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/advantage


    0 packages can be updated.
    0 updates are security updates.

    New release '18.04.4 LTS' available.
    Run 'do-release-upgrade' to upgrade to it.


    Last login: Tue Apr 21 07:07:48 2020 from 10.0.2.2

  $ cd /vagrant_data
  $ docker-compose up -d
    Creating network "vagrant_data_default" with the default driver
    Starting vagrant_data_mariadb_1 ... done
    Starting vagrant_data_wordpress_1 ... done
```

Virtual Machine port 80 has been mapped with host machine port 8080. CRM will be accessible from host machine by visiting `localhost:8080`.

**CRM Dashboard available at `localhost:8080/wp-admin`.**

To make changes in default configuration of wordpress, make use of env file available at `./files/.env`

---

>**Note:** This version of wordpress user `nginx` as its webserver and `mariadb` as database instead of MySQL. This makes the whole configuration smaller in size (comparatively 1/3 of original configuration).
