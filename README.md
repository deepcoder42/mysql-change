# Python project for modifying a replication set in a MySQL replication schema.
# Classification (U)

# Description:
  This program is used to administrate changes in a replication set in a MySQL replication schema to include promoting a slave to master status, moving a slave to under a new master, and making a slave a master/slave.


###  This README file is broken down into the following sections:
  * Features
  * Prerequisites
  * Installation
  * Configuration
  * Program Help Function
  * Testing
    - Unit


# Features:
  * Move slave in a slave array to under another slave in the same slave array.
  * Move slave in a slave array to under another slave in the same slave array and remove the replication connection between the current master and new master.
  * Take a slave that is under a slave/master and move it to under the master that is hosting the slave/master.


# Prerequisites:

  * List of Linux packages that need to be installed on the server.
    - git
    - python-pip

  * Local class/library dependencies within the program structure.
    - lib/cmds_gen
    - lib/arg_parser
    - lib/gen_libs
    - lib/machine
    - lib/gen_class
    - mysql_lib/mysql_libs
    - mysql_lib/mysql_class


# Installation:

Install the project using git.
  * Replace **{Python_Project}** with the baseline path of the python program.

```
umask 022
cd {Python_Project}
git clone git@github.com:deepcoder42/mysql-change.git
```

Install/upgrade system modules.

```
cd mysql-change
umask 022
pip install -r requirements.txt --upgrade --system
exit
```

Install supporting classes and libraries.

```
pip install -r requirements-python-lib.txt --target lib --system
pip install -r requirements-mysql-lib.txt --target mysql_lib --system
pip install -r requirements-python-lib.txt --target mysql_lib/lib --system
```

# Configuration:
  * Replace **PYTHON_PROJECT** with the baseline path of the python program.

Create MySQL configuration file and make the appropriate change to the environment.
  * Change these entries in the MySQL setup:
    - user = "USER"
    - japd = "PSWORD"
    - host = "HOST_IP"
    - name = "HOST_NAME"
    - sid = SERVER_ID
    - extra_def_file = "PYTHON_PROJECT/config/mysql.cfg"
    - cfg_file = "DIRECTORY_PATH/my.cnf"
  * Change these entries only if required:
    - serv_os = "Linux"
    - port = 3306

```
cd config
cp mysql_cfg.py.TEMPLATE mysql_cfg.py
vim mysql_cfg.py
chmod 600 mysql_cfg.py
```

Create MySQL definition file and make the appropriate change to the environment.
  * Change these entries in the MySQL definition file:
    - password="PASSWORD"
    - socket="DIRECTORY_PATH/mysqld.sock"

```
cp mysql.cfg.TEMPLATE mysql.cfg
vim mysql.cfg
chmod 600 mysql.cfg
```

Create a MySQL slave configuration file and make the appropriate change to the environment.
  * Change these entries in the MySQL slave setup:
    - user = USER
    - japd = PSWORD
    - rep_user = REP_USER
    - rep_japd = REP_PSWORD
    - host = HOST_IP
    - name = HOST_NAME
    - sid = SERVER_ID
    - extra_def_file = DIRECTORY_PATH/mysql.cfg
  * Change these entries only if required:
    - cfg_file = None
    - serv_os = Linux
    - port = 3306
  * NOTE:  Create a new set of entries for each slave in the MySQL replica set.

```
cp slave.txt.TEMPLATE slave.txt
vim slave.txt
chmod 600 slave.txt
```


# Program Help Function:

  The program has a -h (Help option) that will show display an usage message.  The help message will usually consist of a description, usage, arugments to the program, example, notes about the program, and any known bugs not yet fixed.  To run the help command:
  * Replace **{Python_Project}** with the baseline path of the python program.

```
{Python_Project}/mysql-change/mysql_rep_change.py -h
```


# Testing:

# Unit Testing:

### Installation:

Install the project using git.
  * Replace **{Python_Project}** with the baseline path of the python program.
  * Replace **{Branch_Name}** with the name of the Git branch being tested.  See Git Merge Request.

```
umask 022
cd {Python_Project}
git clone --branch {Branch_Name} git@github.com:deepcoder42/mysql-change.git
```

Install/upgrade system modules.

```
cd mysql-change
sudo bash
umask 022
pip install -r requirements.txt --upgrade --system
exit
```

Install supporting classes and libraries.

```
pip install -r requirements-python-lib.txt --target lib --system
pip install -r requirements-mysql-lib.txt --target mysql_lib --system
pip install -r requirements-python-lib.txt --target mysql_lib/lib --system
```


### Testing:
  * Replace **{Python_Project}** with the baseline path of the python program.

```
cd {Python_Project}/mysql-change
test/unit/mysql_rep_change/unit_test_run.sh
```

### Code Coverage:
```
cd {Python_Project}/mysql-change
test/unit/mysql_rep_change/code_coverage.sh
```

