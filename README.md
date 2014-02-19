Usage
-----

Copy group_vars/all.sample to group_vars/all, and edit.

Put your target in an inventory file
    [vm_host]
    my.target.example.com

Generate an ssh config for the host and passthru

If on RHEL 6
    export ANSIBLE_SSH_ARGS=""

Then:

    export ANSIBLE_HOST_KEY_CHECKING=False
    ansible-playbook -i hosts ssh_config.yml -u root

The resulting file in /tmp/ssh_config_{{ target hostname }} can be used via:

    export ANSIBLE_SSH_ARGS="-F /tmp/ssh_config_hostname"

Or, you can just append it to $HOME/.ssh/config

Add a target host to your inventory, and run.

    ansible-playbook -i hosts site.yml

You will end up with an inventory file pointing to your new VMs in /tmp/inventory.

Revert
------

You can revert to the 'first_snap' snapshot by running

    ansible-playbook -i hosts revert.yml

Cleanup
-------

You can remove all the guests (including the initimage) with

    ansible-playbook -i hosts cleanup.yml

Currently, this doesn't clean up the snapshots quite right on RHEL 6.x. Works on Fedora.

Beaker
------

Add a host to your inventory in the [beaker_client] group

To add a new *released* distro, put it in roles/beakerbox/defaults/main.yml.

To add an as yet released distro, override the distros dictionary with the new
release.

To select a distro, set 'distro={distro name}' on the command line or in group_vars/all,
where {distro name} is a key in the distros dict.
