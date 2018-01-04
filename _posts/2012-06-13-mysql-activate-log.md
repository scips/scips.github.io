---
layout: post
categories: truc de g33k
tags: MariadDB, Mysql, log
title: Activate full log MariaDB/Mysql
meta:
    synopsys: Where you learn how to enable/disable mysql log
author:
    name: Sébastien Barbieri
    website: https://scips.github.io/
    twitter: scips
    email: sebastien.barbieri@gmail.com
---

# Activate full log MariaDB/Mysql

## Set the log filename

    db001 [(none)]> SET GLOBAL general_log_file = '/var/log/mysql/full.log';

## activate full log

    db001 [(none)]> SET GLOBAL general_log = 'ON';

## deactivate full log

    db001 [(none)]> SET GLOBAL general_log = 'OFF';

