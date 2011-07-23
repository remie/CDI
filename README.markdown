# Continuous Database Integration

* Version: 0.3.0
* Author: Remie Bolte <http://github.com/remie>
* Build Date: 2011-07-22
* Requirements: Symphony 2.2.1, requires a small modification to class.mysql.php (see below)

Special thanks go out to Nick Dunn <http://github.com/nickdunn/> and Richard Warrender <http://github.com/rwarrender>. 
Part of the code comes from their DB_Sync <https://github.com/nickdunn/db_sync> extension. 
Future patches to their extension will be closely monitored and implemented to increase the stability of this extension.

## Installation

1. Download the CDI extension and upload the 'cdi' folder to the 'extensions' folder of all your Symphony instances on all your environments.
2. Enable the extension by selecting "Continuous Database Integration" in the list and choose Enable from the with-selected menu, then click Apply.
3. Modify the `query()` function in `symphony/lib/toolkit/class.mysql.php` adding the lines between `// Start database logger` and `// End database logger` from the `class.mysql.php.txt` file included with this extension. Place these before the start of the Profile performance logging so it doesn't interfere with performance monitoring and regular query execution.

## Warning

Since this extension requires a core file modification, changes you make to the MySQL class will be lost when you upgrade Symphony. 
Remember to add in the logging call back into `class.mysql.php` if you update Symphony!

The queries are stored in a folder named `cdi` in your `/manifest` folder. This is unsecured, and therefore I strongly advise that you 
alter you .htaccess file to prevent your webserver from exposing these files.

## Disclaimer

Although it is designed to assist you with the entire release chain of development, test, acceptance and production, I cannot guarantee that it is stable. 
Be sure that you have executed the database updates on all environments before going to production. To avoid the risk of database integrity issues, be sure
to create a backup of your data in production, and only run the upgrade in maintenance mode. This allows you to revert any damage that was caused by this extension.

## Roadmap

* Add support for DATA changes from the backend

* Implement a rolling file appending strategy to prevent the aggregated SQL files from becoming to large

* Add support for DATA changes from the front-end

* Add support for active replication (for load-balancing)

## Version History

### 0.4.0
* Added automatic backup of current database before executing CDI queries using https://github.com/nils-werner/dump_db

* Added automatic restore of database backup upon query execution errors (including switch to maintenance mode) 

* Added support for manual backup & restore of current database using https://github.com/nils-werner/dump_db

* UI tweaks and Ajaxification of the preferences implementation

### 0.3.0
* Support the same features as the Database Synchroniser extension: a single db_sync.sql file that logs all queries for manual propagating changes to other instances.

* Aggregate all queries and save them to a single file (using JSON or XML serialization)
  WARNING: this feature breaks backwards compatibility with version 0.2.0

### 0.2.0
* Add rollback support in case of SQL execution errors

* Add status information of the CDI log on the preferences screen

* Add a "clear CDI log" button from the preferences screen

### 0.1.0
* initial release of this extension, waiting impatiently for your feedback!