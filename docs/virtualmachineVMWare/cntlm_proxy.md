---
layout: default
title: Proxy Authentication
parent: Virtual Machine - VMWare
nav_order: 7
---

# Tunnel through the Corporate Proxy

To make the VM function when both on and off the corporate network network, we will now create a set of functions to enable and disable CNTLM.

Instructions:
1. Edit your '/etc/profile.d/proxy.sh' file.
2. Paste in the below text at the bottom of the file;

>     function proxy() {
>      if [[ -z "${1// }" ]]; then
>       ___print_proxy_usage
>      else
>       case "$1" in
>        on) ___proxy_on ;;
>        off) ___proxy_off ;;
>        status) ___proxy_status ;;
>       esac
>      fi
>     }
>
>     function ___proxy_on() {
>      sudo sed -i -e'/^NoProxy/d' /etc/cntlm.conf
>      sudo sed -i -e'/^Proxy/a NoProxy  localhost, 127.0.0.*, 10.*, 192.168.*' /etc/cntlm.conf
>      ___cntlmRestart
>      echo -e "${GREEN}The proxy is currently set :-${NC}"
>      sudo cat /etc/cntlm.conf | grep NoProxy
>     }
>
>     function ___proxy_off() {
>      sudo sed -i -e'/^NoProxy/d' /etc/cntlm.conf
>      sudo sed -i -e '/^Proxy/a NoProxy  *' /etc/cntlm.conf
>      ___cntlmRestart
>      echo -e "${GREEN}The proxy is currently set :-${NC}"
>      sudo cat /etc/cntlm.conf | grep NoProxy
>     }
>
>     function ___proxy_status() {
>      sudo cat /etc/cntlm.conf | grep NoProxy
>     }
>
>     function ___cntlmRestart() {
>      sudo service cntlm restart &> /dev/null
>     }
>
>     function ___print_proxy_usage() {
>      echo -e "${GREEN}Usage:"
>      echo -e "${CYAN}  proxy on: ${GREEN} turns on the previously defined proxy."
>      echo -e "${CYAN}  proxy off: ${GREEN} turns off the previously defined proxy."
>      echo -e "${CYAN}  proxy status: ${GREEN} prints the proxy status."
>     }

4. Save and then execute the file - '. /etc/profile.d/proxy.sh'.


Run 'proxy on' if working on URA or in the Office.
Run 'proxy off' if working on an unrestricted network.
Run 'proxy status' to find out the current setting.

5. Ensure the proxy is on, and then update the OS by running 'sudo yum update -y'.