# Automation-on-CLI-or-ECCLI-based-networks
Choosing cli_command and/or eric_eccli_command modules for automation and configuration management

While starting with configuration and automation on Ericsson nodes found [eric_eccli_command](https://docs.ansible.com/ansible/latest/modules/eric_eccli_command_module.html) module introduced in Ansible 2.9 With ansible_connection and ansible_network_os introduced as per [ERIC_ECCLI Platform Options](https://docs.ansible.com/ansible/latest/network/user_guide/platform_eric_eccli.html) in inventory, all flavors of both commands in the module worked. Specially the predefined checks in result[0] and result[1] used in wait_for give clue to user that commands are getting executed on the server(s)

As I understood result[0] can be used for all commands, including the 'show version' where grep can be made on the string 'IPOS' similary result[1] is set for 'management' to check the output for. Is one of the two strings always found in the output of any ECCLI? Where are the rest of result[i] defined otherwise? What are the rest of result[i] supposed to contain? Couldn't find the description. 

Irrespective of this satisfaction, the Ansible user stays blind with the output of the command being executed on the server. The module does not support the register parameter to store the output for Ansible user to view or further play with the registered info.

[cli_command](https://docs.ansible.com/ansible/latest/modules/cli_command_module.html), introduced in Ansible 2.7, amazingly had no issue in running the both commands, described in [eric_eccli_command](https://docs.ansible.com/ansible/latest/modules/eric_eccli_command_module.html) documentation, on Ericsson ECCLI/IPOS. And the module also supports registering the output.

Get your inventory ready with hosts and vars like ansible_connection, ansible_user, ansible_ssh_pass (though plain text not recommmended), ansible_network_os to try both modules

![724TD2](https://user-images.githubusercontent.com/47313728/88474627-6244ed00-cedd-11ea-9e6d-591317056991.png)
