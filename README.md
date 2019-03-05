# linux_cmd_examples
list of usefull linux commando line examples

## index
1. [system](#system)
2. [wget](#wget-and-curl)
3. [archiving utilitys](#archiving-utilitys)
4. [search and found](#search-and-found)
5. [python](#python)
6. [xargs](#xargs)
7. [files](#files) work with files
8. [ncftp](#ncftp) and other ftp clients
9. pass

## system
update ubunut, debian, linuxmint etc...
```bash
sudo apt-get upade && sudo apt-get upgrade -y
```

## wget and curl
```sh
# wget spider
wget -r -nd --spider -o links.txt -np --post-data="username=admin&password=password&Login=Login" --keep-session-cookies http://localhost/vuln_test/DVWA/login.php
wget -r --spider -o links.txt http://www.kultur-cottbus.de/
cat links.txt |grep -o -E "(http[s]?://.*)\n" > spider.txt
cat links.txt |grep -o -P "http[s]?://[^ \r\n]+" > spider.txt
```

```sh
# wget download online greping ftp filez and multithreading
wget --no-remove-listing "ftp://saug:mich@localhost:2222/REQUEST/"
awk '{print $NF}' .listing |td -d "\r" |grep "EUR" > .downloading
xargs -a .downloading -i -n 1 -P 2 wget -c -r "ftp://saug:mich@localhost:2222/REQUEST/{}"
```

```sh
# same as singel liner oneliner
wget --no-remove-listing "ftp://localhost/" |awk '{print $NF}' .listing |td -d "\r" |xargs -P4 -i proxychains wget -nH -nd -r -c "ftp://localhost/"
```

```sh
# wget login to uploaded.net and make cookiefile
wget -O - --save-cookies=ulnet --post-data="id=123789&pw=pass123" "http://uploaded.net/io/login"
# wget filelist downloader with cookie and use remotefilename for the localname
wget --load-cookies=ulnet --content-disposition -i links.txt
# wget downloader use with cookie and use remotefilename for the localname
wget --load-cookies=ulnet --content-disposition -i "$link"
# curl variante
curl -L -J -b ulnet "$link"
# multi download with xargs
xargs -a och.txt -n 1 -P 3 wget -c --load-cookies=../../../ulnet --content-disposition > /dev/null &
# download recrusiv a ftp folder
wget -r -c -nH -nd ftp://wii:games@localhost:4681 > /dev/null &
```

# archiving utilitys
```sh
## unrar für unix
wget http://www.rarlab.com/rar/rarlinux-3.6.0.tar.gz && tar -zxvf rarlinux-3.6.0.tar.gz && mv rar rar2 && cp ./rar2/rar_static rar && rm rarlinux-3.6.0.tar.gz && rm -r rar2
## copy download befehle
wget bwc.php http://rarlab.com/rar/rarlinux-5.0.0.tar.gz
curl -O http://rarlab.com/rar/rarlinux-5.0.0.tar.gz
var_dump(copy("http://rarlab.com/rar/rarlinux-5.0.0.tar.gz", "rarlinux-5.0.0.tar.gz"));
### unrar entpacken
./rar x -o+ -pPASSWORT -y \*part1.rar

## rar packen
rar a -m1 -v1024m archiv.rar datei folder
-hp = password

## gzip gz packen komprimieren
gzip -9 -r ./ordner/ > ./backup.sql.gz
gzip -d backup.sql.gz
### archiv.tar.gz
tar cfzv archiv.tar.gz inhalt1 inhalt2 inhalt3
### archiv.tar.bz2
tar cfvj archiv.tar.bz2 inhalt1 inhalt2

## bz2 entpacken mit tar
tar xfvj tinyproxy-1.8.3.tar.bz2
tar -xjf example.tar.bz2
tar xfv example.tar.xz
bzip2 -d wikipedia-wordlist-sraveau-20090325.txt.bz2

## normales entpacken (tar, tar.gz)
tar xfvz example.tar

## unix backup tar:
tar -cvf /opt/lampp/htdocs/webface.tar /opt/lampp/htdocs/tmp

tar -cvzf pop3.tar.gz datei1 datei2 ordner blabla
```
[Archive_unter_Linux_(tar,_gz,_bz2,_zip)](https://www.thomas-krenn.com/de/wiki/Archive_unter_Linux_(tar,_gz,_bz2,_zip))


## search and found
```sh
## suche, datein inhalte recrusiv
grep -w -i "_SERVER\['REMOTE_ADDR'\]" -r ./*
grep -w -i "eval(" -r ./*
grep -w -i "16codezBZqw3Uc2tCcrxZ3q62SFoKGjJFq" -r ./*

## suchen und ersetzten in mehreren datein
find ./test/plugin -type f -exec sed -i 's/from bs4 import \*/from thirdparty.beautifulsoup import \*/g' {} \;
﻿

## extrem suche
find $(pwd) -name "*.php" -print0 |xargs -0 -i -n 1 -P 4 grep -H -n -w -i "SEARCHSTRING" {}
find $(pwd) -name "*.php" -print0 |xargs -0 -i -n 1 -P 2 grep -H -n -w -i "SCRIPTNAME" {}
find . -name '*.py' -print0 | xargs -0 -i grep -H -n -w -i "argparse" {} >> find.txt
```

## python
```sh
# download python static
curl http://pts-mini-gpl.googlecode.com/svn/trunk/staticpython/d.sh | bash /dev/stdin python2.7-static
wget https://github.com/elyase/docker/raw/master/staticpython/python2.7-static
```

## xargs
```sh
## xargs with wget (4 threads)
xargs -a downloadlist -n 1 -P 4 wget

## xargs python wordpress bruter start command
xargs --arg-file=wp.txt -i -n 1 -P 25 python wpbf.py -nps -t 2 {} > /dev/null &
xargs -a wp2.txt -n 1 -P 25 python wpbf.py -w wordlist.txt -t 5 -nf -nps -mu 3 > /dev/null &
xargs -a wp3.txt -i -n 1 -P 25 python wpbf.py -w wordlist.txt -t 2 -nf -nps -mu 3 {} > /dev/null &
xargs -a wp-ovh.txt -P15 python darkwp.py -u
```

## files
```sh
## um ungewünschte zeichen los zu bekommen "\r"
## kill "\r" from file names
rename 's/\%0D$//' /opt/lampp/htdocs/tmp/test/kiff/*\%0D
```
## ncftp
```sh
## ncftp client full download
wget -O nc.tar.gz "ftp://ftp.ncftp.com/ncftp/binaries/ncftp-3.2.5-linux-x86_64-glibc2.3-export.tar.gz" && tar -zxvf nc.tar.gz && rm nc.tar.gz && mv ncftp-3.2.5 nc && ./nc/bin/ncftpput --help

### ncftpput upload
./ncftpput -u 123789 -p 654789 -P 21 -R "ftp.uploaded.net" "./" "./ubuntu.iso"
./ncftpput -u anonymous -p anonymous -P 21 -R "localhost" "/bin/.log/backup" "*gz"

### ncftpput datein im ordner ansprechen und uploaden
./ncftpput -u anonymous -p anonymous -P 21 -R "localhost" "/folder/" "./folder/*.*"
./ncftpput -u anonymous -p anonymous -P 21 -R "127.0.0.1" "/folder/" "./folder/*"

### ncftpput upload with continue, recrusiv and error log
./nc/bin/ncftpput -u anonymous -p anonymous -P 21 -e nc_error.log -z -R "REMOTEHOST" "/remotefolder/" "./localfolder/" >> /dev/null &

### ncftpput multi upload with find and xargs
find ./FAQready/* -type d -maxdepth 1 -print0 | xargs -0 -i -n 1 -P 3 ./ncftp/bin/ncftpput -e nc_error.log -u p0rn -p master -P 2221 -z -R "192.0.0.1" "/XXX/" {}
find ./ftp/javaftpd/home/* -type d -maxdepth 1 -print0 | xargs -0 -i -n 1 -P 2 ./ncftp/bin/ncftpput -e nc_error_dvc.log -u p0rn -p master -P 2221 -z -R "127.0.0.1" "/XXX/" {}
find ./ftp/javaftpd/home/* -type d -maxdepth 1 -print0 | xargs -0 -i -n 1 -P 2 ./ncftp/bin/ncftpput -e nc_error_faq.log -u p0rn -p master -P 2221 -z -R "127.0.0.1" "/XXX/" {}

### ncftpput same but no find, use -a for file-list.txt
xargs -a todoup.txt -i -n 1 -P 3 ./nc/bin/ncftpput -e nc_error.log -u anonymous -p anonymous -P 21 -z -R REMOTEHOST "/REMOTEFOLDER/" "{}"
#### ncftpput ^ todo.txt sampel:
"./html/"
"./Dokumente/"
"./Downloads/"

## ncftpput datein suchen und auf ul.to uppen
find ../../home/Wii/ -name "*.rar" -exec ./ncftpput -e error.log -u 123789 -p pass123 -P 21 ftp.uploaded.net "/" {} \; > /dev/null &

### ncftpls ncftpget xargs multi downloader
../nc/bin/ncftpls -1 "ftp://USERPASSHOSTPORT/XXX/" | xargs -i -n 1 -P 3 ../nc/bin/ncftpget -R "ftp://USERPASSHOSTPORT/XXX/{}" > /dev/null &

## ftp curl upload
curl -T backup.sql.gz -u anonymous:anonymous ftp://127.0.0.1/bin/.log/
```
