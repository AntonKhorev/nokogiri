# Nokogiri

## Description

Nokogiri (鋸) is an HTML, XML, SAX, and Reader parser.  Among
Nokogiri's many features is the ability to search documents via XPath
or CSS3 selectors.

## Links

* http://nokogiri.org
* [Installation Help](http://nokogiri.org/tutorials/installing_nokogiri.html)
* [Tutorials](http://nokogiri.org)
* [GitHub](https://github.com/sparklemotion/nokogiri)
* [Mailing List](https://groups.google.com/group/nokogiri-talk)
* [Bug Reports](https://github.com/sparklemotion/nokogiri/issues)
* [Chat/Gitter](https://gitter.im/sparklemotion/nokogiri)

[![Concourse CI](https://ci.nokogiri.org/api/v1/teams/nokogiri-core/pipelines/nokogiri/jobs/ruby-2.4-system/badge)](https://ci.nokogiri.org/teams/nokogiri-core/pipelines/nokogiri?groups=master)
[![Code Climate](https://codeclimate.com/github/sparklemotion/nokogiri.svg)](https://codeclimate.com/github/sparklemotion/nokogiri)
[![Join the chat at https://gitter.im/sparklemotion/nokogiri](https://badges.gitter.im/sparklemotion/nokogiri.svg)](https://gitter.im/sparklemotion/nokogiri?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


## Features

* XML/HTML DOM parser which handles broken HTML
* XML/HTML SAX parser
* XML/HTML Push parser
* XPath 1.0 support for document searching
* CSS3 selector support for document searching
* XML/HTML builder
* XSLT transformer

Nokogiri parses and searches XML/HTML using native libraries (either C
or Java, depending on your Ruby), which means it's fast and
standards-compliant.


## Installation

If this doesn't work:

```
gem install nokogiri
```

then please start troubleshooting here:

> http://www.nokogiri.org/tutorials/installing_nokogiri.html

There are currently 1,237 Stack Overflow questions about Nokogiri
installation. The vast majority of them are out of date and therefore
incorrect. __Please do not use Stack Overflow.__

Instead, [tell us](http://nokogiri.org/tutorials/getting_help.html)
when the above instructions don't work for you. This allows us to both
help you directly and improve the documentation.


### Binary packages

Binary packages are available for some distributions.

* Debian: https://packages.debian.org/sid/ruby-nokogiri
* SuSE: https://download.opensuse.org/repositories/devel:/languages:/ruby:/extensions/
* Fedora: http://s390.koji.fedoraproject.org/koji/packageinfo?packageID=6756


## Support

There are open-source tutorials (to which we invite contributions!) here: http://nokogiri.org/tutorials

* The Nokogiri mailing list is active: https://groups.google.com/group/nokogiri-talk
* The Nokogiri bug tracker is here: https://github.com/sparklemotion/nokogiri/issues
* Before filing a bug report, please read our submission guidelines: http://nokogiri.org/tutorials/getting_help.html
* The IRC channel is #nokogiri on freenode.


## Security and Vulnerability Reporting

Please report vulnerabilities at https://hackerone.com/nokogiri

Full information and description of our security policy is in [`SECURITY.md`](SECURITY.md)


## Synopsis

Nokogiri is a large library, but here is example usage for parsing and examining a document:

```ruby
#! /usr/bin/env ruby

require 'nokogiri'
require 'open-uri'

# Fetch and parse HTML document
doc = Nokogiri::HTML(open('http://www.nokogiri.org/tutorials/installing_nokogiri.html'))

puts "### Search for nodes by css"
doc.css('nav ul.menu li a', 'article h2').each do |link|
  puts link.content
end

puts "### Search for nodes by xpath"
doc.xpath('//nav//ul//li/a', '//article//h2').each do |link|
  puts link.content
end

puts "### Or mix and match."
doc.search('nav ul.menu li a', '//article//h2').each do |link|
  puts link.content
end
```


## Requirements

* Ruby 2.3.0 or higher, including any development packages necessary
  to compile native extensions.

* In Nokogiri 1.6.0 and later libxml2 and libxslt are bundled with the
  gem, but if you want to use the system versions:

  * First, check out [the long list](http://www.xmlsoft.org/news.html)
    of fixes and changes between releases before deciding to use any
    version older than is bundled with Nokogiri.

  * At install time, set the environment variable
    `NOKOGIRI_USE_SYSTEM_LIBRARIES` or else use the
    `--use-system-libraries` argument. (See
    http://nokogiri.org/tutorials/installing_nokogiri.html#using_your_system_libraries
    for specifics.)

  * libxml2 >=2.6.21 with iconv support
    (libxml2-dev/-devel is also required)

  * libxslt, built with and supported by the given libxml2
    (libxslt-dev/-devel is also required)


## Encoding

Strings are always stored as UTF-8 internally.  Methods that return
text values will always return UTF-8 encoded strings.  Methods that
return a string containing markup (like `to_xml`, `to_html` and
`inner_html`) will return a string encoded like the source document.

__WARNING__

Some documents declare one encoding, but actually use a different
one. In these cases, which encoding should the parser choose?

Data is just a stream of bytes. Humans add meaning to that stream. Any
particular set of bytes could be valid characters in multiple
encodings, so detecting encoding with 100% accuracy is not
possible. `libxml2` does its best, but it can't be right all the time.

If you want Nokogiri to handle the document encoding properly, your
best bet is to explicitly set the encoding.  Here is an example of
explicitly setting the encoding to EUC-JP on the parser:

```ruby
  doc = Nokogiri.XML('<foo><bar /></foo>', nil, 'EUC-JP')
```

## Development

```bash
  bundle install
  bundle exec rake
```

## License

This project is licensed under the terms of the MIT license.

See this license at [`LICENSE.md`](LICENSE.md).
