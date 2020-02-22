# Contributing

Thank you for considering contributing to WordOps.

We love to receive contributions. Maintaining a CLI tool for deploying WordPress with Nginx with a few key strokes require to have enough knowledge for each stack configuration and to work with non-interactive operations. We rely on community contributions and user feedback to continue providing the best CLI tool to deploy WordPress with Nginx, PHP-FPM, MariaDB and Redis.

There are many ways to contribute, with varying requirements of skills, explained in detail in the following sections.

## All WordOps Users

### Give WordOps a GitHub star

This is the minimum open-source users should contribute back to the projects they use. Github stars help the project gain visibility, stand out. So, if you use WordOps, consider pressing that button. **It really matters**.

### Spread the word

Community growth allows the project to attract new talent willing to contribute. This talent is then developing new features and improves the project. These new features and improvements attract more users and so on. It is a loop. So, post about WordOps, add a review or suggest it as an alternative to another app on [alternativeto.net](https://alternativeto.net/software/wordops/), present it to local meetups you attend, let your online social network or twitter, facebook, reddit, etc. know you are using it. **The more people involved, the faster the project evolves**.

### Provide feedback

Is there anything that bothers you about WordOps? Did you experience an issue while installing it or using it? Would you like to see it evolve to you need? Let us know. [Open a github issue](https://github.com/WordOps/WordOps/issues) to discuss it or open a thread on our [Community Forum](https://community.wordops.net/). Feedback is very important for open-source projects. We can't commit we will do everything, but your feedback influences our road-map significantly.

## Experienced Users

### Help other users

As the project grows, an increasing share of our time is spent on supporting this community of users in terms of answering questions, of helping users understand how WordOps works and find their way with it. Helping other users is crucial. It allows the developers and maintainers of the project to focus on improving it.

### Improve documentation

All of our documentation is in markdown (.md) files inside the WordOps GitHub project. All of our [HTML documentation](https://docs.wordops.net) is generated from these files. At the top right of each documentation page you will see a pencil, that leads you directly to the markdown file that was used to generated it. Don't be afraid to click it and edit any of these documents and submit a GitHub Pull Request with your corrections/additions.

## Developers

### Languages and Libraries

WordOps is built with the CLI Framework Cement, with the release v2.8.0 currently.

#### Python Version

WordOps source code is fully developed in python 3.x version.

#### Coding Format

We are following [PEP8](https://www.python.org/dev/peps/pep-0008/) style guide for coding WordOps.

#### Libraries

Here is the List of Libraries we used for WordOps

- [pystache](https://pypi.org/project/pystache/)
- [python-apt](http://apt.alioth.debian.org/python-apt-doc/library/index.html)
- [pynginxconfig](https://pypi.org/project/pynginxconfig/)
- [PyMySQL](https://pypi.org/project/PyMySQL/)
- [psutil](https://pypi.org/project/psutil/)
- [sh](https://amoffat.github.io/sh/)
- [SQLAlchemy](http://www.sqlalchemy.org/)
- [requests](https://pypi.org/project/requests/)
- [distro](https://pypi.org/project/distro/)

### Structure

WordOps application can be found in the `wo` directory of the github repository
Here the structure of WordOps with additional comments

```tree
wo
├── cli # the main directory of the application
│   ├── __init__.py
│   ├── bootstrap.py # Cement framework
│   ├── controllers # Cement framework
│   ├── ext # Cement framework
│   ├── main.py # Cement framework
│   ├── plugins # WordOps commands (stack, site, update .. etc)
│   └── templates # WordOps configuration template
├── core # main functions used in WordOps plugins
└── utils # testing helper

```

Plugins Directory:
Here the list of plugins with the related command or a short description

```tree
├── plugins
│   ├── __init__.py
│   ├── clean.py # wo clean
│   ├── debug.py # wo debug
│   ├── import_slow_log.py # wo import-slow-log (from EE v3)
│   ├── info.py # wo info
│   ├── log.py # wo log
│   ├── maintenance.py # wo maintenance
│   ├── models.py # site information structure for WO internal DB
│   ├── secure.py # wo secure
│   ├── site.py # wo site
│   ├── site_functions.py # functions used by site.py
│   ├── sitedb.py # WO internal SQlite3 database functions
│   ├── stack.py # wo stack install/remove/purge
│   ├── stack_migrate.py # wo stack migrate
│   ├── stack_pref.py # stack configuration used by stack.py & stack_upgrade.py
│   ├── stack_services.py # wo stack start/stop/restart/reload
│   ├── stack_upgrade.py # wo stack upgrade
│   ├── sync.py # wo sync
│   └── update.py # wo update
```

### Development Environnment

### Contributions Ground Rules

#### Code of Conduct and CLA

We expect all contributors to abide by the [Contributor Covenant Code of Conduct](/about/code-of-conduct.md).
