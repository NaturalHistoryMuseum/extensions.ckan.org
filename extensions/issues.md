---
layout: extension
name: issues
title: CKAN Issues Extension
author: Open Knowledge
homepage: https://github.com/okfn/ckanext-issues
github_user: okfn
github_repo: ckanext-issues
category: Extension
featured: 
permalink: /extension/issues/
---


# CKAN Issues Extension

This extension allows users to to report issues with datasets and resources in
a CKAN instance.

**Current Status:** Beta

## What it does

Once installed and enabled, the issues extension will make available a per
dataset issue tracker.

The issue tracker user interface can be found at:

    /dataset/{dataset-name-or-id}/issues

You can add an issue at:

    /dataset/{dataset-name-or-id}/issues/add

You can also add an issue about a specific resource

    /dataset/{dataset-name-or-id}/issues/add/{resource-id}

### Issues API

The issues extension also exposes its functionality as part of the standard [CKAN Action API][api]:

[api]: http://docs.ckan.org/en/latest/api/index.html

Specifically:

    /api/3/action/issue_show
    /api/3/action/issue_create

## Installation and Activation

To install the plugin, enter your virtualenv and install the source::

    pip install git+http://github.com/okfn/ckanext-issues

This will also register a plugin entry point, so you now should be
able to add the following to your CKAN .ini file::

    ckan.plugins = issues

After you clear your cache and reload the site, the Issues plugin
and should be available.

To configure notifications, you should set the following options in your
configuration.  Should notify_admin and notify_owner be set to False then no
emails will be sent about the newly created issue.

    ckanext.issues.notify_admin = True
    ckanext.issues.notify_owner = True
    ckanext.issues.from_address = test@localhost.local

## Feedback

Please open an issue in the github [issue tracker][issues].

[issues]: https://github.com/okfn/ckanext-issues

## Developers

Normal requirements for CKAN Extensions (including an installation of CKAN and
its dev requirements).

Testing:

    nosetests test/ --ckan --nologcapture


