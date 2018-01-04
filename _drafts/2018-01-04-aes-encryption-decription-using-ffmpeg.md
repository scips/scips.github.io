---
layout: post
categories: truc de g33k
tags: AES-128, AES, ffmpeg
title: AES Encryption using aes-128 from A ot Z
meta:
    synopsys: I need a full case where I encrypt video / stream with AES-128 till it reach the browser
author:
    name: Sébastien Barbieri
    website: https://scips.github.io/
    twitter: scips
    email: sebastien.barbieri@gmail.com
---

# AES Encryption using aes-128 from A ot Z

## General architecture

* **STATIC** A web server to serve static files media and html (oneliner node is fine)
* **STREAM** A streamer to stream live content (vlc for instance)
* **BROWSER** A browser to consume the content

## Useful command line instructions

### Generate AES-128 keys

ffmpeg use [key info file](1)

#### Key info file example:

    http://server/file.key
    /path/to/file.key
    0123456789ABCDEF0123456789ABCDEF

the last line is the initialisation vector and is not mandatory if it's not present the segment sequence will be used instead.

#### Shell script to generate the m3u8

    #!/bin/sh
    BASE_URL=${1:-'.'}
    openssl rand 16 > file.key
    echo $BASE_URL/file.key > file.keyinfo
    echo file.key >> file.keyinfo
    echo $(openssl rand -hex 16) >> file.keyinfo
    ffmpeg -f lavfi -re -i testsrc -c:v h264 -hls_flags delete_segments -hls_key_info_file file.keyinfo out.m3u8

### Encrypt a video with ffmpeg

    ffmpeg -i video.mp4 -hls_time 10 -hls_key_info_file file.keyinfo stream.m3u8

    ffmpeg -i $input -vcodec libx264 -acodec libvo_aacenc -b:v 128k -flags -global_header -map 0:0 -map 0:1 -f segment -segment_time 4 -segment_list_size 0 -segment_list list.m3u8 -segment_format mpegts stream%d.ts

## Simple encryption decryption to test

### Let's create an m3u8

in a clean folder */encryption-test-aes-128* put you source file: *video.mp4*

#### create keys

in bash:

    openssl rand 16 > file.key

edit a file: file.keyinfo and put

    http://127.0.0.1:8000/file.key
    file.key

we don't set the IV (initialization vector)

#### encrypt

in bash: 

    ffmpeg -threads 0 -i video.mp4 -strict -2 -c:v h264 -hls_key_info_file file.keyinfo out.m3u8

this will create a bunch of outxx.ts files and the out.m3u8 file

## Links

[1](http://ffmpeg.org/ffmpeg-all.html) search for **hls\_key\_info\_file**