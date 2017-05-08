Ansible Python Script Module
============================

I designed this module to run a Python script from within an Ansible tasklist. Python is a
powerful language, and because it is the programming language used by Ansible, we can share context between Ansible and
scripts written for this module, allowing you to quickly boilerplate code that just will work with Ansible.

Getting Started
---------------

To get started, copy the folders for action_plugins and library into your playbook directory.

Afterward, you should be all set!


Examples
--------

Like most introductions, let's write a "hello world" script.

```yaml
- python_script: src="hello-world.py"
```

{{role_path}}/python_scripts/hello-world.py
```python
print "Hello world!"
```

You can also create new facts in your scripts.

```yaml
- python_script: src="add-a-fact.py"
- debug: var="a_fact"
```

{{role_path}}/python_scripts/add-a-fact.py
```python
facts['a_fact'] = "this is a fact!"
```

We can easiy pass facts to our scripts as well. If it is defined within the Ansible context, it'll be available from
your script!

```yaml
- set_fact:
    a_fact: "this is a fact!"
- python_script: src="use-a-fact.py"
```

{{role_path}}/python_scripts/use-foo.py
```python
print a_fact
```

Although these previous examples are simple, the entire power of Python is at your fingertips. For example, here's a
script I wrote to connect to a MySQL server.

```yaml
- python_script: src="connect-to-mysql.py"
```

{{role_path}}/python_scripts/connect-to-mysql.py
```python
import MySQLdb

db = MySQLdb.connect(host="localhost",
                     user="user",
                     passwd="password",
                     db="db")
```
