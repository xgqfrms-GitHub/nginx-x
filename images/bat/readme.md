# bat for windows (one key execute)


### start_nginx.bat

```bat
@ECHO OFF

REM Start Nginx
tasklist /FI "IMAGENAME eq nginx.exe" 2>NUL | find /I /N "nginx.exe">NUL
IF NOT "%ERRORLEVEL%"=="0" (
   REM Nginx is NOT running, so start it
   d:
   cd \Nginx2016
   start nginx.exe
   ECHO Nginx started.
) else (
   ECHO Nginx is already running.
)

REM Start php-cgi
tasklist /FI "IMAGENAME eq php-cgi.exe" 2>NUL | find /I /N "php-cgi.exe">NUL
IF NOT "%ERRORLEVEL%"=="0" (
   REM php-cgi is NOT running, so start it
   start /min d:\Nginx2016\php\php-cgi.exe -b localhost:9000 -c d:\Nginx2016\php\php.ini
   ECHO php-cgi started.
) else (
   ECHO php-cgi is already running.
)

``` 



### stop_nginx.bat

```bat
@ECHO OFF

REM Stop Nginx
tasklist /FI "IMAGENAME eq nginx.exe" 2>NUL | find /I /N "nginx.exe">NUL
IF "%ERRORLEVEL%"=="0" (
   REM Nginx is currently running, so quit it
   d:
   cd \Nginx2016
   nginx.exe -s quit
   ECHO Nginx quit issued.
) else (
   ECHO Nginx is not currently running.
)

REM Stop php-cgi
tasklist /FI "IMAGENAME eq php-cgi.exe" 2>NUL | find /I /N "php-cgi.exe">NUL
IF "%ERRORLEVEL%"=="0" (
   REM php-cgi is currently running, so quit it
   taskkill /f /IM php-cgi.exe
   ECHO php-cgi killed.
) else (
   ECHO php-cgi is not currently running.
)

``` 




