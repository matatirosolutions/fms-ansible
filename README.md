#Installing FileMaker server on Ubuntu using Ansible

Recently Claris Inc. released a version of FileMaker server for CentOS. They're now following that up with a version for Ubuntu, which is great news for those of us who already use Ubuntu extensively.

At Matatiro Solutions we also use Ansible for our server configuration, management and deployments, so we're very pleased to be able to extend that capability to deploying FileMaker servers as well. If you're not familiar with Ansible, then I'd suggest taking a read of [how Ansible works](https://www.ansible.com/overview/how-ansible-works) for some background details.

At present the Ubuntu version of FileMaker server is only available to members of the ETS programme, however if you want to be involved with that get in touch with [Robert Holsey](mailto:robert_holsey@claris.com) and I'm sure he'd be happy to add you.

## Prerequisite
You will need to have Ansible installed on your local machine, if not [check out the documentation](https://docs.ansible.com/ansible/latest/installation_guide/index.html).

##Using this playbook

1. Download the current version of FileMaker for Ubuntu, unzip the file and place it into `roles > fms > files`
1. Open `group_vars > all` in a text editor and update the variables found there
    - `fqdn` the domain name which your new FileMaker server will be hosted at
    - `admin_user` username for the admin console
    - `admin_password` the correspodning password you wish to set
    - `admin_pin` the pin number to be set in case you need to reset the admin password
    - `installer_filename` should be set to the full name of the installer you downloaded in step 1, e.g. `filemaker-server_19.2.2.213_amd64.deb`  
    - `ssl_key` paste the SSL key you wish to use with your FileMaker server between `-----BEGIN PRIVATE KEY-----` and `-----END PRIVATE KEY-----`. In future versions of this playbook we will integrate with Lets Encrypt to avoid this step being necessary.
    - `ssl_cert` paste your certificate bewteen `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----`
    - `intermediary_cert` add as many intermediary certificates as necesary, each between a set of `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----`
1. Open `ssh_config` in a text editor and update the details there, replacing the domain name, IP address, username and path to the associated ssh key with values applicable to your server.
1. Open `host` in a text editor and add your domain name below `[fms]`   
1. From a command prompt run `ansible-playbook site.yml -i host`.

##The future
We hope to convert this to a proper Ansible role and add it to Ansible Galaxy once Claris release this version.

It should also be possible to download the installer directly from Claris to the remote server, rather than needing to download the file to the role first.

If you run into any issues, please feel free to get in touch.

## Contact Details ##
Steve Winter  
[Matatiro Solutions](https://msdev.nz)  
[steve@msdev.co.uk](mailto:steve@msdev.co.uk)

