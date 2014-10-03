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

## Ideas for Improvement

Here are some ideas for ways that these playbooks could be extended:

- define client_max_body_size variable on nginx.conf instead of on site.conf
- create a solr role
- add xhprof to the php role
- enable apc for the cli (to prevent slowdowns on cron and drush jobs)
- prepare syslog for the drupal watchdog
- handle Drupal upgrades automatically.
- support debian
- enable apc on cli also for ubuntu (we did it for /etc/php5/fpm/php.ini)

We would love to see contributions and improvements, so please fork this
repository on GitHub and send us your changes via pull requests.

## Defined Roles

### syslog

The syslog module disables the watchdog (dblog) module and enables the syslog
module for each of your sites. It depends on your sites already being installed.
It will also configure syslog (`/etc/rsyslog.conf`) to log all drupal events
to `/var/log/drupal.log`
