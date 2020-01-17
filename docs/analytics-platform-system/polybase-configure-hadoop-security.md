---
title: PolyBase Hadoop のセキュリティを構成する
description: Parallel Data Warehouse で PolyBase を構成して外部 Hadoop に接続する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/26/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f275c77556e8abe8932e241075b9e24e2ae5db77
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400653"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>PolyBase の構成と Hadoop 用のセキュリティ

この記事では、Hadoop への APS PolyBase 接続に影響するさまざまな構成設定について説明します。 PolyBase の概要については、「 [polybase とは](configure-polybase-connectivity-to-external-data.md)」を参照してください。

> [!NOTE]
> AP では、すべてのコンピューティングノードと制御ノードで XML ファイルの変更が必要になります。
> 
> APS で XML ファイルを変更するときは、特別な注意が必要です。 タグまたは不要な文字があると、xml ファイルが無効になり、機能の usablが低下する可能性があります。
> Hadoop 構成ファイルは次のパスにあります。  
> ```  
> C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf 
> ``` 
> Xml ファイルを変更する場合は、サービスを再起動して有効にする必要があります。

## <a id="rpcprotection"></a>Hadoop. RPC 保護の設定

Hadoop クラスターで通信を保護する一般的な方法は、hadoop.rpc.protection 構成を "Privacy" または "Integrity" に変更することです。 既定では、PolyBase は構成が "Authenticate" に設定されているものと想定します。 この既定値をオーバーライドするには、次のプロパティを core-site.xml ファイルに追加します。 この構成を変更すると、Hadoop ノード間の安全なデータ転送と、SQL Server への SSL 接続が有効になります。

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

## <a id="kerberossettings"></a>Kerberos の構成  

PolyBase が Kerberos でセキュリティが強化されているクラスターに対して認証を行う場合、hadoop.rpc.protection が既定で "Authenticate" に設定されている必要があることに注意してください。 これにより、Hadoop ノード間のデータ通信が暗号化されなくなります。 hadoop.rpc.protection の "Privacy" または "Integrity" 設定を使用するには、PolyBase サーバーで core-site.xml ファイルを更新します。 詳細については、前のセクションの「[Hadoop.RPC.Protection 設定での Hadoop クラスターへの接続](#rpcprotection)」を参照してください。

MIT KDC を使用して Kerberos で保護された Hadoop クラスターに接続するには、すべての APS 計算ノードと制御ノードで次の変更が必要です。

1. APS のインストールパスで Hadoop 構成ディレクトリを検索します。 通常、このパスは次のとおりです。  

   ```  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf  
   ```  

2. 次の表に示す構成キーの Hadoop 側の構成値を検索します (Hadoop コンピューター上の Hadoop 構成ディレクトリ内でファイルを検索します)。  
   
3. これらの構成値を、SQL Server コンピューター上の対応するファイル内の値プロパティにコピーします。  
   
   |**#**|**［構成ファイル］**|**構成キー**|**処置**|  
   |------------|----------------|---------------------|----------|   
   |1 で保護されたプロセスとして起動されました|core-site.xml|polybase.kerberos.kdchost|KDC のホスト名を指定します。 例: kerberos.your-realm.com.|  
   |2|core-site.xml|polybase.kerberos.realm|Kerberos 領域を指定します。 例: YOUR-REALM.COM|  
   |3|core-site.xml|hadoop.security.authentication|Hadoop 側の構成を検出して SQL Server コンピューターにコピーします。 例: KERBEROS<br></br>**セキュリティに関する注意:** KERBEROS は大文字で記述する必要があります。 小文字の場合、機能しない可能性があります。|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Hadoop 側の構成を検出して SQL Server コンピューターにコピーします。 たとえば次のようになります。hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|Hadoop 側の構成を検出して SQL Server コンピューターにコピーします。 たとえば次のようになります。mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|Hadoop 側の構成を検出して SQL Server コンピューターにコピーします。 例: 10.193.26.174:10020|  
   |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Hadoop 側の構成を検出して SQL Server コンピューターにコピーします。 たとえば次のようになります。yarn/_HOST@YOUR-REALM.COM|  

**core-site.xml**
```xml
<property>
  <name>polybase.kerberos.realm</name>
  <value></value>
</property>
<property>
  <name>polybase.kerberos.kdchost</name>
  <value></value>
</property>
<property>
    <name>hadoop.security.authentication</name>
    <value>KERBEROS</value>
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.namenode.kerberos.principal</name>
  <value></value> 
</property>
```

**mapred-site.xml**
```xml
<property>
  <name>mapreduce.jobhistory.principal</name>
  <value></value>
</property>
<property>
  <name>mapreduce.jobhistory.address</name>
  <value></value>
</property>
```

**yarn-site.xml**
```xml
<property>
  <name>yarn.resourcemanager.principal</name>
  <value></value>
</property>
```

4. 各 Hadoop ユーザーの認証情報を指定するデータベース スコープ資格情報オブジェクトを作成します。 「 [PolyBase T-SQL オブジェクト](../relational-databases/polybase/polybase-t-sql-objects.md)」を参照してください。

## <a id="encryptionzone"></a>Hadoop 暗号化ゾーンのセットアップ
Hadoop 暗号化ゾーンを使用している場合は、次のように core-site.xml と hdfs-site.xml を変更します。 KMS サービスが実行されている ip アドレスを、対応するポート番号を使用して指定します。 CDH の KMS の既定のポートは16000です。

**core-site.xml**
```xml
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value> 
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.encryption.key.provider.uri</name>
  <value>kms://http@<ip address>:16000/kms</value>
</property>
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value>
  </property>
```