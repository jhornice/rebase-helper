How to use the rebase-helper for Upstream Monitoring systems
========================================================

The page describes the integration of the rebase-helper into upstream monitoring systems.
You need to install a rebase-helper package

- either as RPM::

  dnf install rebase-helper

- or from GitHub::

  git clone https://github.com/phracek/rebase-helper

Nowadays only koji build systems are used as a support for upstream monitoring systems.


## Patch the new sources and run koji scratch build

### Python API usage::

   from rebasehelper.application import Application
   cli = CLI(['--non-interactive', '--builds-nowait', '--buildtool', 'fedpkg', 'upstream_version'])
   rh = Application(cli)
   rh.set_upstream_monitoring() # Switch rebase-helper to upstream release monitoring mode.
   rh.run()
   rh.get_rebasehelper_data() # Get all information about the results

### Bash usage::

    rebase-helper --non-interactive --builds-nowait --buildtool fedpkg upstream_version

## Download logs and RPMs for comparing with checkers

### Python API usage::

   cli = CLI(['--non-interactive', '--builds-nowait', '--buildtool', 'fedpkg', '--build-tasks', 'old_id,new-id'])
   rh.run() # Downloads RPMs, logs and runs checkers and provides logs.
   rh.get_rebasehelper_data() # Gets all the information about the results

### Bash usage::

   rebase-helper --non-interactive --builds-nowait --buildtool fedpkg --build-tasks old_id,new-id

