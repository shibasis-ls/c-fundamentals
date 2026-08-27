# showip

A minimal C command-line utility that resolves a hostname to its IP address(es) using `getaddrinfo()`.

## Usage

```bash
./showip hostname
```

**Example:**

```bash
$ ./showip example.com
IP addresses for example.com:

 IPv4: 93.184.216.34
 ipv6: 2606:2800:220:1:248:1893:25c8:1946
```

## Build

```bash
gcc -o showip showip.c
```

## How It Works

- Populates a `struct addrinfo` hints struct with `AF_UNSPEC` (allow IPv4/IPv6) and `SOCK_STREAM`.
- Calls `getaddrinfo()` to resolve the hostname into a linked list of `addrinfo` results.
- Iterates the list, extracting the raw address (`sockaddr_in` or `sockaddr_in6`) based on `ai_family`.
- Converts each address to a human-readable string with `inet_ntop()`.
- Frees the result list with `freeaddrinfo()`.

## Requirements

- POSIX-compliant system (Linux/macOS/BSD)
- GCC or any standard C compiler
