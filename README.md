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

## wget
### wget spider
```sh
wget -r -nd --spider -o links.txt -np --post-data="username=admin&password=password&Login=Login" --keep-session-cookies http://localhost/vuln_test/DVWA/login.php
wget -r --spider -o links.txt http://www.kultur-cottbus.de/
cat links.txt |grep -o -E "(http[s]?://.*)\n" > spider.txt
cat links.txt |grep -o -P "http[s]?://[^ \r\n]+" > spider.txt
```
### wget download online greping ftp filez and multithreading
```sh
wget --no-remove-listing "ftp://saug:mich@localhost:2222/REQUEST/"
awk '{print $NF}' .listing |td -d "\r" |grep "EUR" > .downloading
xargs -a .downloading -i -n 1 -P 2 wget -c -r "ftp://saug:mich@localhost:2222/REQUEST/{}"
```
### singel liner oneliner
```sh
wget --no-remove-listing "ftp://localhost/" |awk '{print $NF}' .listing |td -d "\r" |xargs -P4 -i proxychains wget -nH -nd -r -c "ftp://localhost/"
```
