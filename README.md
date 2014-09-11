## Drupal+Nginx+PHP-FPM Deployment

- Requires Ansible 1.6 or newer
- Expects Ubuntu 14.04 hosts

If you need ssh agent forwarding with vagrant you can add
`config.ssh.forward_agent = true` to your Vagrantfile.

These playbooks deploy a simple all-in-one configuration of the popular
Drupal software platform and CMS, frontend by the Nginx web server and the
PHP-FPM process manager. To use, copy the `hosts.example` file to `hosts` and 
edit the `hosts` inventory file to include the names or URLs of the servers
you want to deploy.

Then run the playbook, like this:

	ansible-playbook -i hosts site.yml

The playbooks will configure MySQL, Drupal, Nginx, and PHP-FPM. When the run
is complete, you can hit access server to begin the Drupal configuration.

### Ideas for Improvement

Here are some ideas for ways that these playbooks could be extended:

- Separate the components (PHP-FPM, MySQL, Nginx) onto separate hosts and 
hande the configuration appropriately.
- Handle Drupal upgrades automatically.

We would love to see contributions and improvements, so please fork this
repository on GitHub and send us your changes via pull requests.
