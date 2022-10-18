# Syslog and Terminal Messages #

## Terminal Messages ##

By default, users connected to the console recveive messages for all severity levels. This happens because of the default ```logging console``` global configuration command.

Other users that are connected in with either Telnet or SSH don't see those messages by default. To enable that requires us to run two commands. IOS has another global configuration setting that tells IOS to enable the sending of log messages to all logged users.

logging monitor

This is not enough to allow users to see the log messages. The user must also issue the following command during the login session. This tells IOS that this terminal would like to receive log messages.

terminal monitor

## Syslog ##

It's good to keep log messages for later review. IOS provides two means to save these messages.

1. IOS can store copies of log messages in RAM by issuing command number 1, done in global configuration mode. You view saved log messages by typing in command no 2.

logging buffered

show logging

 2. This option is more widely used. All devices store their log messages on a syslog server. To configure a router or switch to send log messages to a syslog server is pretty straightforward. This is done in global configuration mode.

To see the options for logging.
logging ?

To send log messages to a syslog server.
logging host {address | hostname}

IOS has uses the following categories for Syslog messages.

- Timestamp.
- What generated the message, e.g., what interface.
- The severity level.
- A mnemonic for the message, a short text string that describes the message.
- The description of the message.

### These are the severity levels ###

| Keyword         | Numeral | Description                |
|-----------------|---------|----------------------------|
| Emergency alert | 0       | System is unusable.        |
| Alert           | 1       | Immediate action required. |
| Critical        | 2       | Critical Event.            |
| Error           | 3       | Error Event.               |
| Warning         | 4       | Warning Event.             |
| Notification    | 5       | Normal, More Important.    |
| Informational   | 6       | Normal, Less Important.    |
| Debug           | 7       | Requested by User Debug.   |

You can swap out the timestamp in global config for a sequence number if that's your thing.

no service timestamps
service sequence-numbers

### How to configure logging message level for each log service ###

| Service  | To Enable Logging                | To Set Message Levels                       |
|----------|----------------------------------|---------------------------------------------|
| Console  | logging console                  | logging console level-name \| level-number  |
| Monitor  | logging monitor                  | logging monitor level-name \| level-number  |
| Buffered | logging buffered                 | logging buffered level-name \| level-number |
| Syslog   | logging host address \| hostname | logging trap level-name \| level-number     |

## Debug Command ##

Debug is a powerful command that has a lot of option. As we can see on the table above us, it's number 8 on the list but I guess that's like saving the best for last?

With the debug EXEC command we can ask IOS to monitor certain events and log messages when those events occur. The debug command does take up CPU resources so we should be careful when using debug commands on production devices.

We can limit the amount of messages sent to the syslog server, based on severity, with the following command.

logging trap ?

This shows us the options we can work with. If we just want to log informational messages that equal severity 6.

logging trap informational

Notice that you can either use the number or the actual severity level name. If you select level 6, **remember that you don't just receive level 6 but messages from levels 0 through 6.**

