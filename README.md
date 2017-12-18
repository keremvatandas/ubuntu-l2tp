# ubuntu-l2tp

Ubuntu L2tp Vpn Conf

```language-bash
sudo apt update
sudo apt -y install intltool libtool network-manager-dev libnm-util-dev libnm-glib-dev libnm-glib-vpn-dev libnm-gtk-dev libnm-dev libnma-dev ppp-dev libdbus-glib-1-dev libsecret-1-dev libgtk-3-dev libglib2.0-dev xl2tpd strongswan
sudo apt -y install git

git clone https://github.com/nm-l2tp/network-manager-l2tp.git
cd network-manager-l2tp
autoreconf -fi
intltoolize
./configure --disable-static --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib/x86_64-linux-gnu --libexecdir=/usr/lib/NetworkManager --localstatedir=/var --with-pppd-plugin-dir=/usr/lib/pppd/2.4.7
make
sudo make install

sudo apparmor_parser -R /etc/apparmor.d/usr.lib.ipsec.charon
sudo apparmor_parser -R /etc/apparmor.d/usr.lib.ipsec.stroke

sudo apt remove -y xl2tpd
sudo apt install -y libpcap0.8-dev

cd ~
wget https://github.com/xelerance/xl2tpd/archive/v1.3.6/xl2tpd-1.3.6.tar.gz
tar xvzf xl2tpd-1.3.6.tar.gz
cd xl2tpd-1.3.6
make
sudo make install

git clone https://github.com/nm-l2tp/network-manager-l2tp.git
cd network-manager-l2tp
autoreconf -fi
intltoolize

./configure --disable-static --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib/x86_64-linux-gnu --libexecdir=/usr/lib/NetworkManager --localstatedir=/var --with-pppd-plugin-dir=/usr/lib/pppd/2.4.7
make
sudo checkinstall
```
