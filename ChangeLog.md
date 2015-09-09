Change Log
==========

All notable changes to the project are documented in this file.

[UNRELEASED][]
--------------

Minor bugfix release.

### Changes
- Support for new API at https://tunnelbroker.net, fixes issue #83.
  Use `default@tunnelbroker.net` to use the DYN.com API to update
  the IPv4 address for your IPv6-in-IPv4 tunnel.  Thanks goes to
  Horst Venzke for reporting this problem.
- The old API for the IPv6-in-IPv4 system `ipv6tb@he.net` is now
  deprecated.  Users should migrate to `default@tunnelbroker.net`

### Fixes
- Fix issue #100: regression from [1.99.13][] pidfile is no longer
  created.  Inadyn 1.x semantics incompatible with OpenBSD `pidfile()`
  that replaced local version in [1.99.14][].  Problem found by
  David Schury.


[1.99.14][] - 2015-07-14
------------------------

Improved support for configuring custom DDNS providers and support for
running in Windows, using Cygwin!

### Changes
- New setting `append-myip` which, instead of appending your hostname
  alias, appends the current IP to the server GET update URL.  See
  [README][README.md] or the man pages for more details.
- Prevent Inadyn from bugging out if it cannot write a cache file when
  the `-o, --once` flag is given.
- Inadyn now defaults to a silent build, use V=1 (like Linux) to get a
  verbose build.  Useful for auto-builders etc.
- Migrate to [libite][] for functions like `pidfile()`, `strlcpy()` etc.
- Add support for <http://GiraDNS.com>, thanks to Thorsten Mühlfelder!
- Add support for <https://www.duiadns.net>, thanks to Ionut Slaveanu!
- Add Cygwin support for running Inadyn in Windows, thanks to Scott Mann!

### Fixes
- Sanitized default logs by placing conditions for debug logs.  Thanks
  to Frank Aurich for this work!
- Fix issue #82: build failure, no rule to build target CHANGELOG, a
  regression introduced in [1.99.13][].
- Fix Duck DNS support, thanks to Ismani Nieuweboer!


[1.99.13][] - 2015-02-08
------------------------

### Changes
- Add support for <https://domains.google.com> DDNS, by Justin McManus
- Add support for <https://www.ovh.com> DDNS service, by Andres Gomez
- Add support for <http://dtdns.com> DDNS, by Denton Gentry
- Rename `NEWS.md` to `CHANGELOG.md` and update formatting in an attempt
  to align with <http://keepachangelog.com> -- this also means using ISO
  date format, finally!

### Fixes
- Fix issue #78: Parsing checkip responses may fail, by Andy Padavan
- Fix issue #79: Don't treat inline '#' as comment if not preceeded by
  space, by Andy Padavan


[1.99.12][] - 2014-10-20
------------------------

### Changes
- Add custom support for <http://Namecheap.com>, by Terzeus S. Dominguez

### Fixes
- Fix cross compilation issues with OpenSSL (depends on libcrypto)
- Fix cross compilation issues with `malloc` vs. `rpl_malloc` (removed
  autoconf check completely)


[1.99.11][] - 2014-10-15
------------------------

### Changes
- Add support for <https://nsupdate.info>, thanks to Thomas Waldmann
- Add support for <https://www.loopia.com> DynDNS service extension
- Add support for <https://duckdns.org>, thanks to Andy Padavan
- Updated man pages, both `inadyn(8)` and `inadyn.conf(5)` with examples

### Fixes
- Fix building on FreeBSD by converting to use GNU Configure & Build system
- Fixes to add support for TLS 1.x with SNI, thanks to Thomas Waldmann
- SSL mitigation fixes for POODLE


[1.99.10][] - 2014-09-13
------------------------

### Changes
- Refactor string functions `strcat()` and `strcpy()` to use secure
  OpenBSD replacements `strlcat()` and `strlcpy()` instead.

### Fixes
- Fix issue #57: `snprintf()` causes loss of \= from password string
- Fix issue #58: Add support for GnuTLS as the default SSL library
- Fix bugs found by Coverity Scan
- Fix memory leaks found by GLIBC (!) on PowerPC
- Fix include order problem with `error.h`


[1.99.9][] - 2014-05-21
-----------------------

### Changes
- Support for <http://www.zerigo.com> DDNS provider
- Support for <http://www.dhis.org> DDNS provider

### Fixes
- Fix memory leak in new HTTPS support, found by Valgrind
- Other misc. Valgrind and Cppcheck fixes


[1.99.8][] - 2014-05-20
-----------------------

### Changes
- Support for HTTPS to secure login credentials at DNS update, issue #36
- Support for persistent cache files with new `--cache-dir PATH`
- Support for <http://twoDNS.de> in generic plugin, see
  [README][README.md] for details
- Man page updates


[1.99.7][] - 2014-05-14
-----------------------

### Changes
- Support for multiple cache files, one per DDNS provider, issue #35
- Refactor DDNS providers as plugins, issue #30


[1.99.6][] - 2013-12-25
-----------------------

### Changes
- Update documentation for custom servers and add missing compatibility
  entry for custom servers.

### Fixes
- Fix nasty socket leak.


[1.99.5][] - 2013-11-27
-----------------------

### Changes
- Support for `--fake-address` on new `SIGUSR1` (forced update)
- Support for `SIGUSR2` (check now),
- Support for `--startup-delay SEC`, for embedded systems
- Man page updates

### Fixes
- Many minor bug fixes


[1.99.4][] - 2013-08-08
-----------------------

This release fixes a base64 password encoding regression in [1.99.3][]


[1.99.3][] - 2013-07-15 [YANKED]
--------------------------------

This release adds the ability to specify the cache file and the ability
to check the IP of the interface (UNIX only).  If no interface is
specified, no external IP check is performed.  The old `--iface` option
has been renamed `--bind`. changeip.com support has been added.  Minor
bugfixes and code optimizations have been made.

### Changes
- Add ability to specify cache file
- Add ability to check IP of interface (UNIX only).  If interface is
  specified, no external IP check performed Old `--iface` option renamed
  to `--bind`
- Specify IP address in freedns.afraid.org update request (only
  autodetect was used)
- Add changeip.com support

### Fixes
- Minor bugfixes and code optimization


[1.99.2][] - 2012-09-07
-----------------------

### Changes
- Get HTTP status description

### Fixes
- Fix inability to change update period (broken in 1.99.0)
- Fix debug output description


[1.99.1][] - 2012-09-01
-----------------------

### Changes
- Make HTTP status code check server-specific
- Update maintainer e-mail address


[1.99.0][] - 2012-08-17
-----------------------

### Changes
- Merge wl500g patches from <http://code.google.com/p/wl500g>:
  - `120-heipv6tb.patch` adds support for tunnelbroker
  - `121-hedyndns.patch` adds support for HE dyndns
  - `210-wildcard.patch` makes wildcard option account specific
- For ddns services that have their own checkip service, use it instead of
  dyndns.org checkip service
- Add ability to handle non-fatal temporary errors ("update too often",
  system error etc.)
- Warn if initial DNS request failed
- Add dnsexit.com support
- Modify http client to parse response for http status code and response
  body
- Remove DynDNS ignored and deprecated parameters (wildcard, mx, backmx,
  system). Wildcard kept for easydns.com
- Report detected IP to sitelutions and dynsip servers (only autodetect
  was used)
- Update TZO support
- Check HTTP status code before validating response
- Remake zoneedit response validation
- Little code cleanup

### Fixes
- Fix malformed HTTP request


[1.98.1][] - 2011-07-18
-----------------------

### Changes
- Preserve time since last update (forced update counter) and num
  interations from being reset by `SIGHUP` restart command
- Extend `--drop-privs` to support hyphens
- Cleanup of inadyn log messages, reformat & clarification

### Fixes
- Bug fix segfault at initial DNS lookup
- Bug fix `--drop-privs` uid/gid was swapped and a possible buffer overflow
- Typo fixes and polish to man pages inadyn(8) and inadyn.conf(5)


[1.98.0][] - 2011-02-28
-----------------------

### Changes
- New config file, command line, syntax (still backwards compatible!)
- New option `--drop-privs USER[:GROUP]` to support privilege separation
- Drop privileges before creating any files
- Documentation updates


[1.97.4][] - 2010-11-02
-----------------------

### Changes
- Support for dynsip.org by milkfish, from DD-WRT
- Add support for sitelutions.com, from inadyn-mt (untested)

### Fixes
- Clear DNS cache before calling `getaddrinfo()`, fixes GitHub issue #3


[1.97.3][] - 2010-11-02
-----------------------

### Changes
- Merge wl500g patches from <http://code.google.com/p/wl500g>:
  - `101-http-request.patch`. This cleans up the DDNS server defintions
	and callbacks, evidently originating from ideas implemented by
	DD-WRT.
  - `102-zoneedit.patch`. This fixes issues in what appears to be both
	request and response formats in ZoneEdit DDNS. Originating from
	DD-WRT.
  - `103-tzo.patch`. This patch adds support for tzo.com DDNS serivices.
  - `110-dnsomatic.patch`.  This patch adds support for DNS-O-Matic
	<http://dnsomatic.com/>, an OpenDNS service which can act as a
	"meta" update to several other DDNS service providers.
  - `120-heipv6tb.patch`. This patch adds support for Hurricane Electric's
	http://tunnelbroker.net/ DDNS services <https://dns.he.net/>.
- When starting: always use cache file, if it exists, or seed with DNS
  lookup

### Fixes
- Fix Debian bug #575549: freedns.afraid.org example in `inadyn(8)` is
  incorrect.


[1.97.2][] - 2010-10-30
-----------------------

### Changes
- Replace `gethostbyname()` with `getaddrinfo()` and improve logging at
  `connect()`

### Fixes
- Fix missing man pages from install/uninstall targets
- Fix GitHub issue #2: `setsocktopt()` takes pointer to `struct
  timeval`, not `int` as argument


[1.97.1][] - 2010-10-19
-----------------------

### Changes
- Add support for properly restarting inadyn on `SIGHUP`
- Remove `INADYN:` prefix in `MODULE_TAG` entirely - messes up syslog
  output


[1.97.0][] - 2010-10-18
-----------------------

- Apply patches by Neufbox4 from <http://dev.efixo.net>:
  - `100-inadyn-1.96.2.patch`, cache file support
  - `100-inadyn-1.96.2.patch`, bind interface support
  - `200-inadyn-1.96.2-64bits-fix.patch`
  - `300-inadyn-1.96.2-pidfile-and-improve.patch`
- New [README][README.md], COPYING and LICENSE file, remove readme.html
- Refactor and cleanup Makefile (renamed from makefile)
- Add support for `SIGTERM` signal
- Relocate include files to include directory
- Apply patch for multiple accounts from Christian Eyrich
- Remove unused `uint typedef` causing trouble on ARM GCC 4.4.x
- Fix missing `strdup()` of input config file and free any preexisting
- Make sure `TYPE_TCP` enum relly is 0 on all compilers
- Improve error messages using `strerror()` and use `-1` as stale
  socket, not `0`
- Fix nasty socket leak
- Merge with inadyn-advanced, <http://sf.net/projects/inadyn-advanced>:
  - Add support for 3322.org and easydns.org
  - Add support for domain wildcarding, `--wildcard` option NOTE: Domain
    wildcarding is now *disabled* by default
  - Add support for running an external command hook on IP update, new
	`--exec` option
  - Add support for datetime in debug messages
- Refactor `DBG_PRINTF((..))` --> `logit(..)`
- Update man page `inadyn(8)` with info on `--bind_interface`,
  `--wildcard`, `--exec` options and support for easydns.org
  and 3322.org services
- Misc fixes and cleanups


1.96.2 - 2007-03-12
-------------------

### Fixes
- If the Dynamic DNS server responds with an error Inadyn will abort.
  This will prevent further retries with wrong dyndns credentials.
- Default port number included in the request, to support the requests
  via Proxy, to ports different than 80.
- Simplified main inadyn update loop function. (there was no bug there)


1.96 - 2005-09-09
-----------------

### Changes
- zoneedit.com supported.
- no-ip.com supported.
- support for generic DNS services that support HTTP updates

### Fixes
- Immediate exit in case of --iterations=1 (not after a sleep period)
- Add missing option for specifying the path in the DNS server


1.95 - 2005-07-20
-----------------

### Changes
- UNIX signals supported - inadyn will stop gracefully in case of ALRM,
  HUP, INT, ...
- New dynamic DNS service supported - www.zoneedit.com - Not tested!
- Makefile adjusted for Solaris - compilable under Solaris.
- Support for generic DYNDNS service that supports update via HTTP with
  basic authentication not yet fully complete. Not known where might be
  applicable.


1.90 - 2005-02-24
-----------------

### Changes
- New option `--change_persona uid:gid` - inadyn can switch the user
  after launch. Typical feature for daemons
- Addition to `--ip_server_name` feature, now it has another parameter:
  the URL to read from the given server name
- Reduced some error messages
- Manual pages updated. (thanks to Shaul Karl)

### Fixes
- Typo fixed (`--ip_server_name` option)


1.86 - 2005-01-30
-----------------

### Changes
- Updated UNIX man pages for inadyn.  Even a page for `inadyn.conf`,
  Thanks to Shaul Karl!
- Inadyn doesn't print anything (e.g. ver. number) anymore when goes to
  background
- New config file parser. Accepts ESCAPE character: `\`

### Fixes
- Corrected check of the return code from `socket()` call


1.85 - 2005-01-10
-----------------

### Changes
- Config file related enhancements:
  - Use default location for config file, when no arguments for inadyn
  - More *NIX like format for the config file.  Thanks to Jerome Benoit

### Fixes
- When 'iterations' option is specified as being '1', inadyn exits
  immediately after first update, not after the sleep period as before


1.81 - 2004-11-23
-----------------

### Changes
- No new features, just a better integration with Linux.  Reviewed usage
  of syslog and fork to background in daemon mode, thanks to Shaul Karl.

1.80 - 2004-10-16
-----------------

### Changes
- Optional output to syslog for Linux, should work for all *nix systems
- Run in background for Linux, should work for all *nix systems

### Fixes
- Minor compile warnings removed


1.70 - 2004-07-05
-----------------

### Changes
- New `--iterations` cmd line option.  Now one can run inadyn with only
  one iteration.  Untested.  It was a debug option now made accessible
  via cmd line.  It should work.

### Fixes
- Custom DNS from dyndns option was not accepted by the cmd line parser.
  "Copy-paste" error :-(


1.60 - 2004-06-05
-----------------

### Changes
- On users' request the inadyn can read the options from file.


1.51 - 2004-05-03
-----------------

### Changes
- Support for more aliases for DNS service offered by freedns.afraid.org


1.5 - 2004-05-01
----------------

### Changes
- Support for dynamic DNS service offered by freedns.afraid.org
- Support for http proxy
- GPL copyright notice added.


1.4 - 2004-03-01
----------------

### Changes
- Support for custom DNS and static DNS services offered by dyndns.org
- Support for forced IP update, so the account will not expire even
  though the IP never changes


1.35 - 2004-02-04
-----------------

### Fixes
- Multiple aliases are AGAIN supported
- In case of error in IP update the OS signal handler is not installed again.


1.34 - 2003-11-06
-----------------

First port to *NIX - Linux running OK as console app.

### TODO
- Run as a background daemon in UNIX
- Better interface

### Fixes
- Various bug fixes.


1.2 - Jun 2003
--------------
Port to pSOS

**Note:** no DNS support under pSOS -- hard coded IP addresses of the
  server.


1.0 - 20013-05-20
-----------------

First stable version.

### Features
- DYNDNS client
- free
- works fine behind a NAT router
- runs fine as a service
- has a nice log file

### TODO
- port to *NIX
- port to pSOS


[UNRELEASED]: https://github.com/troglobit/inadyn/compare/1.99.14...HEAD
[1.99.14]: https://github.com/troglobit/inadyn/compare/1.99.13...1.99.14
[1.99.13]: https://github.com/troglobit/inadyn/compare/1.99.12...1.99.13
[1.99.12]: https://github.com/troglobit/inadyn/compare/1.99.11...1.99.12
[1.99.11]: https://github.com/troglobit/inadyn/compare/1.99.10...1.99.11
[1.99.10]: https://github.com/troglobit/inadyn/compare/1.99.9...1.99.10
[1.99.9]: https://github.com/troglobit/inadyn/compare/1.99.8...1.99.9
[1.99.8]: https://github.com/troglobit/inadyn/compare/1.99.7...1.99.8
[1.99.7]: https://github.com/troglobit/inadyn/compare/1.99.6...1.99.7
[1.99.6]: https://github.com/troglobit/inadyn/compare/1.99.5...1.99.6
[1.99.5]: https://github.com/troglobit/inadyn/compare/1.99.4...1.99.5
[1.99.4]: https://github.com/troglobit/inadyn/compare/1.99.3...1.99.4
[1.99.3]: https://github.com/troglobit/inadyn/compare/1.99.2...1.99.3
[1.99.1]: https://github.com/troglobit/inadyn/compare/1.99.1...1.99.2
[1.99.1]: https://github.com/troglobit/inadyn/compare/1.99.0...1.99.1
[1.99.0]: https://github.com/troglobit/inadyn/compare/1.98.1...1.99.0
[1.98.1]: https://github.com/troglobit/inadyn/compare/1.98.0...1.98.1
[1.98.0]: https://github.com/troglobit/inadyn/compare/1.97.4...1.98.0
[1.97.4]: https://github.com/troglobit/inadyn/compare/1.97.3...1.97.4
[1.97.3]: https://github.com/troglobit/inadyn/compare/1.97.2...1.97.3
[1.97.2]: https://github.com/troglobit/inadyn/compare/1.97.1...1.97.2
[1.97.1]: https://github.com/troglobit/inadyn/compare/1.97.0...1.97.1
[1.97.0]: https://github.com/troglobit/inadyn/compare/1.96.2...1.97.0
[libite]: https://github.com/troglobit/libite
[README.md]: https://github.com/troglobit/inadyn/blob/master/README.md

<!--
  -- Local Variables:
  -- mode: markdown
  -- End:
  -->