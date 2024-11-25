# Installation
Download the script from the master branch and make it executable:
```
curl -LJO https://raw.githubusercontent.com/
chmod +x ./ttfb
```

# Usage

```
Usage: ttfb [options] url [url...]
	-d debug
	-l <log file> (infers -d) log response headers. Defaults to ./curl.log
	-n <number> of times to test time to first byte
	-o <option> pass options to curl (e.g. -o "-k" will make curl ignore invalid certificates)
	-v verbose output. Show response breakdown (DNS lookup, TLS handshake etc)
```

## Examples

Basic usage:

```
$ ttfb example.com
.227436
```

Basic usage with verbose response breakdown:

```
$ ttfb -v https://example.com
DNS lookup: 0.005152 TLS handshake: 0.000000 TTFB including connection: 0.200831 TTFB: .200831 Total time: 0.201132
```

Test multiple times:

```
$ ttfb -n 5 https://example.com
.....
fastest .177263 slowest .214302 median .179957
```

Test multiple URLs:

```
$ ttfb https://example1.com https://example2.com
example1.com       .049985
example2.com       .054122
```

Test multiple URLs, multiple times:

```
$ ttfb -n 5 https://example1.com https://example2.com
.....
.....
example1.com       fastest .030936 slowest .057755 median .034663
example2.com       fastest .031413 slowest .182791 median .035001
```

Verbose response breakdown when multiple tests specified:

```
$ ttfb -v -n 5 https://example.com
DNS lookup: 0.005335 TLS handshake: 0.102314 TTFB including connection: 0.148328 TTFB: .046014 Total time: 0.646115
DNS lookup: 0.005322 TLS handshake: 0.102609 TTFB including connection: 0.150693 TTFB: .048084 Total time: 0.644611
DNS lookup: 0.004277 TLS handshake: 0.102066 TTFB including connection: 0.172199 TTFB: .070133 Total time: 1.196256
DNS lookup: 0.004444 TLS handshake: 0.107375 TTFB including connection: 0.160771 TTFB: .053396 Total time: 0.637290
DNS lookup: 0.005352 TLS handshake: 0.118882 TTFB including connection: 0.168772 TTFB: .049890 Total time: 0.653761

fastest .046014 slowest .070133 median .049890
```