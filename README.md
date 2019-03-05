# linux_cmd_examples
list of usefull linux commando line examples

## system
update ubunut, debian, linuxmint etc...
```bash
sudo apt-get upade && sudo apt-get upgrade -y
```

## wget
### wget spider
```bash
wget -r -nd --spider -o links.txt -np --post-data="username=admin&password=password&Login=Login" --keep-session-cookies http://localhost/vuln_test/DVWA/login.php
wget -r --spider -o links.txt http://www.kultur-cottbus.de/
cat links.txt |grep -o -E "(http[s]?://.*)\n" > spider.txt
cat links.txt |grep -o -P "http[s]?://[^ \r\n]+" > spider.txt
```
