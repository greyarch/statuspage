# Statuspage

[![Updates](https://pyup.io/repos/github/jayfk/statuspage/shield.svg)](https://pyup.io/repos/github/jayfk/statuspage/)
[![Python 3](https://pyup.io/repos/github/jayfk/statuspage/python-3-shield.svg)](https://pyup.io/repos/github/jayfk/statuspage/)
[![Build Status](https://travis-ci.org/jayfk/statuspage.svg?branch=master)](https://travis-ci.org/jayfk/statuspage)
[![codecov.io](https://codecov.io/github/jayfk/statuspage/coverage.svg?branch=master)](https://codecov.io/github/jayfk/statuspage?branch=master)

A statuspage generator that lets you host your statuspage for free on GitHub. Uses
issues to display incidents and labels for severity.

## Demo

![DEMO](https://github.com/jayfk/statuspage/blob/master/demo.gif)

See a real status page generated by this at [status.pyup.io](http://status.pyup.io/) or a [demo site](https://jayfk.github.io/statuspage-demo/)

## Quickstart

Install statuspage with pip:

    pip install statuspage

*There are also binaries for macOS and Linux available, see [installation](docs/installation.md) for more.*

Now, create an GitHub API token:

- Go to your [Personal Access tokens](https://github.com/settings/tokens) page.
- Click on `Generate new token`.
- Make sure to check the `public_repo` and `write:repo_hook` scope.
- Copy the token somewhere safe, you won't be able to see it again once you leave the page.

To create a new status page, run:

    statuspage create --token=<yourtoken>

You'll be prompted for a repo name and the systems you want to show a status for.

    Name: mystatuspage
    Systems, eg (Website,API): Website, CDN, API

*Please note: This will generate a new repo under that name. Make sure it doesn't exist already.*

The command takes a couple of seconds to run. Once ready, it will output links to the issue tracker and your new status page.

    Create new issues at https://github.com/<login>/mystatuspage/issues
    Visit your new status page at https://<login>.github.com/mystatuspage/

The generator will then print the `statuspage update` command filled with all the details you need to update your page.

## Create an issue

To create a new issue, go to your newly created repo and click on `New Issue`.

- Click on the cog icon next to labels on the right.
- Choose the affected systems (black labels)
- Choose a severity label (major outage, degraded performance, investigating)
- Fill in the title, leave a comment and click on `Submit new issue`.

![Add New Issue](docs/new_issue.png)

Now, update your status page. Go back to your commandline and type:

    statuspage update --token=<yourtoken>
    Name: mystatuspage

If you change the issue (eg. when you add a new label, create a comment or close the issue), you'll
need to run `statuspage update` again.

## Adding and removing systems

In order to add or remove a system, run:

    statuspage add_system --token=<token> --name=<repo> --system=<system to add>
    statuspage remove_system --token=<token> --name=<repo> --system=<system to remove>

## Upgrading from previous versions

First, install the latest version with pip, or grab the latest [binary](docs/installation.md):

    pip install statuspage --upgrade

Updating your page to the latest version is now as simple as running:

    statuspage upgrade --token=<token> --name=<repo>

followed by an update:

    statuspage update --token=<token> --name=<repo>

## Translations
The generated status page is translated via JavaScript on the client side using [webL10n](https://github.com/fabi1cazenave/webL10n). It detects the visitors preferred language and translates all strings automatically.

Translations are available for the following languages:

- en
- de
- pt

Want to add a translation? Open `translations.ini` and add it. Pull requests welcome!

## Customizing
Want to change styles, the logo, or the footer? Check out [customizing](docs/customizing.md).

## Options

Want to create a status page for an organisation, or a private one? See [options](docs/options.md).
