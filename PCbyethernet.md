The method for getting pH1000 data onto a PC by ethernet connection is described here.

# Introduction #

The BCSI pH1000 v3.4 system is designed to allow a PC to log onto the instrument by FTP and download a "test\_info" file.  This is described in Appendix C of the users manual.  BCSI does not provide software solutions for users to get data off the pH1000 as this is a very customized and specific activity for users's LIS systems.  One method of collecting data using batch files is described here.


# Details #

There are a few steps that need to be done and most of these commands can be handled with batch files, which execute a series of command line actions.

  * FTP into pH1000 and download test records
```
ftp -n -s:pH1000_ftp.scr 192.168.1.100
```
pH1000\_ftp.scr has
```
user
anonymous
anon
get README
get test_info
quit
```
  * Make a time stamp to append to file name
```
set hh=%time:~0,2%
if "%time:~0,1%"==" " set hh=0%hh:~1,1%
FOR %%A IN (%Date%) DO (
    FOR /F "tokens=1-3 delims=/-" %%B in ("%%~A") DO (
        SET yyyymmdd=%%D%%B%%C
    )
)
set yyyymmdd_hhmmss=%yyyymmdd%_%hh%%time:~3,2%%time:~6,2%
```
  * Define the pH1000 serial number
```
for /F "tokens=2,3,* delims=#" %%i IN ('findstr /V "BCSI pH1000" README') do call set unitsn=%%i
del README
```
  * Add UnitSN and date stamp to the file
```
echo a,,,,,%unitsn%,%yyyymmdd_hhmmss% >> test_info
```
  * Rename the file
```
rename test_info test_%unitsn%_%yyyymmdd_hhmmss%.csv
```
  * Check for new records else delete file
```
for /F %%i IN ('findstr "NO RECORDS AVAILABLE" test_%unitsn%_%yyyymmdd_hhmmss%.csv') do call set cont=%%i
if %cont%==NO del test_%unitsn%_%yyyymmdd_hhmmss%.csv
```

These series of commands are in the **pH1000\_ftp.bat** and **pH1000\_ftp.scr** files and can be used to automatically perform these tasks.  The IP address in the pH1000\_ftp.bat file will need to be edited for the specific pH1000 used.