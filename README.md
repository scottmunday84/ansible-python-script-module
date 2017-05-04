Ansible Local Python Script Module
--

I designed this module to run a Python script from within an Ansible tasklist, using the current context.

```yaml
- local_python_script: src="hello-world.py"
```

{{role_path}}/python_scripts/hello-world.py
```python
print "Hello world!"
```

You can also create new facts easily.

```yaml
- local_python_script: src="add-a-fact.py"
- debug: var="a_fact"
```

{{role_path}}/python_scripts/add-a-fact.py
```python
facts['a_fact'] = "this is a fact!"
```

You can also use facts available to the current context.

```yaml
- set_fact:
    a_fact: "this is a fact!"
- local_python_script: src="use-a-fact.py"
```

{{role_path}}/python_scripts/use-foo.py
```python
print a_fact
```
