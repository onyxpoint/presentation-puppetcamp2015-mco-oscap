# Presentations

This is a template for various public Onyx Point, Inc. presentations.

Each presentation may have its own License file so please check the details of
each prior to reuse.

These are meant to be mixed into the Onyx Point fork of reveal.js at
https://github.com/onyxpoint/reveal.js.

For details on Reveal.js, please see http://lab.hakim.se/reveal-js

## Installation

Run **bundle install** to install the requisite rubygems for building the
presentation.

As you work, you may want to have Guard running to automatically rebuild the
presentation when you save your slides. You can do this using the following
command.


```shell
$ while bundle exec guard; do echo "Restarting Guard..."; done
```

## Usage

The file build/index.html will display your final presentation.

For best results, ensure that your browser is not caching between refreshes.

## Slide Organization

To organize your slides, you can use a human numbering scheme under the
*slides* directory.

I highly recommend leaving some space between your slide numbers so that you
can easily insert items later on.

You must **always** use Markdown in your slide decks.

### Vertical Stacks

Vertical stacks can be made by creating a subdirectory with the same name as
the top level slide.

For instance, if you want a vertical stack under '05_Neat_Stuff', you would
create a directory called '05_Neat_Stuff' and start adding and numbering slides
under that directory.

### Other Persistent Changes

If you want additional persistent changes, you'll need to modify
*index.html.erb* to suit your needs.

