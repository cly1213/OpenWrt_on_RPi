# OpenVPN(with NordVPN)

```bash=
# Install packages
opkg update
opkg install luci-app-openvpn
/etc/init.d/rpcd restart

# Configuration parameters
OVPN_DIR="/etc/openvpn"
OVPN_ID="client"
OVPN_USER="USERNAME"
OVPN_PASS="PASSWORD"

# Save username/password credentials
umask go=
cat << EOF >${OVPN_DIR}/${OVPN_ID}.auth
${OVPN_USER}
${OVPN_PASS}
EOF

# Configure VPN service
sed -i -e "
/^auth-user-pass/s/^/#/
\$a auth-user-pass ${OVPN_ID}.auth
/^redirect-gateway/s/^/#/
\$a redirect-gateway def1 ipv6
" ${OVPN_DIR}/${OVPN_ID}.conf
/etc/init.d/openvpn restart

# Provide VPN instance management
ls /etc/openvpn/*.conf \
| while read -r OVPN_CONF
do
OVPN_ID="$(basename ${OVPN_CONF%.*} | sed -e "s/\W/_/g")"
uci -q delete openvpn.${OVPN_ID}
uci set openvpn.${OVPN_ID}="openvpn"
uci set openvpn.${OVPN_ID}.enabled="1"
uci set openvpn.${OVPN_ID}.config="${OVPN_CONF}"
done
uci commit openvpn
/etc/init.d/openvpn restart

# Configure firewall
uci rename firewall.@zone[0]="lan"
uci rename firewall.@zone[1]="wan"
uci del_list firewall.lan.device="tun+"
uci add_list firewall.lan.device="tun+"
uci commit firewall
/etc/init.d/firewall restart
```
