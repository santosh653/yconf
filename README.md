# YAML configuration processor

You can find usage example in ejabberd. See `econf.erl` and `ejabberd_options.erl` for most parts that are using it.

Validation is performed based on rules that you pass to `yconf:parser/2`, there is no way to load those rules from
some special syntax file. Generally you will do something like this:

```
yconf:parse("/home/me/conf.yml", #{
  host => yconf:string(),
  opts => yconf:options(#{
    addr => yconf:ip(),
    count => yconf:non_neg_int()
  }
)}).
```

That when feed with:

```
host: "test.com"
opts:
  addr: "127.0.0.1"
  count: 100
```

should produce:

```
{ok,[{host,"test.com"},{opts,[{addr,{127,0,0,1}},{count,100}]}]}
```
