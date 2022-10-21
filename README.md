# vue-dns-form-generator
A simple Vue form to manage DNS (Domain Name System) records by adding and removing form row as needed.

## DNS Record Types
- A (IP4 Address) - Maps the domain name to its IP address
- AAAA (IP6 Address) - Maps the domain name to the IPv6 address.
- CNAME (Alias) - Canonical Name. This allows you to create an alias for your domain.
- MX (Mail) - Mail Exchange - MX records determine how mail is delivered to your domain
- SPF (TXT) - Text Record. It allows you to attach comments to a hostname
- SRV (Service) - Service record.

## Form Fields
- Name - A subdomain input field
- Type - Dropdown field to select record type
- Value - Input field to enter record type related IP or Hostname or Text.
- Priority - Input field to give priority for MX record type.
- TTL - Time To Live input field to enter time to propagate the record.

## Component Usage
```
<DNSRecordForm :data=""></DNSRecordForm>
```
## Project setup
```
npm install vue-dns-form-generator
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
