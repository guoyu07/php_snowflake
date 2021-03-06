# php_snowflake

[中文文档](https://github.com/Sxdd/php_snowflake/wiki/%E4%B8%AD%E6%96%87%E6%96%87%E6%A1%A3)
## What is php_snowflake?

Twitter distributed ID generating Algorithm [SnowFlake](https://github.com/twitter/snowflake) PHP implementation version.

## Requires
* PHP >= 5.6  (Below 5.5 self-testing)
* Linux

## Description
Pure PHP can not be achieved SnowFlake algorithm，because version of thread-safe(requires tid)and 
non-thread-safe(requires pid)can not generate same the format id(The only tid of this project system, 
so don't worried about pid conflict of multiple processes). And PHP as scripting language can not maintain sequence,
sequence will be initialized again when the script is finished. In case of high concurrency pure PHP 
Implemented version of  Snowflate algorithm does not have any effect. So was born this project, 
below is the different of Thread-safe version and Non-thread-safe version.

### Non-thread-safe version (NTS)
```
0　0　　　　　　    13　　　　　　 　15   23　　　   26
---+----------------+--------------+----+----------+
   |timestamp(ms)  | service_no 　 |pid | sequence |
---+----------------+--------------+----+----------+
```

### Thread-safe version (TS)
```
0　0　　　　　 　   13　　　　　　 　15   23　　　   26
---+----------------+--------------+----+----------+
   |timestamp(ms)  | service_no 　 |tid | sequence |
---+----------------+--------------+----+----------+
```

## Installation
```
phpize
./configure --with-php-config=/you/phppath/php-config
make
make install
```
## Example
Attention： Interval of $service_no in the range of 10-99. Beyond that scope, PHP will report a fatal mistake.
```
$service_no = 99;
for ($i=0; $i < 10; $i++) { 
        echo PhpSnowFlake::nextId($service_no)."\n";
}
/*

15098671568796600005457001
15098671512126600005457001
15098671509876600005308001

*/
```
## License
Copyright (c) 2016 by [Towers](http://towers.pub) released under MIT License.



```angular2html

make clean 
./configure --with-php-config=/usr/bin/php-config7.1 
make 
sudo make install 
sudo service php7.1-fpm restart

```
