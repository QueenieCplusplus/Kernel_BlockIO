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
    
建立優先 high & low 程度群組：

    # mkdir /cgroup/high
    # mkdir /cgroup/low

優先程度下設定 weight 權重值：

    // 初始值為 500，根群組權重初始值為 1000
    # echo 1000 > /cgroup/high/blkio.weight
    # echo 100 > /cgroup/low/blkio.weight
    
簡單的腳本：

    // blkio_test.sh
    
    
    # ! /bin/sh
    
    #  blkio_test.sh
    # Test Script for Block IO Controller
    # read /mnt/sdb/low.dat($flow)as cgroup $cg_low
    # and read /mnt/sdb/high.dat($fhigh)as cgroup $ cg_high simultaneously.
    #
    # $1: cgroup path for lower priority (--> $cg_low)
    # $2: cgroup path for higher priority (--> $cg_high )

(to be continued...)
