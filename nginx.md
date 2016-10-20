# Nginx


### How is Nginx installed

Nginx is dynamically configured and optimized out of the box based on the detected server's resources available (cpu, memory, disk etc). Nginx has switched back from LibreSSL to OpenSSL for Nginx 1.9.12+ and newer compatibility outlined [here](https://community.centminmod.com/posts/27262/). Currenntly, Nginx 1.11 mainline branch is used which is generally recommended by Nginx as it's more reliable due to all bug fixes ported to Nginx 1.11 mainline branch and not just major critical fixes which applied to the Nginx 1.10 stable branch ([nginx.com](https://www.nginx.com/blog/nginx-1-10-1-11-released/)).

You can see the developer overview of the Nginx install process here.


### Nginx Upgrade

If you are upgrading a server which already previously had Centmin Mod installed, you DO NOT need to run option #1 (in fact as of Centmin Mod v1.2.2-eva2000.14 it will be impossible to run centmin.sh menu option 1 as the script will detect previous install of Centmin Mod and abort the script), instead run centmin.sh menu option 4 and then centmin.sh menu option 5 for upgrading Nginx web server and upgrading PHP. You only need to run these if you upgrading to new Nginx or PHP version. If your existing Centmin Mod install has the same versions for Nginx and PHP, no need to even run those menu options.