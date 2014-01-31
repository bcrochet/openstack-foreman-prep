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

TODO:

Fix need to run with --skip-tags clone_images
