1.4.0:
======

Features:
---------

* Add `source` command. This allows running sql statement from a file. 

  eg: 
  ```
  mycli> source filename.sql
  ```

* Added a config option to make the warning before destructive commands optional. (Thanks: [Daniel West](https://github.com/danieljwest))

  In the config file ~/.myclirc set `destructive_warning = False` which will
  disable the warning before running `DROP` commands.

* Add completion support for CHANGE TO and other master/slave commands. This is
  still preliminary and it will be enhanced in the future. 

* Add custom styles to color the menus and toolbars. 

* Upgrade prompt_toolkit to 0.46. (Thanks: [Jonathan Slenders](https://github.com/jonathanslenders)) 

  Multi-line queries are automatically indented. 

Bug Fixes:
----------

* Fix keyword completion after the `WHERE` clause.
* Add `\g` and `\G` as valid query terminators. Previously in multi-line mode
  ending a query with a `\G` wouldn't run the query. This is now fixed.

1.3.0:
======

Features:
---------
* Add a new special command (\T) to change the table format on the fly. (Thanks: [Jonathan Bruno](https://github.com/brewneaux))
  eg: 
  ```
  mycli> \T tsv
  ```
* Add `--defaults-group-suffix` to the command line. This lets the user specify
  a group to use in the my.cnf files. (Thanks: [Iryna Cherniavska](http://github.com/j-bennet))

  In the my.cnf file a user can specify credentials for different databases and
  invoke mycli with the group name to use the appropriate credentials.
  eg:
  ```
  # my.cnf
  [client]
  user   = 'root'
  socket = '/tmp/mysql.sock'
  pager = 'less -RXSF'
  database = 'account'

  [clientamjith]
  user     = 'amjith'
  database  = 'user_management'
  
  $ mycli --defaults-group-suffix=amjith   # uses the [clientamjith] section in my.cnf
  ```

* Add `--defaults-file` option to the command line. This allows specifying a
  `my.cnf` to use at launch. This also makes it play nice with mysql sandbox.

* Make `-p` and `--password` take the password in commandline. This makes mycli
  a drop in replacement for mysql. 

1.2.0:
======

Features:
---------

* Add support for wider completion menus in the config file.

  Add `wider_completion_menu = True` in the config file (~/.myclirc) to enable this feature.

Bug Fixes:
---------

* Prevent Ctrl-C from quitting mycli while the pager is active. 
* Refresh auto-completions after the database is changed via a CONNECT command.

Internal Changes:
-----------------

* Upgrade prompt_toolkit dependency version to 0.45.
* Added Travis CI to run the tests automatically.

1.1.1:
======

Bug Fixes:
----------

* Change dictonary comprehension used in mycnf reader to list comprehension to make it compatible with Python 2.6.


1.1.0:
======

Features:
---------

* Fuzzy completion is now case-insensitive. (Thanks: [bjarnagin](https://github.com/bjarnagin))
* Added new-line (`\n`) to the list of special characters to use in prompt. (Thanks: [brewneaux](https://github.com/brewneaux))
* Honor the `pager` setting in my.cnf files. (Thanks: [Iryna Cherniavska](http://github.com/j-bennet))

Bug Fixes:
----------

* Fix a crashing bug in completion engine for cross joins.
* Make `<null>` value consistent between tabular and vertical output.

Internal Changes:
-----------------

* Changed pymysql version to be greater than 0.6.6.
* Upgrade prompt_toolkit version to 0.42. (Thanks: [Yasuhiro Matsumoto](https://github.com/mattn))
* Removed the explicit dependency on six.

2015/06/10:
===========

Features:
---------

* Customizable prompt. (Thanks [Steve Robbins](https://github.com/steverobbins))
* Make `\G` formatting to behave more like mysql.
   
Bug Fixes:
----------

* Formatting issue in \G for really long column values.


2015/06/07:
===========

Features:
---------

* Upgrade prompt_toolkit to 0.38. This improves the performance of pasting long queries. 
* Add support for reading my.cnf files.
* Add editor command \e.
* Replace ConfigParser with ConfigObj.
* Add \dt to show all tables.
* Add fuzzy completion for table names and column names.
* Automatically reconnect when connection is lost to the database.

Bug Fixes:
----------

* Fix a bug with reconnect failure.
* Fix the issue with `use` command not changing the prompt.
* Fix the issue where `\\r` shortcut was not recognized.


2015/05/24
==========

Features:
---------

* Add support for connecting via socket.
* Add completion for SQL functions.
* Add completion support for SHOW statements.
* Made the timing of sql statements human friendly. 
* Automatically prompt for a password if needed.

Bug Fixes:
----------
* Fixed the installation issues with PyMySQL dependency on case-sensitive file systems. 
