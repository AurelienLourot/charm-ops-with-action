# Hello-world charm with an action

This [Juju charm](https://juju.is/docs) is an attempt to create a charm with an
action using the [Operator framework](https://github.com/canonical/operator).

```
$ git submodule update --init --recursive
$ juju deploy .
$ juju run-action ops-with-action/0 hello --wait | grep status
  status: completed
```
