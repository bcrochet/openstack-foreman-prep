Copy group_vars/all.sample to group_vars/all, and edit.

Add a target host to your inventory, and run.

    ansible-playbook -i hosts site.yml

You will end up with an inventory file pointing to your new VMs in /tmp/inventory.

Also, you will need to set up a proxy in your ssh_config ($HOME/.ssh/config),
so that the client config will work properly.

    Host 192.168.7.*
        UserKnownHostsFile /dev/null
        StrictHostKeyChecking no
        ProxyCommand ssh root@{{ remote_box }} -W %h:%p
        User root
        IdentityFile /tmp/ssh_key/{{ remote_box }}/root/.ssh/id_rsa

Replace {{ remote_box }} with the hostname of the box you are building VMs on.
