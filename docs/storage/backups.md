# Backups

First, add these to `~/.zshrc` to get the `benji`, `benji-restore-pvc` and `benji-command` commands on your local machine:

```
# Benji Aliases
do_benji_subcommand() {
  benji_pod=$(k get po -n backup-system --selector=app.kubernetes.io/component=maint,app.kubernetes.io/instance=benji,app.kubernetes.io/name=benji -o jsonpath='{.items[0].metadata.name}')
  k exec -i -n backup-system "$benji_pod" -c benji -- $@
  return "$?"
}
alias benji="do_benji_subcommand benji"
alias benji-restore-pvc="do_benji_subcommand benji-restore-pvc"
alias benji-command="do_benji_subcommand benji-command"
alias benji-backup-pvc="do_benji_subcommand benji-backup-pvc"
```

## Storage Stats

```
# note: this can take some time to return
benji storage-stats
+---------------+--------------+
| objects_count | objects_size |
+---------------+--------------+
|         19826 |      38.3GiB |
+---------------+--------------+
```

## Querying Backups

```
# get all backups
benji ls

# just get ones from less than a day ago
benji ls 'date > "1 day ago"'

# get backups for specific PVC
benji ls 'volume == "default/gitea-db-v1"'

# and you can combine them!
benji ls 'volume == "default/gitea-db-v1" and date > "1 day ago"'
```

## Restoring Backups

The command is long, mostly because I use a nonstandard `restore-url-template`.

```
# basic command with args
benji-restore-pvc \
  --pvc-storage-class rook-ceph-block \
  --restore-url-template "replicapool:{pool}/{image}" \
  <version uid> \
  <new namespace> \
  <new pvc name>
```

Example of restoring

```
# find the latest backup version uid
benji ls 'date > "1 day ago"'

# restore it to the "games" namespace
benji-restore-pvc \
  --pvc-storage-class rook-ceph-block \
  --restore-url-template "replicapool:{pool}/{image}" \
  default-hajimari-config-v1-l5krjs games hajimari-restored

Restoring version default-hajimari-config-v1-l5krjs to PVC games/hajimari-restored.
Waiting for persistent volume creation.
    INFO: Restored 1/8 blocks (12.5%)
    INFO: Restored 2/8 blocks (25.0%)
    INFO: Restored 3/8 blocks (37.5%)
    INFO: Restored 4/8 blocks (50.0%)
    INFO: Restored 5/8 blocks (62.5%)
    INFO: Restored 6/8 blocks (75.0%)
    INFO: Restored 7/8 blocks (87.5%)
    INFO: Restored 8/8 blocks (100.0%)
    INFO: Successfully restored version default-hajimari-config-v1-l5krjs in 04s with 6.9MiB/s.
```

# Restoring Benji Itself

TODO
