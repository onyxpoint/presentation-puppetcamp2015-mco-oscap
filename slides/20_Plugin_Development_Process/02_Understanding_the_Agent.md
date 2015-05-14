## Writing the Agent: Capabilities

* Know what you need to run by hand **first**
* Remember: This part runs **on the server**

```bash
$ oscap xccdf eval --profile 'my-profile' --cpe cpe-dict.xml \
        --results /tmp/scan.xml os-xccdf.xml
```

* With SCAP, [Pry](http://pryrepl.org/) and [Nokigiri](http://www.nokogiri.org/) are your friends
    * Load the XML and dig for gold

<!-- .element: class="fragment" data-fragment-index="1" -->
