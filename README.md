# ansible-role.apache

Install
========
```
git submodule add git@github.com:Waldz/ansible-role.apache.git roles/apache
git submodule add git@github.com:weareinteractive/ansible-openssl.git roles/openssl
```

Example
========
```
- name: Basic configuration to all servers
  hosts: all
  sudo: true
  roles:
    - role: openssl
    - role: apache
```

Variables
========
group_vars/all.yml
```
---

# Apache setup
apache:
  default_ssl_cert: "{{ openssl_certs_path }}/{{ fqdn }}.crt"
  default_ssl_key: "{{ openssl_keys_path }}/{{ fqdn }}.key"

# SSL certificates for Apache
openssl_certs_path: /etc/apache/ssl
openssl_keys_path: /etc/apache/ssl
openssl_self_signed:
  - {
    name: "{{ ansible_fqdn }}",
    domains: ["{{ fqdn }}", "*.{{ ansible_fqdn }}"],
    country: 'US',
    state: 'California',
    city: 'Los Angeles',
    organization: 'JSC Organization',
    unit: '',
    email: 'info@organization.com',
    days: 3650
  }
```
