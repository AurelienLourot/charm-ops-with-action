# Hello-world charm with an action

This [Juju charm](https://juju.is/docs) is an attempt to create a charm with an
action using the [Operator framework](https://github.com/canonical/operator).

## Without [charmcraft](https://github.com/canonical/charmcraft)

```
$ git submodule update --init --recursive
$ juju deploy .
$ juju run-action ops-with-action/0 hello --wait | grep status
  status: completed
```

## With [charmcraft](https://github.com/canonical/charmcraft)

```
$ git submodule update --init --recursive
$ virtualenv --python=python3 env
$ source env/bin/activate
(env)$ pip install charmcraft
(env)$ charmcraft build
(env)$ juju deploy ./charm-ops-with-action.charm
```

Fails with:

```
2020-06-16 09:57:36 ERROR juju-log Uncaught exception while in charm code:
Traceback (most recent call last):
  File "/var/lib/juju/agents/unit-ops-with-action-0/charm/hooks/install", line 38, in <module>
    main(CharmOpsWithAction)
  File "lib/ops/main.py", line 313, in main
    charm = charm_class(framework)
  File "/var/lib/juju/agents/unit-ops-with-action-0/charm/hooks/install", line 30, in __init__
    self.framework.observe(self.on.hello_action, self.on_hello_action)
AttributeError: 'CharmEvents' object has no attribute 'hello_action'
2020-06-16 09:57:36 ERROR juju.worker.uniter.operation runhook.go:132 hook "install" failed: exit status 1
```

This happens because
[charmcraft doesn't support actions yet](https://github.com/canonical/charmcraft/issues/35).
