# Mentos

*the freshmaker!*

Mentos is a gem refresh your browser automatically when files on disk changes.
I like having my editor on one side of the screen and my browser on the other,
and to have changes show up on the page I'm currently working on.

## Features

* Watch different directories and update specific sites by directory.
* Works on static and dynamic sites.
* One line install for Rack apps using Bundler (see below). Easy install otherwise.
* Pause/resume watching, configurable wait period before refreshes.
* Customizable actions other than page refresh.
* API for managing watched sites.

## Requirements

* mac - uses FSEvents api, might change in the future. TODO: how does autotest work?
* websocket capable browser

## Quick Install for Rack apps

If you're using a popular Rack web framework like Rails or Sinatra, it's as
simple as adding a line to your bundler's Gemfile:

    group :development do
      gem "mentos", :source => "gems.github.com"
    end

After running "bundle install", mentos will do the following the next time you
start your Rack app:

* check if mentos-server is running, start it if it isn't.
* add the current app as a site to monitor if it isn't already monitored.
* add mentos rack middleware to inject javascript to connect to mentos-server.

## Regular Installation

Mentos works with any vanilla site.  Here's an example for configuring a
static site:

    gem install mentos --source gems.github.com
    cd ~/Sites/mysite
    mentos add mysite
    mentos watch mysite

Next in your main layout, add the [mentos javascript]() to your html head:

    <head>
      <script type="text/javascript" src="mentos.js" />
      <script type="text/javascript" charset="utf-8">
        Mentos.watch('mysite');
      </script>
    </head>

## Configuration

For a list of commands and options, run:

    mentos help

TODO: API, config vars/paths

## Architecture

Mentos functionality is comprised of 2 parts:

* mentos-server: a sinatra websocket server that maintains a list of which
  sites are watched, and monitors directories specified by the configuration.
  It also includes a REST API for managing sites.

* mentos.js: javascript websocket client that connects to mentos-server to be
  notified when changes are received.

In addition to these, there are a few additional utilities:

* mentos-cli: the command line client for managing sites.
* mentos-rack: middleware to inject preconfigured mentos.js into Rack apps.

## Alternatives

* [XRefresh](http://xrefresh.binaryage.com/)
* [NodeJuice](http://nodejuice.com/)

## License

Copyright (c) 2010 Jerry Cheung

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.