# azerothcore_user

Create users via the AzerothCore SOAP API.

This role manages users (including gm status). Example config below:

```yaml
azerothcore_user_list:
  admin:
    enabled: true
    gmlevel: 1
    password: <vault_encrypt_string>

```

See the collection README for supported variables.

## License

GPL-3.0-only
