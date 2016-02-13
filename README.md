# git-hooks #

Some of these git hooks might actually be good for something

## update-auth-merge ##

### What it is ###

This update hook is written in python2 and offers two policies which are configured on a per-branch basis.
The hook expects your platform to have a binary named "python2" somewhere along its PATH, so if it doesn't,
throw your archaic OS in the garbage and use one that gets with the times (or modify the hashbang line accordingly).

1. Require all updates to the target branch to be merge commits
2. Require all updates to the target branch to be signed with a validated GPG key

### How to use it ###

Create a file inside of your git repository folder (e.g., your .git in a non-bare repository) along the path `hooks-data/conf/update.json`.
This is a hard-coded path. This JSON file is expected to contain an object in which the keys are strings which name each branch to add 
policies to. For each such branch, the value should be another JSON object which contains the policy configurations. 
The policy configuration object has two effective keys, expected to be defined as strings.

1. *merge-only*: The value for this key is expected to be a boolean. When true, this branch will reject any updates which are not merge commits.
2. *auth-only*: If this key exists and defines a valid filesystem directory as its value, this branch will reject any updates which are not signed
   with a verifiable PGP signature. The directory defined in this option will be used as the GNUPGHOME when verifying signatures.

### Extras ###

If you or one of your users receives a message stating "Internal error ocurred", then the error message should also provide
an error code. You can use this error code to look up the exact error in the hook log file. The hook will log errors to
`hooks-data/log/update.log`. If the error message state "Unidentified internal error", then the error ocurred before logging
could be successfully setup, and you're on your own to identify the problem.

**Dumb caveat**: The error log messages currently do not include timestamps. This is for no other reason than my own laziness and lack of need.
Pull requests welcome :)
