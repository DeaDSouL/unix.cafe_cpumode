#!/bin/bash
# vim: tabstop=8 expandtab shiftwidth=4 softtabstop=4 foldmethod=marker
# ----------------------------------------------------------------------
# Author:   DeaDSouL (Mubarak Alrashidi)
# URL:      https://unix.cafe/wp/en/2020/07/toggle-between-cpu-powersave-and-performance-in-linux/
# GitHub:   https://github.com/DeaDSouL/unix.cafe_cpumode
# Twitter:  https://twitter.com/_DeaDSouL_
# License:  GPLv3
# ----------------------------------------------------------------------

# usage menu
function show_usage() { #{{{
    echo -e "USAGE:\t$0 powersave|performance|current"
    echo -e "\t\tpowersave\tSet CPU in power-saving mode."
    echo -e "\t\tperformance\tSet CPU in performance mode."
    echo -e "\t\tcurrent\t\tShow the current CPU mode."
    echo -e "\t\thelp\t\tShow this menu."
    exit 1
} #}}}

# our error exit function
function ee() { #{{{
    echo "$1"; exit 1
} #}}}

# get cpu mode
function getcpumode() { #{{{
    cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
} #}}}

# set cpu mode
function setcpumode() { #{{{
    [ $1 != 'powersave' -a $1 != 'performance' ] && ee 'Invalid given value..'
    [ $(getcpumode) == $1 ] && ee "It's already in '$1' mode"
    echo $1 | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
} #}}}

# make sure we have root's power
if [ $UID -ne 0 ]; then #{{{
    echo 'Script should be executed by "root"'
    ee 'Or prefixed with "sudo".'
fi #}}}

# get & set actions
case "$1" in #{{{
    performance)    setcpumode performance; exit 0              ;;
    powersave)      setcpumode powersave; exit 0                ;;
    current|get)    getcpumode; exit 0                          ;;
    help)           show_usage                                  ;;
    *)              ee "Try: $0 help"                           ;;
esac #}}}
