# Build git from source

https://stackoverflow.com/questions/21820715/how-to-install-latest-version-of-git-on-centos-7-x-6-x

Step 1: Install Required Packages

Firstly we need to make sure that we have installed required packages on your system. Use following command to install required packages before compiling Git source.

$ yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
$ yum install  gcc perl-ExtUtils-MakeMaker
Step 2: Uninstall old Git RPM

Now remove any prior installation of Git through RPM file or Yum package manager. If your older version is also compiled through source, then skip this step.

$ yum remove git
Step 3: Download and Compile Git Source

Download git source code from kernel git or simply use following command to download Git 2.0.4.

$ cd /usr/src
$ wget https://www.kernel.org/pub/software/scm/git/git-2.0.4.tar.gz
$ tar xzf git-2.0.4.tar.gz
After downloading and extracting Git source code, Use following command to compile source code.

$ cd git-2.0.4
$ make prefix=/usr/local/git all
$ make prefix=/usr/local/git install

$ echo 'export PATH=$PATH:/usr/local/git/bin' >> /etc/bashrc
$  or
$ echo 'export PATH=$PATH:/usr/local/git/bin' > /etc/profile.d/git.sh

$ source /etc/bashrc
HINT 1: Updated method of adding compiled git bin directory to bashrc. Because echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc used "" instead of '', it would expand the current session's value for $PATH instead of keeping it as a variable, and could adversely affect the entire system. At the minimum, it should use '' instead of "" and should really be a separate script in /etc/profile.d/

HINT 2 (@DJB):  /usr/local/git/bin before $PATH, since the older version of git was already on $PATH: export PATH=/usr/local/git/bin:$PATH

Step 4. Check Git Version

One completion of above steps, you have successfully install Git in your system. Let use following command to check git version

$ git --version

git version 2.0.4
