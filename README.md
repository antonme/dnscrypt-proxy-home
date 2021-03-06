# dnscrypt-proxy-home 2

Patched version of dnscrypt-proxy with some additional features. This features are mostly for local home use, and some of them may be a bit dangerous for using in public spaces.

### New features:

  * #### Permanent cache
    Save cache into a file on exit and load it back on start — so that restart will not neccessarily mean you lose all cache. Configured by `cache_persistent` and `cache_filename` options in config file

  * #### Forced cache mode
    Always answer from cache, even if it is expired. After answerring from expired cache, update cache even without request. As a result, we almost always answer in 0ms and the cache entries will not really be that old. Makes a big difference with high-latency connections (and on a very fast ones too). Configured by `cache_forced` and `cache_forced_ttl` options

  * #### Manually flush single query from cache
    Send `flush@www.github.com` query to remove `www.github.com` from the cache (same DNS record type removed as the one sent). Very useful for debugging, but may be not fully safe for public places. Configyred by `cache_flush_command` option
    
  * #### Log file additions
    * Added temporary support for `SVCB` and `HTTPS` DNS record types which are not yet supported by [miekg/dns](https://github.com/miekg/dns) module, but appear in the wild (and the logs) quite often. Here's [pull request](https://github.com/miekg/dns/pull/1067) at miekg/dns to monitor.
    * TTL now logged in for every query. 
    * Also, there are new types of responce in a log files:
      * `CACHE_HIT` - answered from cache
      * `FORCED_CACHE` - answered from a cache that has already expired
      * `POSTFETCH` - auto-query to update cache after `FORCED_CACHE`
     
   * #### Beautifier for a log file :)
     Makes monitoring a log file a bit easier
     ### [PICTURE TO BE]

# Readme of original dnscrypt-proxy:
# ![dnscrypt-proxy 2](https://raw.github.com/dnscrypt/dnscrypt-proxy/master/logo.png?3)

[![Financial Contributors on Open Collective](https://opencollective.com/dnscrypt/all/badge.svg?label=financial+contributors)](https://opencollective.com/dnscrypt)
[![DNSCrypt-Proxy Release](https://img.shields.io/github/release/dnscrypt/dnscrypt-proxy.svg?label=Latest%20Release&style=popout)](https://github.com/dnscrypt/dnscrypt-proxy/releases/latest)
[![Build Status](https://github.com/DNSCrypt/dnscrypt-proxy/workflows/CI%20and%20optionally%20publish/badge.svg)](https://github.com/DNSCrypt/dnscrypt-proxy/actions)
![CodeQL scan](https://github.com/DNSCrypt/dnscrypt-proxy/workflows/CodeQL%20scan/badge.svg)
![ShiftLeft Scan](https://github.com/DNSCrypt/dnscrypt-proxy/workflows/ShiftLeft%20Scan/badge.svg)
[![#dnscrypt-proxy:matrix.org](https://img.shields.io/matrix/dnscrypt-proxy:matrix.org.svg?label=DNSCrypt-Proxy%20Matrix%20Chat&server_fqdn=matrix.org&style=popout)](https://matrix.to/#/#dnscrypt-proxy:matrix.org)

## Overview

A flexible DNS proxy, with support for modern encrypted DNS protocols such as [DNSCrypt v2](https://dnscrypt.info/protocol), [DNS-over-HTTPS](https://www.rfc-editor.org/rfc/rfc8484.txt) and [Anonymized DNSCrypt](https://github.com/DNSCrypt/dnscrypt-protocol/blob/master/ANONYMIZED-DNSCRYPT.txt).

* **[dnscrypt-proxy documentation](https://dnscrypt.info/doc) ← Start here**
* [DNSCrypt project home page](https://dnscrypt.info/)
* [DNS-over-HTTPS and DNSCrypt resolvers](https://dnscrypt.info/public-servers)
* [Server and client implementations](https://dnscrypt.info/implementations)
* [DNS stamps](https://dnscrypt.info/stamps)
* [FAQ](https://dnscrypt.info/faq)

## [Download the latest release](https://github.com/dnscrypt/dnscrypt-proxy/releases/latest)

Available as source code and pre-built binaries for most operating systems and architectures (see below).

## Features

* DNS traffic encryption and authentication. Supports DNS-over-HTTPS (DoH) using TLS 1.3, DNSCrypt and Anonymized DNS
* Client IP addresses can be hidden using Tor, SOCKS proxies or Anonymized DNS relays
* DNS query monitoring, with separate log files for regular and suspicious queries
* Filtering: block ads, malware, and other unwanted content. Compatible with all DNS services
* Time-based filtering, with a flexible weekly schedule
* Transparent redirection of specific domains to specific resolvers
* DNS caching, to reduce latency and improve privacy
* Local IPv6 blocking to reduce latency on IPv4-only networks
* Load balancing: pick a set of resolvers, dnscrypt-proxy will automatically measure and keep track of their speed, and balance the traffic across the fastest available ones.
* Cloaking: like a `HOSTS` file on steroids, that can return preconfigured addresses for specific names, or resolve and return the IP address of other names. This can be used for local development as well as to enforce safe search results on Google, Yahoo, DuckDuckGo and Bing
* Automatic background updates of resolvers lists
* Can force outgoing connections to use TCP
* Compatible with DNSSEC
* Includes a local DoH server in order to support ECHO (ESNI)

## Pre-built binaries

Up-to-date, pre-built binaries are available for:

* Android/arm
* Android/arm64
* Android/x86
* Android/x86_64
* Dragonfly BSD
* FreeBSD/arm
* FreeBSD/x86
* FreeBSD/x86_64
* Linux/arm
* Linux/arm64
* Linux/mips
* Linux/mipsle
* Linux/mips64
* Linux/mips64le
* Linux/x86
* Linux/x86_64
* MacOS X
* NetBSD/x86
* NetBSD/x86_64
* OpenBSD/x86
* OpenBSD/x86_64
* Windows
* Windows 64 bit

How to use these files, as well as how to verify their signatures, are documented in the [installation instructions](https://github.com/dnscrypt/dnscrypt-proxy/wiki/installation).

## Contributors

### Code Contributors

This project exists thanks to all the people who contribute. [[Contribute](CONTRIBUTING.md)].
<a href="https://github.com/dnscrypt/dnscrypt-proxy/graphs/contributors"><img src="https://opencollective.com/dnscrypt/contributors.svg?width=890&button=false" /></a>

### Financial Contributors

Become a financial contributor and help us sustain our community. [[Contribute](https://opencollective.com/dnscrypt/contribute)]

#### Individuals

<a href="https://opencollective.com/dnscrypt"><img src="https://opencollective.com/dnscrypt/individuals.svg?width=890"></a>

#### Organizations

Support this project with your organization. Your logo will show up here with a link to your website. [[Contribute](https://opencollective.com/dnscrypt/contribute)]

<a href="https://opencollective.com/dnscrypt/organization/0/website"><img src="https://opencollective.com/dnscrypt/organization/0/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/1/website"><img src="https://opencollective.com/dnscrypt/organization/1/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/2/website"><img src="https://opencollective.com/dnscrypt/organization/2/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/3/website"><img src="https://opencollective.com/dnscrypt/organization/3/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/4/website"><img src="https://opencollective.com/dnscrypt/organization/4/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/5/website"><img src="https://opencollective.com/dnscrypt/organization/5/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/6/website"><img src="https://opencollective.com/dnscrypt/organization/6/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/7/website"><img src="https://opencollective.com/dnscrypt/organization/7/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/8/website"><img src="https://opencollective.com/dnscrypt/organization/8/avatar.svg"></a>
<a href="https://opencollective.com/dnscrypt/organization/9/website"><img src="https://opencollective.com/dnscrypt/organization/9/avatar.svg"></a>
