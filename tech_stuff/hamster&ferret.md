# Hack with Hamster & Ferret



```bash
wget http://www.erratasec.com/erratasec.zip
unzip erratasec.zip
cp -R ferret/ /pentest/exploits/ && cp -R hamster/ /pentest/exploits/
cd /pentest/exploits/hamster/build/gcc4/ && make
cd /pentest/exploits/ferret/build/gcc4/ && make
cp /pentest/exploits/ferret/bin/ferret /pentest/exploits/hamster/bin
cd /pentest/exploits/hamster/bin/ && ./hamster
# Start Firefox
# Edit -> Preferences
# Advanced Tab -> Network Tab
# Click on Settings
# Select Manual proxy configuration
# Set the HTTP Proxy: 127.0.0.1 on Port: 1234
# Tick Use this proxy server for all protocols and click ok
```



