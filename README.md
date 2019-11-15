![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 更改所有数据库的兼容性级别
#### Change Compatibility Levels For All Databases
**发布-日期: 2016年12月12日 (评论)**

![#](images/change-compatibility-levels-for-all-databases.png?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
假设你刚刚将一些数据库还原到新的数据库服务器（SQL 2014），你需要仔细检查并更改兼容性级别。这是快速实现这一目标的逻辑。


## English
Suppose you just restored some databases to a new database server (SQL 2014), and you need to double check and perhaps change the compatibility levels. Here’s some quick logic to get that going fast.

---
## Logic
```SQL
use master;
set nocount on
 
-- get compatibility levels from existing databases  --获取现有数据库的兼容级别

select
            'database'       = upper(name)
,           'compatibility'  = compatibility_level
from
            sys.databases
where
            database_id > 4
order by
            name asc
 
-- change compatibility levels to 120 for only those databases that are not set to 120  --仅将那些未设置为120的数据库的兼容级别更改为120

declare              @change_compatibility_level  varchar(max)
set                  @change_compatibility_level  = ''
select               @change_compatibility_level = @change_compatibility_level +
'alter database [' + name + '] set compatibility_level = 120;' + char(10)
from                sys.databases
where               database_id > 4 and compatibility_level not in ('120')
exec                (@change_compatibility_level)


```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

