Git is a distributed version control system.
# ATS_autest
note ATS_autest

export https_proxy=https://proxy-prc.intel.com:911
export http_proxy=http://proxy-prc.intel.com:911

1.	records.config
/etc/trafficserver/records.config:  change the following defaults –
CONFIG proxy.config.cache.threads_per_disk INT 16
CONFIG proxy.config.cache.ram_cache.size INT 21474836480 (20GB)
CONFIG proxy.config.cache.ram_cache_cutoff INT 4194304 (4MB)
CONFIG proxy.config.cache.limits.http.max_alts INT 5
CONFIG proxy.config.body_factory.template_sets_dir STRING body_factory     (not found)
CONFIG proxy.config.url_remap.filename STRING remap.config
CONFIG proxy.config.ssl.server.ticket_key.filename STRING NULL

2.	remap.config
/etc/trafficserver/remap.config:  change to reflect the HTTP content server location --
第一个用户访问baidu.com 第二个是 ATS自动去访问baidu.com取源，当然也可以是ip地址
map http://www.baidu.com/ http://www.baidu.com/
这个测试当做百度的一个代理服务器，192.168.1.100是TS所在服务器的IP地址

3.	storage.config
/etc/trafficserver/storage.config:  change to reflect the correct (list of) cache storage device(s).  Could be a raw disk endpoint or a mount point.  Raw disk preferred --
30GB or MB

make clean
make clean all -j4
make distclean
rm -rf /usr/lib/trafficserver /etc/trafficserver /opt/ats


autoreconf -if
./configure --prefix=/opt/ats --sysconfdir=/etc/trafficserver --libdir=/usr/lib/trafficserver --with-user=pid --with-group=pid --disable-silent-rules --enable-wccp --enable-experimental-plugins    --enable-linux-native-aio  --enable-experimental-linux-native-aio
sudo make && make install

time ./autest.sh --ats-bin /opt/ats/bin/ | tee `date +%Y%m%d_%H%M%S`.log



root@badcpaewp007:/home/pid/nginx/trafficserver-8.0.0/tests# ./autest.sh --ats-bin /opt/ats/bin/ -h
usage: autest run [-h] [-R [REPORTERS [REPORTERS ...]]] [-j JOBS] [-C CLEAN]
                  [--normalize-kill NORMALIZE_KILL] [-D DIRECTORY]
                  [--autest-site [AUTEST_SITE [AUTEST_SITE ...]]]
                  [--sandbox SANDBOX] [--env [Key=Value [Key=Value ...]]]
                  [-f [FILTERS [FILTERS ...]]] [-V] --ats-bin ATS_BIN
                  [--show-color] [--disable-color]
                  [--verbose [CATEGORY [CATEGORY ...]]]
                  [--debug [CATEGORY [CATEGORY ...]]]

optional arguments:
  -h, --help            show this help message and exit
  -R [REPORTERS [REPORTERS ...]], --reporters [REPORTERS [REPORTERS ...]]
                        Names of Reporters to use for report generation
  -j JOBS, --jobs JOBS  The number of test to try to run at the same time
  -C CLEAN, --clean CLEAN
                        Level of cleaning for after a test is finished. all >
                        exception > failed > warning > passed > skipped >
                        unknown> none Defaults at passed
  --normalize-kill NORMALIZE_KILL
                        Normalizes the exit code when a process is given
                        SIGKILL
  -D DIRECTORY, --directory DIRECTORY
                        The directory with all the tests in them
  --autest-site [AUTEST_SITE [AUTEST_SITE ...]]
                        A user provided autest-site director(y)ies to use
                        instead of the default.
  --sandbox SANDBOX     The root directory in which the tests will run
  --env [Key=Value [Key=Value ...]]
                        Set a variable to be used in the local test
                        environment. Replaces value inherited from shell.
  -f [FILTERS [FILTERS ...]], --filters [FILTERS [FILTERS ...]]
                        Filter the tests run by their names
  -V, --version         show program's version number and exit
  --ats-bin ATS_BIN     A user provided directory to ATS bin

Console options:
  Arguments unique to console

  --show-color          Show colored output
  --disable-color       Disable colored output
  --verbose [CATEGORY [CATEGORY ...]], -v [CATEGORY [CATEGORY ...]]
                        Display all verbose messages or only messages of
                        provided categories
  --debug [CATEGORY [CATEGORY ...]]
                        Display all debug messages or only messages of
                        provided categories

						
						
sudo apt-get install git
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
git clone https://github.com/enzomao/ATS_autest.git
cd 
git status
git add -A
git commit -m ""
git push
username & password


t is a distributed version control system.
