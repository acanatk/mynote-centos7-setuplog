**********************************************************************
FTPサービスセットアップ
**********************************************************************

他の環境からのファイルコピーするときに使用するため、FTPサービスをセットアップします。

FTPサービスとして、vsftpdを使用します。

======================================================================
インストール
======================================================================

**vsftpd** パッケージをインストールする。

.. code-block:: bash

    $ yum install vsftpd

======================================================================
設定ファイル変更
======================================================================

/etc/vsftpd/vsftpd.confファイルの次のパラメータを変更する。

.. code-block:: text

    anonymous_enable=NO
    ascii_upload_enable=YES
    ascii_download_enable=YES
    chroot_local_user=YES
    chroot_list_enable=YES
    chroot_list_file=/etc/vsftpd/chroot_list
    ls_recurse_enable=YES
    listen=YES
    listen_ipv6=NO
    use_localtime=YES

/etc/vsftpd/chroot_listファイルを作成し、ユーザを追加する。
ここでは **foo** ユーザを追加する場合を例に記述してあります。

.. code-block:: text

    foo

======================================================================
ファイアウォール設定変更
======================================================================

FTPサービスおよびポートを許可する。

.. code-block:: bash

    $ firewall-cmd --add-service=ftp --permanent
    $ firewall-cmd --add-port=20-21/tcp --permanent
    $ firewall-cmd --reload

======================================================================
FTPサービスの起動と停止
======================================================================

FTPサービスは必要なときのみ起動するため、以下の手順で起動および停止する。

FTPサービスを起動する。

.. code-block:: bash

    $ systemctl start vsftpd

FTPサービスを停止する。

.. code-block:: bash

    $ systemctl stop vsftpd
