# Python 3 error

Error while installing mkdocs "error: externally-managed-environment

```
pip install mkdocs
```
Run

```
python3 -m pip config set global.break-system-packages true
```

Run the pip install again and it will be installed.

# Azure client

When running the command az login you can get an error on azure-mgmt-rdbms. The command ``python3 -m pip config set global.break-system-packages true`` shoukd have been run.

```
pip install --force-reinstall -v "azure-mgmt-rdbms==10.2.0b17"
```

After that the az login should not give any errors anymore.
