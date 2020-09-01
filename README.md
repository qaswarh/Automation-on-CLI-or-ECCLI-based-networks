# Ansible Network Automation - CLI vs ECCLI
Choosing cli_command and/or eric_eccli_command modules for automation and configuration management

When started with configuration and automation on Ericsson nodes, found [eric_eccli_command](https://docs.ansible.com/ansible/latest/modules/eric_eccli_command_module.html) module introduced in Ansible 2.9 

All example of two commands (show version and show running-config), mentioned in the module, worked with ansible_connection and ansible_network_os introduced in the inventory, as per [ERIC_ECCLI Platform Options](https://docs.ansible.com/ansible/latest/network/user_guide/platform_eric_eccli.html). The predefined checks in result[0] and result[1], used in wait_for parameter, give clue to the Ansible user that at least commands are getting executed on the server(s)

result[0] can be used for all commands where the result would have string 'IPOS', similary the result[1] is set to look for string 'management' in the output. However result[i] vars are not available for Ansible user to use the output as per need, for example in debug module. Also 'IPOS' and/or 'management' strings may not be present always in the output every ECCLI. Is i = [0,1] otherwise what could be result[i] looking in the output where i >= 2? No relevant description found 

Irrespective of presumbale satisfaction that commmands are getting excuted on the server(s), the Ansible user stays blind on what is the output of the commands. The module does not support the register parameter to store the output in a var for Ansible user to review or further use.

[cli_command](https://docs.ansible.com/ansible/latest/modules/cli_command_module.html), introduced in Ansible 2.7, amazingly had no issue in running the said commands, described in [eric_eccli_command](https://docs.ansible.com/ansible/latest/modules/eric_eccli_command_module.html) documentation, on Ericsson ECCLI/IPOS network. And the module also supports registering the output.

Get your inventory ready with hosts and vars like ansible_connection, ansible_user, ansible_ssh_pass (though plain text not recommmended), ansible_network_os to try both modules

![724TD2](https://user-images.githubusercontent.com/47313728/88474627-6244ed00-cedd-11ea-9e6d-591317056991.png)
