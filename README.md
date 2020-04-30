# Kernel_BlockIO

Block IO 是 Cgroup 子系統之一，實作部分在 I/O scheduler 輸出入排程器中。

編譯時使用選項：

    CONFIG_BLK_CGROUP

    CONFIG_CFO_GROUP_IOSCHED

修正的設定檔案：

    /boot/grub/grub.conf
    
Scheduler 排程器檔案內容會隨裝置種類而有不同，I/O Scheduler 用於 Block Device （磁碟）區塊裝置上。

掛載後使用選項傳入：

    # mount -t cgroup -o bliko cgroup /cgroup
    
控制 I/O 優先程度：

    # echo cfq > /sys/class/block/sdb/queue/scheduler
    $ cat /sys/class/block/sdb/queue/scheduler
    
建立優先 high & low 程度群組:

    # mkdir /cgroup/high
    # mkdir /cgroup/low

