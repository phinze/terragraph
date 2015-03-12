# terragraph

a wee utility for converting terraform textual graph notation into graphviz dot

## example

Given input file `input.tfgraph` with contents:

```
aws_eip.foo_eip
  aws_instance.foo_instance
aws_eip.foo_eip (destroy tainted)
  aws_internet_gateway.gw (destroy tainted)
aws_eip.foo_eip (destroy)
  provider.aws
aws_instance.foo_instance
  aws_security_group.tf_test_foo
  aws_subnet.foo
aws_instance.foo_instance (destroy tainted)
  aws_eip.foo_eip (destroy tainted)
aws_instance.foo_instance (destroy)
  aws_eip.foo_eip (destroy)
aws_internet_gateway.gw
  aws_eip.foo_eip
aws_internet_gateway.gw (destroy tainted)
  provider.aws
aws_security_group.tf_test_foo
  aws_vpc.foo
aws_security_group.tf_test_foo (destroy tainted)
  aws_instance.foo_instance (destroy tainted)
aws_security_group.tf_test_foo (destroy)
  aws_instance.foo_instance (destroy)
aws_subnet.foo
  aws_vpc.foo
aws_subnet.foo (destroy tainted)
  aws_instance.foo_instance (destroy tainted)
aws_subnet.foo (destroy)
  aws_instance.foo_instance (destroy)
aws_vpc.foo
  aws_vpc.foo (destroy tainted)
  aws_vpc.foo (destroy)
aws_vpc.foo (destroy tainted)
  aws_security_group.tf_test_foo (destroy tainted)
  aws_subnet.foo (destroy tainted)
aws_vpc.foo (destroy)
  aws_security_group.tf_test_foo (destroy)
  aws_subnet.foo (destroy)
provider.aws
```

Run:

```
./terragraph input.tfgraph | dot -Tpng > output.png
```

See:

![](https://raw.github.com/phinze/terragraph/master/output.png)
