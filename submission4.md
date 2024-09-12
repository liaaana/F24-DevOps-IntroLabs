# Task 1: Configure and Use a Local Package Repository
## Downloaded teamviewer.deb from the internet

## Created local repo

```sh
mkdir -p ~/local-apt-repo
cp /home/ubuntu/Downloads/teamviewer.deb ~/local-apt-repo/
```

## Tried to generate a package index. Faced errors and resolved them.

```sh
dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz
sudo apt install dpkg-dev
sudo apt install dpkg-dev --fix-missing
sudo apt update
```

## Generated a package index

```sh
dpkg-scanpackages ~/local-apt-repo /dev/null | gzip -9c > ~/local-apt-repo/Packages.gz
```

## Added the local repo to sources list

```sh
echo "deb [trusted=yes] file:/home/ubuntu/local-apt-repo ./" | sudo tee /etc/apt/sources.list.d/local-apt-repo.list
sudo apt update
```

**Got error and fixed it by manually extracting Packages.gz. Additionally updated path to make it relative.**

``` sh
E: Failed to fetch file:/home/ubuntu/local-apt-repo/./Packages  File not found - /home/ubuntu/local-apt-repo/./Packages (2: No such file or directory)
```

## Verified content of the Packages.gz

```sh
cd local-apt-repo/
zcat Packages.gz
apt policy teamviewer
```

### Output 

``` sh
Package: teamviewer
Version: 15.57.3
Architecture: arm64
Maintainer: TeamViewer Germany GmbH <service@teamviewer.com>
Installed-Size: 332020
Depends: libc6 (>= 2.17), libdbus-1-3, libexpat1, libfontconfig1, libfreetype6, libglib2.0-0, libgl1, libice6, libminizip1, libnspr4, libnss3, libsm6, libx11-6, libx11-xcb1, libxcb1, libxcb-glx0, libxcb-icccm4, libxcb-image0, libxcb-keysyms1, libxcb-randr0, libxcb-render0, libxcb-render-util0, libxcb-shape0, libxcb-shm0, libxcb-sync1, libxcb-xfixes0, libxcb-xinerama0, libxcb-xkb1, libxcomposite1, libxcursor1, libxdamage1, libxext6, libxfixes3, libxi6, libxkbcommon0, libxkbcommon-x11-0, libxrandr2, libxrender1, libxss1, libxtst6, zlib1g, libpolkit-agent-1-0, policykit-1
Recommends: ttf-liberation | fonts-liberation, xdg-utils
Conflicts: teamviewer-host
Filename: /home/ubuntu/local-apt-repo/teamviewer.deb
Size: 93218320
MD5sum: 7545690cc2fb058cab93ac040e7df48f
SHA1: a4ee0050aad644e32f83b66e75c7de2e3d766d27
SHA256: 031ce64d39f65979d6fb86eee200201682b28013e46665cf603e6c731294624a
Section: non-free/net
Priority: optional
Homepage: http://www.teamviewer.com
Description: Remote control and meeting solution.
 TeamViewer provides easy, fast and secure remote access and meeting solutions
 to Linux, Windows PCs, Apple PCs and various other platforms,
 including Android and iPhone.
 .
 TeamViewer is free for personal use.
 You can use TeamViewer completely free of charge to access your private
 computers or to help your friends with their computer problems.
 .
 To buy a license for commercial use, please visit http://www.teamviewer.com
 .
 This package contains Free Software components.
 For details, see /opt/teamviewer/doc/license_foss.txt
```

### Output

``` sh
 teamviewer:
  Installed: (none)
  Candidate: 15.57.3
  Version table:
     15.57.3 500
        500 file:/home/ubuntu/local-apt-repo ./ Packages
```

## Installed package from local repo

```sh
sudo apt install teamviewer
```

Successfully installed! (Verified the installation by `teamviewer` command)

# Task 2: Configure and Use a Local Package Repository

## Chose a package `nginx` to simulate installation

```sh
apt-cache showpkg nginx
```

### Output

```sh
Package: nginx
Versions: 
1.18.0-6ubuntu14.4 (/var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy-updates_main_binary-arm64_Packages)
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: en
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy_main_i18n_Translation-en
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy-updates_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy-security_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8

1.18.0-6ubuntu14.3 (/var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy-security_main_binary-arm64_Packages)
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: en
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy_main_i18n_Translation-en
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy-updates_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy-security_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8

1.18.0-6ubuntu14 (/var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy_main_binary-arm64_Packages)
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: en
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy_main_i18n_Translation-en
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy-updates_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8
 Description Language: 
                 File: /var/lib/apt/lists/ports.ubuntu.com_ubuntu-ports_dists_jammy-security_main_binary-arm64_Packages
                  MD5: 902443ddbee17249123a068e7ca7c6d8


Reverse Depends: 
  nginx-core,nginx 1.4.5-1
  nginx-light,nginx 1.4.5-1
  nginx-full,nginx 1.4.5-1
  nginx-extras,nginx 1.4.5-1
  libnginx-mod-stream-geoip,nginx
  libnginx-mod-rtmp,nginx
  libnginx-mod-nchan,nginx
  libnginx-mod-http-upstream-fair,nginx
  libnginx-mod-http-uploadprogress,nginx
  libnginx-mod-http-subs-filter,nginx
  libnginx-mod-http-perl,nginx
  libnginx-mod-http-ndk,nginx
  libnginx-mod-http-headers-more-filter,nginx
  libnginx-mod-http-geoip,nginx
  libnginx-mod-http-fancyindex,nginx
  libnginx-mod-http-echo,nginx
  libnginx-mod-http-dav-ext,nginx
  libnginx-mod-http-cache-purge,nginx
  libnginx-mod-http-auth-pam,nginx
  nginx-core,nginx 1.4.5-1
  libnginx-mod-stream-geoip2,nginx
  libnginx-mod-stream,nginx
  libnginx-mod-mail,nginx
  libnginx-mod-http-xslt-filter,nginx
  libnginx-mod-http-image-filter,nginx
  libnginx-mod-http-geoip2,nginx
  nginx-light,nginx 1.4.5-1
  nginx-full,nginx 1.4.5-1
  nginx-extras,nginx 1.4.5-1
  libnginx-mod-stream-geoip,nginx
  libnginx-mod-rtmp,nginx
  libnginx-mod-nchan,nginx
  libnginx-mod-http-upstream-fair,nginx
  libnginx-mod-http-uploadprogress,nginx
  libnginx-mod-http-subs-filter,nginx
  libnginx-mod-http-perl,nginx
  libnginx-mod-http-ndk,nginx
  libnginx-mod-http-headers-more-filter,nginx
  libnginx-mod-http-geoip,nginx
  libnginx-mod-http-fancyindex,nginx
  libnginx-mod-http-echo,nginx
  libnginx-mod-http-dav-ext,nginx
  libnginx-mod-http-cache-purge,nginx
  libnginx-mod-http-auth-pam,nginx
  collectd-core,nginx
  cacti,nginx
  nginx-core,nginx 1.4.5-1
  libnginx-mod-stream-geoip2,nginx
  libnginx-mod-stream,nginx
  libnginx-mod-mail,nginx
  libnginx-mod-http-xslt-filter,nginx
  libnginx-mod-http-image-filter,nginx
  libnginx-mod-http-geoip2,nginx
  zoneminder,nginx
  zabbix-frontend-php,nginx
  sugarplum,nginx
  searx,nginx
  samizdat,nginx
  rss-bridge,nginx
  rainloop,nginx
  python3-searx,nginx
  python3-certbot-nginx,nginx
  nginx-light,nginx 1.4.5-1
  nginx-full,nginx 1.4.5-1
  nginx-extras,nginx 1.4.5-1
  mailman3-web,nginx
  libnginx-mod-stream-geoip,nginx
  libnginx-mod-rtmp,nginx
  libnginx-mod-nchan,nginx
  libnginx-mod-http-upstream-fair,nginx
  libnginx-mod-http-uploadprogress,nginx
  libnginx-mod-http-subs-filter,nginx
  libnginx-mod-http-perl,nginx
  libnginx-mod-http-ndk,nginx
  libnginx-mod-http-headers-more-filter,nginx
  libnginx-mod-http-geoip,nginx
  libnginx-mod-http-fancyindex,nginx
  libnginx-mod-http-echo,nginx
  libnginx-mod-http-dav-ext,nginx
  libnginx-mod-http-cache-purge,nginx
  libnginx-mod-http-auth-pam,nginx
  lemonldap-ng-uwsgi-app,nginx
  lemonldap-ng-fastcgi-server,nginx
  kopano-webapp-nginx,nginx
  fusiondirectory,nginx
  fcgiwrap,nginx
  colplot,nginx
  cacti,nginx
  libnginx-mod-http-geoip2,nginx
  libnginx-mod-stream-geoip2,nginx
  libnginx-mod-stream,nginx
  libnginx-mod-mail,nginx
  libnginx-mod-http-xslt-filter,nginx
  libnginx-mod-http-image-filter,nginx
Dependencies: 
1.18.0-6ubuntu14.4 - nginx-core (19 1.18.0-6ubuntu14.4.1~) nginx-full (19 1.18.0-6ubuntu14.4.1~) nginx-light (19 1.18.0-6ubuntu14.4.1~) nginx-extras (3 1.18.0-6ubuntu14.4.1~) nginx-core (18 1.18.0-6ubuntu14.4) nginx-full (18 1.18.0-6ubuntu14.4) nginx-light (18 1.18.0-6ubuntu14.4) nginx-extras (2 1.18.0-6ubuntu14.4) libnginx-mod-http-lua (3 1.18.0-6ubuntu5) 
1.18.0-6ubuntu14.3 - nginx-core (19 1.18.0-6ubuntu14.3.1~) nginx-full (19 1.18.0-6ubuntu14.3.1~) nginx-light (19 1.18.0-6ubuntu14.3.1~) nginx-extras (3 1.18.0-6ubuntu14.3.1~) nginx-core (18 1.18.0-6ubuntu14.3) nginx-full (18 1.18.0-6ubuntu14.3) nginx-light (18 1.18.0-6ubuntu14.3) nginx-extras (2 1.18.0-6ubuntu14.3) libnginx-mod-http-lua (3 1.18.0-6ubuntu5) 
1.18.0-6ubuntu14 - nginx-core (19 1.18.0-6ubuntu14.1~) nginx-full (19 1.18.0-6ubuntu14.1~) nginx-light (19 1.18.0-6ubuntu14.1~) nginx-extras (3 1.18.0-6ubuntu14.1~) nginx-core (18 1.18.0-6ubuntu14) nginx-full (18 1.18.0-6ubuntu14) nginx-light (18 1.18.0-6ubuntu14) nginx-extras (2 1.18.0-6ubuntu14) libnginx-mod-http-lua (3 1.18.0-6ubuntu5) 
Provides: 
1.18.0-6ubuntu14.4 - 
1.18.0-6ubuntu14.3 - 
1.18.0-6ubuntu14 - 
Reverse Provides: 
nginx-light 1.18.0-6ubuntu14.3 (= )
nginx-full 1.18.0-6ubuntu14.3 (= )
nginx-extras 1.18.0-6ubuntu14.3 (= )
nginx-core 1.18.0-6ubuntu14.3 (= )
nginx-light 1.18.0-6ubuntu14.4 (= )
nginx-full 1.18.0-6ubuntu14.4 (= )
nginx-extras 1.18.0-6ubuntu14.4 (= )
nginx-core 1.18.0-6ubuntu14.4 (= )
nginx-light 1.18.0-6ubuntu14 (= )
nginx-full 1.18.0-6ubuntu14 (= )
nginx-extras 1.18.0-6ubuntu14 (= )
nginx-core 1.18.0-6ubuntu14 (= )
```

## Simulated the installation

```sh
sudo apt-get install -s nginx
```

### Output

```sh
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libnginx-mod-http-geoip2 libnginx-mod-http-image-filter
  libnginx-mod-http-xslt-filter libnginx-mod-mail libnginx-mod-stream
  libnginx-mod-stream-geoip2 nginx-common nginx-core
Suggested packages:
  fcgiwrap nginx-doc
The following NEW packages will be installed:
  libnginx-mod-http-geoip2 libnginx-mod-http-image-filter
  libnginx-mod-http-xslt-filter libnginx-mod-mail libnginx-mod-stream
  libnginx-mod-stream-geoip2 nginx nginx-common nginx-core
0 upgraded, 9 newly installed, 0 to remove and 117 not upgraded.
Inst nginx-common (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [all])
Inst libnginx-mod-http-geoip2 (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Inst libnginx-mod-http-image-filter (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Inst libnginx-mod-http-xslt-filter (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Inst libnginx-mod-mail (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Inst libnginx-mod-stream (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Inst libnginx-mod-stream-geoip2 (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Inst nginx-core (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Inst nginx (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Conf nginx-common (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [all])
Conf libnginx-mod-http-geoip2 (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Conf libnginx-mod-http-image-filter (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Conf libnginx-mod-http-xslt-filter (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Conf libnginx-mod-mail (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Conf libnginx-mod-stream (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Conf libnginx-mod-stream-geoip2 (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Conf nginx-core (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
Conf nginx (1.18.0-6ubuntu14.4 Ubuntu:22.04/jammy-updates [arm64])
```


## Output analysis

Examined the versions and dependencies of the nginx package and simulated its installation. The simulation demonstrated that the installation of nginx would also install several associated packages, thereby guaranteeing that all essential components are included. Commands from this task help in managing and understanding dependencies and packages.

### Dependencies and packages for installation with versions:

```sh
nginx-common (1.18.0-6ubuntu14.4)
libnginx-mod-http-geoip2 (1.18.0-6ubuntu14.4)
libnginx-mod-http-image-filter (1.18.0-6ubuntu14.4)
libnginx-mod-http-xslt-filter (1.18.0-6ubuntu14.4)
libnginx-mod-mail (1.18.0-6ubuntu14.4)
libnginx-mod-stream (1.18.0-6ubuntu14.4)
libnginx-mod-stream-geoip2 (1.18.0-6ubuntu14.4)
nginx-core (1.18.0-6ubuntu14.4)
nginx (1.18.0-6ubuntu14.4)
```

# Task 3: Hold and Unhold Package Versions

## Install a package

```sh
sudo apt install teamviewer
```

## Hold the choosen package

```sh
sudo apt-mark hold teamviewer
```

### Output
```sh
teamviewer set on hold.
```

## Check held packages

```sh
apt-mark showhold
```

### Output

```sh
teamviewer
```

## Unhold the package

```sh
sudo apt-mark unhold teamviewer
```

### Output

```sh
Canceled hold on teamviewer.
```

## Check held packages again


```sh
apt-mark showhold
```

### Output

Empty => no packages are hold