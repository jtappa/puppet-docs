---
layout: default
title: "puppet-agent: What is it, and what's in it?"
---

[Facter]: {{facter}}/
[Hiera]: {{hiera}}/
[MCollective]: /mcollective/
[agent]: ./services_agent_unix.html
[apply]: ./services_apply.html
[Puppet Server]: {{puppetserver}}/
[release notes]: ./release_notes_agent.html

## Release contents of `puppet-agent` 1.x

See the table for details about which components shipped in which `puppet-agent` release, and the [package-specific release notes][release notes] for more information about packaging and installation fixes and features.

{% partial /puppet-agent/_agent1.x.html %}

>**Note:**
>
>* [Hiera 5](./hiera_intro.html) is a backwards-compatible evolution of Hiera, which is built into Puppet. To provide some backwards-compatible features, it uses the classic Hiera 3 codebase. This means "Hiera" is still shown as version 3.x in the table above, even though this Puppet version uses Hiera 5.
>
>* Puppet 4.9.1 does not appear on this table because it was a gem-only release and has not been packaged in `puppet-agent`.
>
>* Windows `puppet-agent` versions 1.4.2 through 1.5.2 shipped with Ruby 2.1.8.


## What `puppet-agent` and Puppet Server are

Starting with Puppet 4, we distribute Puppet as two core packages.

- `puppet-agent` --- This package contains Puppet's main code and all of the dependencies needed to run it, including [Facter][], [Hiera][], and bundled versions of Ruby and OpenSSL. It also includes [MCollective][]. Once it's installed, you have everything you need to run [the Puppet agent service][agent] and the [`puppet apply` command][apply].
- `puppetserver` --- This package depends on `puppet-agent`, and adds the JVM-based [Puppet Server][] application. Once it's installed, Puppet Server can serve catalogs to nodes running the Puppet agent service.

> **Note:** For information about Puppet agent in Puppet 3, see the [Puppet 3 services documentation](/puppet/3.8/services_commands.html#puppet-agent).

## How version numbers work

Puppet Server is a separate application that, among other things, runs instances of the Puppet master application. It has its own version number separate from the version of Puppet it runs, and can usually work with several nearby Puppet versions. For instance, agents running Puppet 4 work with masters running Puppet Server 2. (The Puppet Server package depends on a specific version of the Puppet Agent package, but can communicate with agents running older versions of Puppet. For instance, updating Puppet Server might update Puppet Agent on the master, but agents running previous versions of Puppet Agent will still work.)

The `puppet-agent` package also has its own version number, which doesn't match the version of Puppet it installs. For example, `puppet-agent` 1.3 includes Puppet 4.3.

Since the `puppet-agent` package distributes several different pieces of software, its version number will frequently increase when Puppet's version does not --- for example, `puppet-agent` 1.2.0 and 1.2.1 ship the same Puppet version but different Facter versions. Similarly, new versions of Puppet Server usually don't require updates to the core Puppet code.

Our options were to either let the versions be completely separate, or ship a bunch of "empty" Puppet releases where the version number increases without any changes to Puppet itself. For now, we're going with the former.
