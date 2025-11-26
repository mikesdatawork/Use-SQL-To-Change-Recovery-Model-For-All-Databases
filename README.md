> **Note** — The folder `linguist-samples/` contains tiny real files so GitHub can correctly display all languages used in this repo.  
> The actual content and examples remain in this README.

![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Use SQL To Change Recovery Model For All Databases
**Post Date: August 30, 2016**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Here's some quick logic to change the recovery models of all databases (excluding system databases). This question comes up quite a bit and there are a number of ways to automate so thought I would throw it out there for anyone that might be interesting in doing it.</p>     


## SQL-Logic
```SQL
use master;
 
set nocount on
 
select name, recovery_model_desc from sys.databases where database_id > 4 order by name asc -- check recovery model for all databases.
 
declare @set_full_recovery_all_databases varchar(max)
 
set @set_full_recovery_all_databases = ''
 
select @set_full_recovery_all_databases = @set_full_recovery_all_databases +
 
'alter database [' + name + '] set recoverty full;' + char(10)
 
from sys.databases where database_id > 4 and state_desc = 'online'
 
exec (@set_full_recovery_all_databases) -- change all databases to full recovery.
 
select name, recovery_model_desc from sys.databases where database_id > 4 order by name asc -- check recovery model again to confirm.
```

![Change SQL Recovery Model]( https://mikesdatawork.files.wordpress.com/2016/08/image0014.png "Change Recovery For SQL Databases")
 


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

 
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")
