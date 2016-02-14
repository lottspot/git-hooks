# git-hooks #

Some of these git hooks might actually be good for something

## update-auth-merge ##

### What it is ###

This update hook is written in python2 and offers two policies which are configured on a per-branch basis.
The hook expects your platform to have a binary named "python2" somewhere along its PATH, so if it doesn't,
throw your archaic OS in the garbage and use one that gets with the times (or modify the hashbang line accordingly).
The policies offered to each branch by this hook are:

1. Require all updates to the target branch to be merge commits
2. Require all updates to the target branch to be signed with a validated GPG key

### Configuration ###

The hook uses the following git config directives:

- **hook.<name>.logPath**            : *(path)*      Path to the hook error log file. Defaults to info/<name>.log
- **branch.<name>.enforceMergeOnly** : *(boolean)*   Enforce a merge-only policy on the named branch. Defaults to off
- **branch.<name>.enforceAuthOnly**  : *(boolean)*   Enforce an auth-only policy on the named branch. Defaults to off
- **branch.<name>.authGpgHome**      : *(directory)* Directory to use as GNUPGHOME when enforcing auth-only policy on named branch. Defaults to system value
