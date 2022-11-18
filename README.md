Ansible Role: zammad
=====================

An Ansible role that installs [zammad](https://zammad.org) and configures it. It is basically written for RHEL/CentOS but can be ported to other distributions.

Table of Contents
-----------------

<!-- toc -->

- [Description](#description)
- [Requirements](#requirements)
- [Role Variables](#role-variables)
  * [Basic Variables](#basic-variables)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Top-Level Playbook](#top-level-playbook)
  * [Role Dependency](#role-dependency)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->

Description
-----------

This Role will install nginx, elasticsearch java and zammad and deploy it's config based on jinja2 templates. It relates on having a custom ssl cert for https traffic. Elasticsearch component don't work yet.

Requirements
------------

- Ansible 2+
- SSL Certificates for nginx server (mandatory)

Role Variables
--------------

### Basic Variables

Variables you have to set:

```yml
zammad_ssl_cert_key: 'my_zammad_key.pem'
zammad_ssl_cert: 'my_zammad_cert.pem'
zammad_ssl_dir: '/my/path/to/zammad-certdir'

```

Dependencies
------------

None.

Example Playbook
----------------

Add to `requirements.yml`:

```yml
---

- src: DirectorSloan.zammad

...
```

Download:

```console
$ ansible-galaxy install -r requirements.yml
```

### Top-Level Playbook

Write a top-level playbook:

```yml
---

- name: worker server
  hosts: worker

  roles:
    - role: DirectorSloan.zammad
      tags:
        - zammad

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: sloan87.zammad
    tags:
      - zammad

...
```

License
-------

MIT

Author Information
------------------

This role was created in 2018 by Ben Langenberg [DirectorSloan at GitHub][DirectorSloan], HPC cluster systems administrator at the [Helmholtz-Centre for Environmental Research GmbH - UFZ][ufz], role skel based on a draft by Christian Krause aka [wookietreiber at GitHub][wookietreiber].


[ufz]: https://www.ufz.de
[DirectorSloan]: https://github.com/DirectorSloan
[wookietreiber]: https://github.com/wookietreiber
[zammad]: http://www.zammad.org
