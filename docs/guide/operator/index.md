**MOF** backend is written in golang with [rk-boot](https://github.com/rookie-ninja/rk-boot) framework. All the configuration changes can be done in rk-boot way.

## boot.yaml
**MOF** backend server is configured to bootstrap with a config file named boot.yaml. It is a rk-boot style config file can be used to override bootstrapping values.

There two ways to override the boot.yaml file.

- Environment variable
- Flags

### Rules: ENV
Prefix of "RK" will be used as environment variable key. The schema follows above.

**example-boot.yaml:**

```yaml
gin:
   - port: 1949
     commonService:    
       enabled: true
```

We can override values in example-boot.yaml file as bellow:

```go
os.Setenv("RK_GIN_0_PORT", "2008")
os.Setenv("RK_GIN_0_COMMONSERVICE_ENABLED", "false")
```

### Rules: Flags
**example-boot.yaml:**

```yaml
gin:
  - port: 1949
    commonService:
      enabled: true
```
   
We can override values in example-boot.yaml file as bellow:

```bash
./your_compiled_binary --rkset "gin[0].port=2008,gin[0].commonService.enabled=false"
```

**Basic rules:**

- Using comma(,) to separate different k/v section.
- Using [index] to access arrays in YAML file.
- Using equal sign(=) to distinguish key and value.
- Using dot(.) to access map in YAML file.

## Change Database
**MOF** can be configured to use bellow databases. 

| Database   | Suggested Version |
|------------|-------------------|
| MySQL      | >5.6              |
| PostgreSQL | >8.4              |
| SQL Server | >8.4              |
| SQLite     | >15.0             |

Changing database types is not required to do code changes. 

### Environment variables
Here is full database configuration yaml format. Change values with rules mentioned above.

```yaml
mysql:
  - name: mof
    enabled: true
    domain: "*"
    user: root
    pass: pass
    addr: "host.docker.internal:3306"
    database:
      - name: user
        autoCreate: true
      - name: offer
        autoCreate: true
      - name: prov
        autoCreate: true
```

Example: Change address

```bash
export RK_MYSQL_0_ADDR="your-remote-addr:3306"
```

### Flags
Example: Change address

```bash
./mof --rkset "mysql[0].addr=your-remote-addr:3306"
```

## Change exchange rate
Exchange rate is currently configured as static value. Overriding this value can be done as the same way mentioned above.

```yaml
exchange:
  name: exchange
  enabled: true
  baseUnit: USD
  static:
    enabled: true
    currency:
      CNY: 6.66
```

Or, a remote exchange rate server can be configured. Please refer to [rk-ex](https://github.com/rookie-ninja/rk-repo/tree/master/exchange)

## Change crypto token
Crypto token is used to encrypt user password stored in database. User can override it as bellow.

```bash
export RK_CONFIG_0_CONTENT_CRYPTOTOKEN="your-new-token"
```

Here is the full config currently used by **MOF**

```yaml
config:
  - name: mof
    content:
      offerRefreshIntervalHours: 720
      redirectURL: "http://localhost:8080/v2/auth"
#      cryptoToken: "rk-crypto-key-xx"
```

## JWT signing method
TODO