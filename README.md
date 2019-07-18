![Logo](https://raw.githubusercontent.com/idealista/cerebro_role/master/logo.gif)

[![Build Status](https://travis-ci.org/idealista/cerebro_role.png)](https://travis-ci.org/idealista/cerebro_role)

# Cerebro Ansible role

- [Getting Started](#getting-started)
  - [Prerequisities](#prerequisities)
  - [Installing](#installing)
- [Usage](#usage)
- [Testing](#testing)
- [Built With](#built-with)
- [Versioning](#versioning)
- [Authors](#authors)
- [License](#license)
- [Contributing](#contributing)

## Getting Started

Ansible role for Cerebro Elasticsearch web admin tool. Currently this works on Debian based linux systems. Tested platforms are:

* Debian 8
* Debian 9

These instructions will get you a copy of the role for your ansible playbook. Once launched, it will install [Cerebro](https://github.com/lmenezes/cerebro).
### Prerequisities

#### To execute this role:

Ansible 2.7.9.0 version installed.

#### For testing purposes:

* Python 3.6
* [Molecule](https://molecule.readthedocs.io/)
* [Pipenv](https://github.com/pypa/pipenv) 
* [jmespath](http://jmespath.org/) 
* [Docker](https://www.docker.com/) as driver


### Installing

Create or add to your roles dependency file (e.g requirements.yml):

```yml
- src: http://github.com/idealista/cerebro_role.git
  scm: git
  version: 1.0.0
  name: cerebro
```

Install the role with ansible-galaxy command:

```sh
ansible-galaxy install -p roles -r requirements.yml -f
```

Use in a playbook:

```yml
---
- hosts: someserver
  roles:
    - role: cerebro
```

## Usage

Look to the [defaults](defaults/main.yml) properties file to see the possible configuration properties.

### Role Variables

#### Cerebro installation configuration

```
cerebro_version: 0.8.3
cerebro_force_reinstall: false
cerebro_home_dir: /opt/cerebro
cerebro_group: cerebro
cerebro_user: cerebro
cerebro_user_home_dir: /home/{{ cerebro_user }}
cerebro_host: "0.0.0.0"
cerebro_port: 9000
cerebro_service_enabled: true
cerebro_service_state: started
```

#### Cerebro app configuration

```
cerebro_conf_dir: "{{ cerebro_home_dir }}/conf"
cerebro_data_dir: /var/lib/cerebro
cerebro_pid_dir: /var/run/cerebro
cerebro_play_secret: ki:s:[[@=Ag?QI`W2jMwkY:eqvrJ]JqoJyi2axj3ZvOv^/KavOT4ViJSv?6YY4[N
cerebro_rest_history: 50

cerebro_es_hosts:
  - name: cluster
    host: localhost:9200
```

#### Configuration for LDAP

```
cerebro_ldap_auth:
  url: ldap://host:port
  base_dn: ou=active,ou=Employee
  method: simple
  user_domain: domain.com
  user_auth:
    username: admin
    password: 1234
```

### Example Playbook

```
---
- hosts: all
  roles:
    - role: cerebro
  vars:
    cerebro_play_secret: ki:s:[[@=Ag?QI`W2jfdsfwkY:eqvrJ]JqoJyi2DCj3Zv0v^/KavOT4ViJdsafY4[N
    cerebro_rest_history: 200

    cerebro_es_hosts:
      - name: pro-cluster
        host: es-pro:9200
        es_auth:
          username: ES_user
          password: ES_user_password
      - name: qa-cluster
        host: es-qa:9200
```

## Testing

```sh
pipenv install -r test-requirements.txt
pipenv run molecule test
```

Cerebro Admin UI should be accessible from docker container host at URL:

http://localhost:9000

## Built With

![Ansible](https://img.shields.io/badge/ansible-2.7.9.0-green.svg)

## Versioning

For the versions available, see the [tags on this repository](https://github.com/idealista/cerebro_role/tags).

Additionaly you can see what change in each version in the [CHANGELOG.md](CHANGELOG.md) file.

## Authors

- **Idealista** - *Work with* - [idealista](https://github.com/idealista)

See also the list of [contributors](https://github.com/idealista/cerebro_role/contributors) who participated in this project.

## License

![Apache 2.0 License](https://img.shields.io/hexpm/l/plug.svg)

This project is licensed under the [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) license - see the [LICENSE](LICENSE) file for details.

## Contributing

Please read [CONTRIBUTING.md](.github/CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.