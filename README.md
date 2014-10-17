# POODLE Checker

Scans a target host (domain or IP) to see if it accepts SSL connections with the SSLv3 protocol.

## System Requirements
* Python 2
* An SSL library that supports SSLv3

## Basic Usage

	python checker.py <domain>

where `domain` is an IP address or a DNS name. Technically it can be anything that Python understands as a hostname.

An output of `https (443): No Answer` indicates the server is not listening on port 443 (or is very slow - see `--timeout`). An output of `https (443): Rejected` indicates that the server does not accept connections with the SSLv3 protocol. An output of `https (443): **WARNING** CONNECTION ACCEPTED` indicates that the server does accept https connections with SSLv3. 

## Additional Arguments

`--timeout` (`-t`): Specify the number of seconds to wait for a response on a port before moving to another port.

`--quiet (-q)`: Suppress messages about certain services not existing (only show messages about rejected and accepted connections).

`--ports (-p)`: Specify which groups of ports to scan. Options include `https`, `msg`, `web`, `file`, `db`, and `all`. `msg` covers typical SSL email ports as well as SSL chat ports (XMPP, IRC, etc.). `web` covers cPanel and related services. `file` covers file transfer protocols such as sftp, ftps, scp, and ldap. `db` covers secure connections to internet-facing databases such as MySQL, MSSQL, and Oracle.

Putting all of the above together, you might end up with a command such as:

	python checker.py -q -t 2.5 -p all google.com

The above command will scan all known SSL ports on google.com and report back any that accept or reject an SSLv3 encrypted connection. We will also wait 2.5 seconds before deciding that a service is non-existent and we should check the next one.