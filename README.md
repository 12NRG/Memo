# How to Save past GNU screen output to a file

```
One way to do it is to use copy mode to copy the entire scrollback history, then dump it into a file. (There is likely a better way.)

With default keybindings, this would be something like:
```
- Ctrl-A to send screen a command
- [ to enter copy mode
- g to go to the top
- Space bar to mark the beginning of the scrollback buffer (where you are) as the start of the text to be copied
- G to go to the end
- Enter to mark the end of the text to be copied, and copy it.
- Then open up vim, run :set paste to avoid issues with e.g. auto-indentation, and then use Ctrl-A ] to paste.

# dhclient could not discover the server due to some reason: How to check

The "dhclient dhcpdiscover no such device" error means dhclient can't find or bind to the network interface you specified for DHCP discovery. To fix it, verify the network interface name is correct and you have root/sudo privileges, then check for a problematic lease file in /var/lib/dhcp or a long device name that dhclient may not handle well. 
Troubleshooting Steps
1. Check Interface Name:
- Confirm the network interface (e.g., eth0, wlan0) you provided to dhclient is correct for your system. 
- Use commands like ip a or ifconfig to list available network interfaces and find the correct name. 
2. Run with sudo:
- Ensure you are running the dhclient command with root privileges using sudo, as it requires elevated permissions to manage network interfaces. 
3. Remove Lease Files:
- Delete any old or corrupt .leases files in /var/lib/dhcp/. 
- Restart the dhclient or your network service, as these files can sometimes cause conflicts or hold onto incorrect configurations. 
4. Check for Long Device Names:
- In some cases, very long network interface names (e.g., for a wireless adapter) can cause issues with dhclient. 
- Check your system's network interface names to see if any are unusually long and investigate if this could be the cause. 
5. Consider Multiple Interfaces or Configuration:
- If you have multiple network interfaces, ensure dhclient is not incorrectly trying to configure the wrong one. 
- Review your /etc/dhcp/dhclient.conf file for any specific interface configurations that might be misdirecting the client. 
6. Check Network Settings:
- If using a desktop environment, try disabling and re-enabling the network connection via the system tray. 
- If the issue persists, consider resetting network settings to their defaults, which can help resolve underlying configuration issues.

# How to check the device
Linuxでネットワークデバイスを再認識させるには、まずデバイスが認識されているかを確認し、認識されていない場合は、デバイスドライバ（モジュール）を再読み込みするなどの方法があります。﻿
1. デバイスの認識状態を確認する
まず、ネットワークデバイスがシステムに認識されているかどうかを確認します。﻿
ip a または ifconfig コマンドを使用する。
ip a は現在のネットワークインターフェースの情報を表示します。
ifconfig はネットワークインターフェースの動作状況や設定を表示します。
表示された一覧に、eth0 や enpXsY といった名前のデバイスがあれば、認識されています。
2. デバイスの再認識を試みる
デバイスが認識されていない場合、以下の手順で再認識を試みることができます。
ネットワークデバイスの再接続（物理的な操作）
USB接続のネットワークアダプタであれば、一度抜き差しして再接続します。﻿
有線LANの場合は、一度ケーブルを抜き差ししてみます。﻿
ネットワークインターフェースの再起動
ip link set dev <インターフェース名> down コマンドでインターフェースを停止し、ip link set dev <インターフェース名> up で再起動します。﻿
例: ip link set dev eth0 down、ip link set dev eth0 up。﻿
udevルールの再生成（自動再認識）
udevadm control --reload-rules と udevadm trigger コマンドを実行して、udevルールを再ロードし、デバイスの検出をトリガーします。﻿
ネットワークマネージャーの再起動
systemctl restart NetworkManager コマンドで、システムでネットワークサービスを管理しているNetworkManagerを再起動します。﻿
モジュールの再読み込み
ネットワークドライバのモジュールが正しくロードされていない場合、一度アンロードしてから再度ロードし直すことで認識されることがあります。﻿
lsmod コマンドでロードされているモジュールを確認し、rmmod <モジュール名> でアンロード、modprobe <モジュール名> で再度ロードします。﻿

