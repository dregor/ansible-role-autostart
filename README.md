Makes and starts servise files for your own scripts, that must be started after reboot.
Example:

```yaml
sd_autostart:
  - name: disableHugepage
    description: Disable hugepage
    exec_start:  /bin/sh -c 'echo "never" | /usr/bin/tee /sys/kernel/mm/transparent_hugepage/enabled'
    templated: no
  - name: changeIOShedulerToCFQ
    description: Change IO sheduler to  CFQ for disk %I
    exec_start:  /bin/sh -c 'echo "cfq" | /usr/bin/tee /sys/block/%i/queue/scheduler'
    subitems:
      - sda
      - sdb
  - name: changeReadahead
    description: Change readahead for disk %I
    exec_start:  /usr/sbin/blockdev --setra 8192 /dev/%i
    subitems:
      - md2
```

### Be careful don't make it 'autostart', before testing!