# kurento-media-server-6.0-deb
Offline deb package of kurento-media-server-6.0

## MACHINE WITH INTERNET CONNECTION

**requirements**
apt-rdepends : sudo apt-get install apt-rdepends

1) Update and Upgrade your machine

`sudo apt-get update && sudo apt-get upgrade`

2) Create a bash script "kms-repo.sh" 

```javascript
# Add the Kurento Packages Repository
# For Ubuntu 14.04 (Trusty), use "trusty-dev" for "development" repo
# For Ubuntu 16.04 (Xenial) , use "xenial" or "xenial-dev" 
REPO="trusty"  
tee /etc/apt/sources.list.d/kurento-${REPO}.list > /dev/null <<EOF
# Kurento Packages repository
deb http://ubuntu.kurento.org ${REPO} kms6
EOF
wget http://ubuntu.kurento.org/kurento.gpg.key -O - | apt-key add -
apt-get update
```

3) Create a bash script "kms-depends.sh"

```javascript
PACKAGE="kurento-media-server-6.0"
DEPENDS=$(apt-rdepends "$PACKAGE" 2>/dev/null | grep -v '^ ') 
mkdir kms-debs; cd kms-debs
for D in $DEPENDS; do
  apt-get download "$D"
done
```
4) Change file permissions
`sudo chmod +x kms-repo.sh && sudo chmod +x kms-depends.sh`

5) Run the scripts

First 
`sudo ./kms-repo.sh`

When finished 
`sudo ./kms-depends.sh`


6) Copy all \*.deb in the folder kms-debs and transfer to you offline machine

## MACHINE WITHOUT INTERNET CONNECTION

7) Install all deb files.

`cd kms-debs
sudo dpkg -i *.deb
`

thanks to [@j1elo](https://github.com/j1elo) to help me [on this!](https://mail.google.com/mail/u/0/#inbox/15d3bdb0ea160b5e)
