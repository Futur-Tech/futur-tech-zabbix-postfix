# zabbix-postfix-template
Zabbix template for Postfix SMTP server

Works for Zabbix 4.x

Forked from http://admin.shamot.cz/?p=424

# Requirements
* [pflogsum](http://jimsun.linxnet.com/postfix_contrib.html)
* [pygtail](https://pypi.org/project/pygtail/)

# Installation
    # for Ubuntu / Debian
    apt-get install pflogsumm pygtail
    
    # for CentOS
    yum install postfix-perl-scripts
    
    # ! check MAILLOG path in zabbix-postfix-stats.sh
    cp zabbix-postfix-stats.sh /usr/bin/
    chmod +x /usr/local/bin/zabbix-postfix-stats.sh

    cp userparameter_postfix.conf /etc/zabbix/zabbix_agentd.d/
    
    # run visudo as root
    
    visudo /etc/sudoers.d/zabbix-postfix
    
    Defaults:zabbix !requiretty
    zabbix ALL=(ALL) NOPASSWD: /usr/local/bin/zabbix-postfix-stats.sh
    
    # or 
    tee /etc/sudoers.d/zabbix-postfix << EOF
    Defaults:zabbix !requiretty
    zabbix ALL=(ALL) NOPASSWD: /usr/local/bin/zabbix-postfix-stats.sh
    EOF

    systemctl restart zabbix-agent

Finally import template_app_zabbix.xml and attach it to your host
