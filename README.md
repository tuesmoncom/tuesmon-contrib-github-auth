Tuesmon contrib github auth
=========================

[![Kaleidos Project](http://kaleidos.net/static/img/badge.png)](https://github.com/kaleidos "Kaleidos Project")
[![Managed with Tuesmon.com](https://img.shields.io/badge/managed%20with-TUESMON.io-709f14.svg)](https://manage.tuesmon.com/project/tuesmon/ "Managed with Tuesmon.com")

The Tuesmon plugin for github authentication.

Installation
------------
### Production env

#### Tuesmon Back

In your Tuesmon back python virtualenv install the pip package `tuesmon-contrib-github-auth` with:

```bash
  pip install tuesmon-contrib-github-auth
```

Modify your `settings/local.py` and include the line:

```python
  INSTALLED_APPS += ["tuesmon_contrib_github_auth"]

  # Get these from https://github.com/settings/developers
  GITHUB_API_CLIENT_ID = "YOUR-GITHUB-CLIENT-ID"
  GITHUB_API_CLIENT_SECRET = "YOUR-GITHUB-CLIENT-SECRET"
```

#### Tuesmon Front

Download in your `dist/plugins/` directory of Tuesmon front the `tuesmon-contrib-github-auth` compiled code (you need subversion in your system):

```bash
  cd dist/
  mkdir -p plugins
  cd plugins
  svn export "https://github.com/tuesmoncom/tuesmon-contrib-github-auth/tags/$(pip show tuesmon-contrib-github-auth | awk '/^Version: /{print $2}')/front/dist"  "github-auth"
```

Include in your `dist/conf.json` in the 'contribPlugins' list the value `"/plugins/github-auth/github-auth.json"`:

```json
...
    "gitHubClientId": "YOUR-GITHUB-CLIENT-ID",
    "contribPlugins": [
        (...)
        "/plugins/github-auth/github-auth.json"
    ]
...
```

### Dev env

#### Tuesmon Back

Clone the repo and

```bash
  cd tuesmon-contrib-github-auth/back
  workon tuesmon
  pip install -e .
```

Modify `tuesmon-back/settings/local.py` and include the line:

```python
  INSTALLED_APPS += ["tuesmon_contrib_github_auth"]

  # Get these from https://github.com/settings/developers
  GITHUB_API_CLIENT_ID = "YOUR-GITHUB-CLIENT-ID"
  GITHUB_API_CLIENT_SECRET = "YOUR-GITHUB-CLIENT-SECRET"
```

#### Tuesmon Front

After clone the repo link `dist` in `tuesmon-front` plugins directory:

```bash
  cd tuesmon-front/dist
  mkdir -p plugins
  cd plugins
  ln -s ../../../tuesmon-contrib-github-auth/dist github-auth
```

Include in your `dist/conf.json` in the 'contribPlugins' list the value `"/plugins/github-auth/github-auth.json"`:

```json
...
    "gitHubClientId": "YOUR-GITHUB-CLIENT-ID",
    "contribPlugins": [
        (...)
        "/plugins/github-auth/github-auth.json"
    ]
...
```

In the plugin source dir `tuesmon-contrib-github-auth/front` run

```bash
npm install
```
and use:

- `gulp` to regenerate the source and watch for changes.
- `gulp build` to only regenerate the source.

Running tests
-------------

We only have backend tests, you have to add your `tuesmon-back` directory to the
PYTHONPATH environment variable, and run py.test, for example:

```bash
  cd back
  add2virtualenv /home/tuesmon/tuesmon-back/
  py.test
```

