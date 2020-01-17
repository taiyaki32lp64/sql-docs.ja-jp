3. すべてのクラスター ノードで、Pacemaker のファイアウォール ポートを開きます。 `firewalld` を使用してこれらのポートを開くには、次のコマンドを実行します。

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > ファイアウォールに高可用性構成が組み込まれていない場合、Pacemaker 用に次のポートを開きます。
   >
   > * TCP: ポート 2224、3121、21064
   > * UDP: ポート 5405

1. すべてのノードに Pacemaker パッケージをインストールします。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

2. Pacemaker と Corosync のパッケージをインストールしたときに作成された既定のユーザー用のパスワードを設定します。 すべてのノードで同じパスワードを使います。 

   ```bash
   sudo passwd hacluster
   ```

3. 再起動後にノードがクラスターに再度参加できるように、`pcsd` サービスと Pacemaker を有効にして開始します。 すべてのノードで次のコマンドを実行します。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. クラスターを作成します。 クラスターを作成するには、次のコマンドを実行します。

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >前に同じノードでクラスターを構成した場合は、`pcs cluster setup` を実行するときに `--force` オプションを使用する必要があります。 このオプションは、`pcs cluster destroy` を実行するのと同等です。 Pacemaker を再度有効にするために、`sudo systemctl enable pacemaker` を実行します。

5. SQL Server の SQL Server リソース エージェントをインストールします。 すべてのノードで次のコマンドを実行します。 

   ```bash
   sudo yum install mssql-server-ha
   ```
