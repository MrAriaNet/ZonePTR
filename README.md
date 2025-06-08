# ZonePTR - Wildcard DNS for Any IP (like sslip.io)

ZonePTR is a self-hosted PowerDNS PipeBackend written in Python 3, designed to provide wildcard DNS resolution for any IPv4 address (e.g., `1-2-3-4.zoneptr.com` resolves to `1.2.3.4`).

## Features

- Wildcard A-records for IPs in domain names
- Configurable TTL, SOA, nameservers
- Optional whitelist/blacklist CIDR/IPs
- Easy environment-variable-based overrides
- Pure Python 3, no dependencies

## Example

```sh
dig 1-2-3-4.zoneptr.com
# Returns: 1.2.3.4
````

## Configuration

* Place the `pdns.local.pipe.conf` in `/etc/powerdns/pdns.d/`
* Place the `backend.py` and `backend.conf` inside `/etc/powerdns/zoneptr/`
* Make sure `backend.py` is executable: `chmod +x backend.py`

## PowerDNS Config

```ini
launch+=pipe

pipe-command=/etc/powerdns/zoneptr/backend.py
pipe-abi-version=5
```

## Environment Variables (optional)

| Variable              | Description                        |
| --------------------- | ---------------------------------- |
| `ZonePTR_DOMAIN`      | Main domain (default: zoneptr.com) |
| `ZonePTR_TTL`         | TTL value                          |
| `ZonePTR_SOA_ID`      | SOA serial                         |
| `ZonePTR_NAMESERVERS` | e.g., `ns1.zoneptr.com=1.2.3.4`    |
| `ZonePTR_WHITELIST`   | e.g., `allow1=10.0.0.0/8`          |
| `ZonePTR_BLACKLIST`   | e.g., `badguy=1.2.3.4`             |

## License

Apache License 2.0
