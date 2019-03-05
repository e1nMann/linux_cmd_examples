# linux_cmd_examples
list of usefull linux commando line examples

## index
1. system
2. wget

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
[Archive_unter_Linux_(tar,_gz,_bz2,_zip)](https://www.thomas-krenn.com/de/wiki/Archive_unter_Linux_(tar,_gz,_bz2,_zip))

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
