# containerglide
Implementation of the [autopilot pattern](http://autopilotpattern.io) without consul.

## Design
Containerpilot is designed as a lightweight "init"-like program for containers. It
manages started applications through their lifecycle, including starting and
stopping the applications, running periodic tasks such as backups, and capturing
the STDOUT and STDERR of the started applications and logging them to the container's
STDOUT and STDERR.

### Invariants
1. Applications started by containerglide should not perform the traditional "double-fork"
some do in order to "daemonize" themselves. Doing so will break the process monitoring of
containerglide as well as lose the ability to read the STDOUT and STDERR of the started process.

2. Pidfiles are considered unreliable and therefore are ignored.
