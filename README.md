hiera_param
===========

Assigns parameters to a node using an hash merge lookup that retrieves the
values for a user-specified key from a Hiera data source.

To use `hiera_param`, the following configuration is required:

- A key name to use for parameters, e.g. `params`.
- A line in the puppet `sites.pp` file (e.g. `/etc/puppet/manifests/sites.pp`)
  reading `hiera_param('params')`. Note that this line must be outside any node
  definition and below any top-scope variables in use for Hiera lookups.
- Class keys in the appropriate data sources. In a data source keyed to a node's role,
  one might have:

```yaml
---
params:
  dc: 'NYC'
  cluster: 'web'
````

In addition to the required `key` argument, `hiera_param` accepts two additional
arguments:
- a `default` argument in the second position, providing an hash to be returned
  in the absence of matches to the `key` argument
- an `override` argument in the third position, providing a data source to consult
  for matching values, even if it would not ordinarily be part of the matched hierarchy.
  If Hiera doesn't find a matching key in the named override data source, it will continue
  to search through the rest of the hierarchy.