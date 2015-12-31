# Drupal+Nginx+PHP-FPM Deployment

- Requires Ansible 1.6 or newer
- Expects Ubuntu 14.04 or CentOS/RedHat 6.5 hosts
- If using vagrant with ubuntu you need to `apt-get install nfs-kernel-server`

These playbooks (found in sample_yml) deploy a simple all-in-one configuration
of the popular Drupal software platform and CMS, frontend by the Nginx web server
and the PHP-FPM process manager. To use with vagrant:

    cp sample_yml/site.example.yml site.yml
    edit site.yml
    vagrant up

At this time the VM will come up with the IP of 192.192.0.8. Our road map will
parameterize this and other values for greater flexibility.

The playbooks will configure MySQL, Drupal, Nginx, and PHP-FPM. When the run
is complete, you can access server (http://192.192.0.8/) to begin the Drupal
configuration.

Then run the playbook with a remote server instead of a vagrant VM you need to
create a `hosts` file and a `site.yml` file and then run the `ansible-playbook`
command, like this:

    ansible-playbook -i hosts site.yml

There are example hosts and site.yml files in the sample_yml folder.

## TODO

Here are some ideas for ways that these playbooks could be extended:

- Use our own nginx.conf based on (epoll, multi_accept, file_cache):
  - http://www.slashroot.in/nginx-web-server-performance-tuning-how-to-do-it
  - http://www.codestance.com/tutorials-archive/nginx-tuning-for-best-performance-255
  - https://github.com/h5bp/server-configs-nginx/blob/master/nginx.conf
  - https://www.digitalocean.com/community/tutorials/how-to-optimize-nginx-configuration
- add xhprof to the php role
- test debian support
- handle Drupal upgrades automatically.

We would love to see contributions and improvements, so please fork this
repository on GitHub and send us your changes via pull requests.

## Other Defined Roles

### php7-fpm

PHP 7 for ubuntu 14.04.

### hhvm

HHVM serves as a replacement for php-fpm role. It is already configured as a
fastcgi server. HHVM is only compiled for 64bit machines and right now this role
is only for ubuntu 14.04.

### syslog

The syslog module disables the watchdog (dblog) module and enables the syslog
module for each of your sites. It depends on your sites already being installed.
It will also configure syslog (`/etc/rsyslog.conf`) to log all drupal events
to `/var/log/drupal.log`

### mailer

A role to allow the server to send emails. It uses postfix and the default
distribution configuration.

### solr

A role to run solr using the provided jetty example, which is the recommended 
method instead of using tomcat or full jetty.

http://lucene.472066.n3.nabble.com/difference-between-apache-tomcat-vs-Jetty-td4096680.html
