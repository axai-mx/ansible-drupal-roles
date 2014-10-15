# Drupal+Nginx+PHP-FPM Deployment

- Requires Ansible 1.6 or newer
- Expects Ubuntu 14.04 or CentOS/RedHat 6.5 hosts

These playbooks deploy a simple all-in-one configuration of the popular
Drupal software platform and CMS, frontend by the Nginx web server and the
PHP-FPM process manager. To use, copy the `hosts.example` file to `hosts` and 
edit the `hosts` inventory file to include the names or URLs of the servers
you want to deploy. Then copy and modify the site.example.yml or
site.big-example.yml to site.yml.

Then run the playbook, like this:

    ansible-playbook -i hosts site.yml

If you want to use vagrant you can try our sample Vagrantfile just by installing
vagrant and running:

    vagrant up.

The playbooks will configure MySQL, Drupal, Nginx, and PHP-FPM. When the run
is complete, you can access server (http://localhost:8080 on vagrant) to begin
the Drupal configuration.

## TODO

Here are some ideas for ways that these playbooks could be extended:

- Use our own nginx.conf based on (epoll, multi_accept, file_cache):
  - http://www.slashroot.in/nginx-web-server-performance-tuning-how-to-do-it
  - http://www.codestance.com/tutorials-archive/nginx-tuning-for-best-performance-255
  - https://github.com/h5bp/server-configs-nginx/blob/master/nginx.conf
  - https://www.digitalocean.com/community/tutorials/how-to-optimize-nginx-configuration
- enable apcu for the cli (to prevent slowdowns on cron and drush jobs, we are
  only doing it for fpm on ubuntu)
- add xhprof to the php role
- test debian support
- handle Drupal upgrades automatically.

We would love to see contributions and improvements, so please fork this
repository on GitHub and send us your changes via pull requests.

## Defined Roles

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
