![image](https://raw.githubusercontent.com/szelcsanyi/remote-commander/master/commander.png) Remote-commander
================

## Description
Rcmdr is a script which runs a single command on multiple computers at the 
same time over ssh in parallel or one by one. With Zabbix intergration 
computer groups can be selected from the monitoring database.

## Requires
- mysql command line client
- ssh client
- zabbix (www.zabbix.com) database access 

## Installation
- Put rcmdr script into /usr/local/bin
- chmod +x /usr/local/bin/rcmdr
- Create mysql user with these permissions:
<pre>
GRANT USAGE ON *.* TO 'rcmdr'@'%' IDENTIFIED BY 'secretpassword'
GRANT SELECT ON 'zabbix'.'hosts_groups' TO 'rcmdr'@'%'
GRANT SELECT ON 'zabbix'.'hosts' TO 'rcmdr'@'%'
GRANT SELECT ON 'zabbix'.'groups' TO 'rcmdr'@'%'
</pre>
- Set up these variables
<pre>
ZABBIX_HOST="" # Database host
ZABBIX_DB="zabbix" # Database name
ZABBIX_USER="rcmdr" # Database user name
ZABBIX_PW="" # Database user password
</pre>

## Usage
<pre>
Usage: rcmdr --pool=WEB|DB... --host='host1[ host2 host3]' --excludepool=MEMCACHE... --excludehost='host1[ host2 host3]' --delay=sec [--parallel] [--parallelcount|--pcount] [--waitafterfirst|--waf] [--help] [--test] --command='hostname -f'

Description:
 --pool:              Destination target pool
                       Zabbix group like DB, WEB, etc.
 --host:              Destination hosts separated by spaces or commas
                       'app1.mydomain.com app2.mydomain.com'
 --excludepool:       Excluded destination pool
 --excludehost:       Excluded destination hosts separated by spaces or commas
                       'app1.mydomain.com app2.mydomain.com'
 --delay:             Delay between command execution on hosts
 --parallel:          Do the job in parallel on hosts
 --parallelcount:     Parallel execution concurrency if --parallel is set
 --pcount:            Short form of --parallelcount
 --waitafterfirst:    Pause after command execution on first host
 --waf:               Short form of --waitafterfirst
 --nocolor:           Do not color output messages
 --test:              Execute hostname -f and date
 --help:              This help screen
 --command:           Execute specified command
 --user:              Username for ssh connection (default: root)
 --silent:            Be less verbose. Start command execution immediately
 --jumphost:          Ssh jumphost. Connect destinaiton host via this host
 --jumphostuser:      Username for jumphost ssh connection
 example: rcmdr --pool=WEB --command='date'"
</pre>

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License

* Freely distributable and licensed under the [MIT license](http://szelcsanyi.mit-license.org/2014/license.html).
* Copyright (c) 2014 Gabor Szelcsanyi

[![image](https://ga-beacon.appspot.com/UA-56493884-1/remote-commander/README.md)](https://github.com/szelcsanyi/remote-commander)

