# Usage Examples #

## Initializing the ApiClient ##

```
from poodledo import ApiClient

client = ApiClient()
client.authenticate('my.mail@example.com', 'mypass')
```

## Re-using the authentication key ##

```
from poodledo import ApiClient

client = ApiClient()
key = client.authenticate('my.mail@example.com', 'mypass')

# save key somewhere ...
# so we can skip authenticate later

key = ... # load key from where ever it was stored
client = ApiClient(key)


```


## Tasks ##

### List all Tasks ###
```
all_tasks = client.getTasks()
```

### List Tasks matching a predicate ###


The section _Retrieving Tasks_ in the [Developer's API Documentation](http://www.toodledo.com/info/api_doc.php) lists all available parameters to filter tasks.
You can use them as named parameter in the _getTasks()_ method.

```
# get all Tasks that are not completed
incomplete_tasks = client.getTasks(notcomp=True)

# get all Tasks that are not completed and are starred
starred_incomplete_tasks = client.getTasks(notcomp=True, star=True)

# get all Tasks in the Context 'Home' that are not completed
incomplete_tasks_at_home = client.getTasks(context='Home', notcomp=True)
```

### Deleted Tasks ###

To get a list of tasks IDs of the tasks that were deleted after a specified date and time, you can use the _getDeleted()_ method with the _after_  parameter:

```
deleted_tasks = client.getDeleted(after='2008-01-01 00:00:00')

for task in deleted_tasks:
    # eg: local_db.delete_task(task.id)

```
## Folders ##

### Get the list of Toodledo folders ###

```
folders = client.getFolders()
for f in folders:
    print "%s (%d)" % (f.title, f.id)
```