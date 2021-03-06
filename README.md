hostlist_expression
===================

[![Gem Version](https://badge.fury.io/rb/hostlist_expression.svg)](http://badge.fury.io/rb/hostlist_expression) [![Gem Version](https://travis-ci.org/udondan/hostlist_expression-ruby.svg)](https://travis-ci.org/udondan/hostlist_expression-ruby)


Ruby [gem](https://rubygems.org/gems/hostlist_expression) for expanding hostlist expressions.

An expression like `host-[1-3].com` will expand into an array containing these elements:
```
host-1.com
host-2.com
host-3.com
```

This gem supports **numeric** and **alphabetic** **ranges** and **sequences**, and any combination.

By default both characters `:` ([Ansible](http://docs.ansible.com/intro_inventory.html#hosts-and-groups) style) and `-` ([pdsh](https://code.google.com/p/pdsh/wiki/HostListExpressions) style) are interpreted as range connectors.

Numeric ranges can have leading zeros `[01-99]`.

With commata you can define sequences: `[1,3,5]`.

A complex example with all variations:

Expression: `host-[A-C]-[c,d,001-003].com`

Result:
```
host-A-c.com
host-A-d.com
host-A-001.com
host-A-002.com
host-A-003.com
host-B-c.com
host-B-d.com
host-B-001.com
host-B-002.com
host-B-003.com
host-C-c.com
host-C-d.com
host-C-001.com
host-C-002.com
host-C-003.com
```

Please note, in an alphabetic range both items are required to be either lowercase or uppercase, you can't mix. A range like `[A-c]` will throw an exception.

#Usage:
```rb
require "hostlist_expression"
hosts = hostlist_expression("host-[1-3].com")
print hosts

# => ["host-1.com", "host-2.com", "host-3.com"]
```

You may optionally pass custom characters for range definitions as 2nd parameter. (String or Array)

```rb
hosts = hostlist_expression("host-[1~3].com", "~")
hosts = hostlist_expression("host-[1~3,A-C,x/z].com", ["~", "-", "/"])
```

#License
MIT
