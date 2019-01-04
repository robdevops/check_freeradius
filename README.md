# check_freeradius

Nagios / Icinga plugin. Checks if the FreeRADIUS status server responds correctly. Also returns performance data.

Based on [collectd-freeradius](https://github.com/kshcherban/collectd-freeradius) by [kshcherban](https://github.com/kshcherban/).

## Usage
```
Usage: check_freeradius -s <SECRET> [options]

Options:
  -h, --help            show this help message and exit
  -H HOST, --host=HOST  RADIUS server. Defaults to localhost.
  -p PORT, --port=PORT  RADIUS server port. Defaults to 18121.
  -s SECRET, --secret=SECRET
                        RADIUS secret. Required.
  -t STATSTYPE, --type=STATSTYPE
                        FreeRADIUS-Statistics-Type. 1 for Authentication &
                        Authorisation. 2 for Accounting. 3 for Both. Defaults
                        to 3.
  -w TIMEOUT, --wait=TIMEOUT
                        Response timeout in seconds. Defaults to 3.
  -z, --zero            Include counters of value 0. Uses more disk space.
 ```
 
## Example Output
```
$ check_freeradius --secret SECRET --zero
```
```
OK: Received response ID 2, code 2, length = 224 |auth_malformed_requests=0;;; acct_invalid_requests=0;;; access_requests=513523;;; access_accepts=513413;;; auth_dropped_requests=96;;; accounting_responses=0;;; acct_malformed_requests=0;;; auth_responses=513425;;; auth_invalid_requests=2;;; auth_duplicate_requests=0;;; acct_unknown_types=0;;; access_rejects=12;;; access_challenges=0;;; acct_duplicate_requests=0;;; acct_dropped_requests=0;;; auth_unknown_types=0;;; accounting_requests=0;;; 
```
```
$ echo $?
0
```

```
$ check_freeradius -s SECRET
```
```
WARNING: radclient: no response from server for ID 135 socket 3
```
```
$ echo $?
1
```

## Dependencies
Enable the [FreeRADIUS status server](http://wiki.freeradius.org/config/Status) to use this script. 

