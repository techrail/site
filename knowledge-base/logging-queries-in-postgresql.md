---
draft: false
title: How to save PostgreSQL logs
tags:
  - blog
  - vaibhav
  - postgresql
  - logging
  - wiki
---
When developing a backend app (since I work mostly on backend), calling a database is quite a common action that we developers take. As developers, we sometimes use libraries and ORMs to make our lives easy because they help us do more in less time. But sometimes, when we need to debug why something is not working, we need to get into details.

One of the details that ORMs (sometimes even basic-looking connection libraries) hide from the developers is the exact query that they sent to the database and that's quite important for us to work with. To deal with that problem, I usually log the queries that the database receives. 

Since I work with PostgreSQL most of the time, this is how I setup my PostgreSQL installation (tested on version 14, but should work from versions 10 and above).

## Know where your config file is

You would have to edit your config file. The first step to know where the config file is located. This can be very specific to which OS you are on and how you installed PostgreSQL. But no need to scratch your head for that. Just run `psql` and run the command `show config_file;` and it should tell you which file is acting as the config file: 

![[psql_show_config_file.jpg]]
Although the version of the PostgreSQL in the screenshot is a bit old, it works for any version from 10.x to 16. I have used this command for quite some time.
## Setup logging correctly
You would have to edit the config file. You can basically paste the lines below and it should work. But the better way would be to look for each setting (part before `=`) in the file, read the info given in the file (yes, postgresql is well documented every step of the way) and understand what you are doing.

```
log_destination = 'stderr'
logging_collector = on
log_directory = '/Users/vaibhavkaushal/tmp/postgres_logs'
log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
log_file_mode = 0777
log_checkpoints = on
log_connections = on
log_disconnections = on
log_statement = 'all'
log_timezone = 'Asia/Kolkata'
```
## What do those options mean?
Remember to read about what these mean in the config file. But in short, you have to focus on these: 

1. `log_destination = 'stderr'` - The config file says you can use other values but I have not always succeeded in making those work. This setting almost always works.
2. `logging_collector = on` - If you do not set the logging_collector on, nothing seems to work in my observation.
3. `log_directory = '/Users/vaibhavkaushal/tmp/postgres_logs'` - You are setting the directory (remember, the **directory**) where log files will be created. Make sure it exists, the path you set in the file does not end in a `/` and that postgres will be able to write to it. 
4. `log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'` - The format in which the filename will be created in the directory you just mentioned.
5. `log_file_mode = 0777` - This is **insecure** in a way but this setting is about debugging on development machines. Do not use this setting on production. This is the permission that is applied to the file that gets created by the PostgreSQL daemon.
6. `log_statement = 'all'` - This asks postgres to log all statements it receives.

There are a lot more options which control the behavior but the default ones are good enough for most needs.

## Don't forget to restart your server

> [!info]+ Don't forget!
> 
> Remember to restart your PostgreSQL server for the settings to take effect.

That should start logging your queries in the file and allow debugging your code better!