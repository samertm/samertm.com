title: changes in ram usage from 2gb to 8gb in this old laptop
date: 2014-06-03 19:00
---

I've been aching for an x86 laptop for a while now, and I found my Dad's old laptop, an HP ProBook 4510s from 2009, in his closet. After successfully installing Ubuntu 14.04 (after multiple failed attempts to put Arch on it), it became a useable laptop! It only had 2gb of RAM, though, and I kept bumping into issues with it. Starting the terminal immediately after closing it was noticeably sluggish, and it would start swapping if I had too many tabs open in firefox. I was constantly closing unused tabs and applications so I could have enough space to breath.

I bought 8gb of ram (after buying 6gb of DDR2 ram that didn't fit, whoops) and thought it would be fun to record the results! I used a simple shell script hooked up to /proc/meminfo to gather the data, and I recorded my memory usage for about the same amount of time for the before and after data:

    #!/bin/bash
    
    OUT=mem_after # or whatever you want to name the output file
    MATCH="(^MemTotal:|^MemFree:|^Cached:|^Active:|^Inactive:)"
    
    while [ 1 ] ; do
        echo "start" $(date +%s) >> $OUT
        /bin/grep -E -e $MATCH /proc/meminfo >> $OUT
        sleep 5
    done

And here are the results:

*06-01-2018: Unfortunately, the results have been lost to the sands of time*

And what are my conclusions? I'm not exactly sure :P 
