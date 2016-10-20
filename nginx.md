# Nginx


### How is Nginx installed

Nginx is dynamically configured and optimized out of the box based on the detected server's resources available (cpu, memory, disk etc). Nginx has switched back from LibreSSL to OpenSSL for Nginx 1.9.12+ and newer compatibility outlined [here](https://community.centminmod.com/posts/27262/). Currenntly, Nginx 1.11 mainline branch is used which is generally recommended by Nginx as it's more reliable due to all bug fixes ported to Nginx 1.11 mainline branch and not just major critical fixes which applied to the Nginx 1.10 stable branch ([nginx.com](https://www.nginx.com/blog/nginx-1-10-1-11-released/)).

You can see the developer overview of the Nginx install process here.


### Nginx Upgrade

If you are upgrading a server which already previously had Centmin Mod installed, you DO NOT need to run option #1 (in fact as of Centmin Mod v1.2.2-eva2000.14 it will be impossible to run `centmin.sh menu option 1` as the script will detect previous install of Centmin Mod and abort the script), instead run `centmin.sh menu option 4` and then `centmin.sh menu option 5` for upgrading Nginx web server and upgrading PHP. You only need to run these if you upgrading to new Nginx or PHP version. If your existing Centmin Mod install has the same versions for Nginx and PHP, no need to even run those menu options.


### Automatic Nginx Config Backup

Nginx upgrade process will also backup your existing Nginx conf directory and file via 3 options in centmin.sh: `NGINXBACKUP='y'`, `NGINXCONFDIR='/usr/local/nginx/conf'`, `NGINXBACKUPDIR='/usr/local/nginxbackup'`. You will find backups of previous Nginx versions in timestamped directories located within `/usr/local/nginxbackup`.


### Nginx Upgrade - Error Checking Routine

Centmin Mod has an inbuilt Nginx upgrade error checking routine which checks at Nginx configure, make and make install stages for errors. If any of 3 stages have errors, the script will abort and give you an idea where and what the error is.

For example Nginx configure stage error and script abort due to missing Nginx module file for `nginx-http-concat` module:

```
configuring additional modules
adding module in ../ngx-fancyindex-ngx-fancyindex
 + ngx_http_fancyindex_module was configured
adding module in ../ngx_cache_purge-2.0
 + ngx_http_cache_purge_module was configured
adding module in ../nginx-accesskey-2.0.3
 + ngx_http_accesskey_module was configured
adding module in ../nginx-http-concat-master
./configure: error: no ../nginx-http-concat-master/config was found

Sat Feb 23 22:15:41 CET 2013
Error: 1, Nginx configure failed
```

For more detailed troubleshooting for failed upgrades, you can also check the automated logs when Nginx upgrade runs. The log directory is defined by variable `CENTMINLOGDIR='/root/centminlogs'` in inc/centminlogs.inc. When you run a menu option, the entire process will be logged to a time stamped text log file named `${CENTMINLOGDIR}/centminmod_${SCRIPT_VERSION}_${DT}_*.log` so you can review the logs for error messages etc

Example log listing:

```
ls -lhrt /root/centminlogs/

total 7.3M
4.3M Apr 14 17:14 centminmod_1.2.2-eva2000.15_140412-151749_install.log
1.7M Apr 14 17:44 centminmod_1.2.2-eva2000.15_140412-173219_php_upgrade.log
 30K Apr 14 17:44 centminmod_1.2.2-eva2000.15_140412-173219_apc_reinstall.log
 89K Apr 14 17:45 centminmod_1.2.2-eva2000.15_140412-173219_memcached_reinstall.log
 24K Apr 14 17:46 centminmod_1.2.2-eva2000.15_140412-173219_suhosin_install.log
 17K Apr 14 17:49 centminmod_1.2.2-eva2000.15_140412-173219_ffmpeg_install.log
1.3M Apr 14 18:02 centminmod_1.2.2-eva2000.15_140412-173219_nginx_upgrade.log
 23K Apr 14 18:31 centminmod_1.2.2-eva2000.15_140412-183136_nsd_reinstall.log
 ```
