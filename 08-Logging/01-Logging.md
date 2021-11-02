***
# Case Statements
***
***
* Logs are the who, what, when, where and why
* You want logs - output may scroll off the screen, or your script may run unattended (via cron, etc..)

***
***
# Syslog
* Linux uses the syslog standard for message logging
* the syslog standard uses the facilities and severities to categorize messages
### Facilities
* facilities are used to indicate what part of the system the message originated from
* Facilities: kern, user, mail, daemon, auth, local0, local7
### Severities
* Severities: emerg, alert, crit, err, warning, notice, info
### Log locations
* Log file locations are configurable
```
# ex:
/var/log/messages
/var/log/syslog
```
***
***
# Logging with logger
* logger is a utility
by default it creates user.notice messages
* generic log:
```
logger "message"
# output: Aug 2 01:22:34 linuxsvr username: Message
```
* specify the facility and severity
```
# -p if you want to specify the facility and severity
logger -p local0.info "Message" 
# output: Aug 2 01:22:34 linuxsvr username: Message
```
* display the message on screen and send it to the logs
```
# -s if you want to display the message onscreen
logger -s -p local0.info "Message"
# outpt on screen: username: Message
```
* tag the log message
```
# -t if you want to tag the message (usually is the name of the script)
logger -t myscript -p local0.info "Message"
# output: Aug 2 01:22:34 linuxsvr myscript: Message
```
* include the PID
```
#-i to include the PID in the log message
logger -i -t myscript "Message"
# output: Aug 2 01:22:34 linuxsvr myscript[12986]: Message
```
***
***
# Custom function to handle logging
* you can make a function to handle logging
```
#!/bin/bash

VERBOSE=false
HOST="google.com"
PID="$$"
PROGRAM_NAME="$0"
THIS_HOST=$(hostname)

logit () {
  local LOG_LEVEL=$1
  # shifts the params to contain all but the first param
  shift 
  MSG=$@
  TIMESTAMP=$(date +"%Y-%m-%d %T")
  if [ $LOG_LEVEL = 'ERROR' ] || $VERBOSE
  then
    echo "${TIMESTAMP} ${THIS_HOST} ${PROGRAM_NAME}[${PID}]: ${LOG_LEVEL} ${MSG}"
  fi
}

logit INFO "Processing data."

fetch-data $HOST || logit ERROR "Could not fetch data from $HOST"
```