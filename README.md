Secretfiles Cookbook
==============

Cookbook for decrypting and storing decrypted content in file system.

Generic where data bag, secret file path, items and notification is set in attributes for a node. In the encrypted data bag a list of files can be specified with their respective path, content, owner, group and mode.

Usage
-----

Just include `secretfiles` in your node's `run_list`:

```json
{
  "name":"my_node",
  "default_attributes": {
    "secretfiles": {
      "non-important_unique_name": {
        "data_bag": "data_bag name",
        "items": ["item in data_bag"],
        "secret-file": "path for secret file on target",
        "notifies": ["restart", "subscriber", "delayed"]
      },
      "service-nginx-ssl": {
        "data_bag": "service-nginx",
        "items": ["ssl-certs"],
        "secret-file": "/etc/chef/secrets/service-nginx.pem",
        "notifies": ["restart", "service[nginx]"]
      }
    }
  },
  "run_list": [
    "recipe[secretfiles]"
  ]
}
```

Encrypted data bag example:

```json
{
  "id": "ssl-certs",
  "secretfiles": [
    {
      "path": "/etc/pki/nginx/cert.pem",
      "content": "Content base64 encoded",
      "owner": "nginx",
      "group": "nginx",
      "mode": "0660"
    },
    {
      "path": "/etc/pki/nginx/cert.crt",
      "content": "Content base64 encoded",
      "owner": "nginx",
      "group": "nginx",
      "mode": "0660"
    }
  ]
}
```

License and Authors
-------------------
Authors: Carl Loa Odin <carlodin@gmail.com>
