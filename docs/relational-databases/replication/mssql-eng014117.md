---
title: MSSQL_ENG014117 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014117 error
ms.assetid: e5906a76-9511-4c47-8826-8c765b58a39d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 2d6a7318c8d45da6c6c029dcacc315fdd1b36460
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809963"
---
# <a name="mssql_eng014117"></a>MSSQL_ENG014117
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14117|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|'%s' はディストリビューション データベースとして構成されていません。|  
  
## <a name="explanation"></a>説明  
 このエラーは、次のいずれかまたは両方に該当する場合に発生する可能性があります。  
  
-   指定したディストリビューション データベースのエントリが、 **msdb..MSdistributiondbs**に存在しない場合。  
  
-   **master** データベース内にローカル サーバーのエントリがない場合、またはエントリは存在するが正しくない場合。  
  
     レプリケーションでは、コンピューター名とオプションのインスタンス名 (クラスター化されたインスタンスの場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仮想サーバー名とオプションのインスタンス名) を使用して、トポロジのすべてのサーバーを登録する必要があります。 レプリケーションが正しく機能するためには、トポロジの各サーバーに対して `SELECT @@SERVERNAME` によって返された値が、コンピューター名または仮想サーバー名と、オプションのインスタンス名で一致している必要があります。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのいずれかを IP アドレスまたは完全修飾ドメイン名 (FQDN) で登録している場合、レプリケーションはサポートされません。 レプリケーションの構成時に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内に IP アドレスまたは FQDN で登録された [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] インスタンスがあった場合、このエラーが発生する可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 ディストリビューター インスタンスが正しく登録されているかどうかを確認します。 コンピューターのネットワーク名と SQL Server インスタンスの名前が異なる場合は、次のいずれかを実行してください。  
  
-   SQL Server インスタンス名を有効なネットワーク名として追加します。 代替ネットワーク名を設定する 1 つの方法は、その名前をローカル ホスト ファイルに追加することです。 ローカル ホスト ファイルは、既定では、WINDOWS\system32\drivers\etc または WINNT\system32\drivers\etc にあります。詳細については、Windows のマニュアルを参照してください。  
  
     たとえば、コンピューター名が comp1、そのコンピューターの IP アドレスが 10.193.17.129、インスタンス名が inst1/instname の場合、ホスト ファイルに次のエントリを追加します。  
  
     10.193.17.129 inst1  
  
-   ディストリビューションを無効化し、インスタンスを登録して、ディストリビューションを再設定してください。 @@SERVERNAME の値が、クラスター化されていないインスタンスに対して適切でない場合は、次の手順を実行してください。  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) ストアド プロシージャを実行したら、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを再起動し、@@SERVERNAME への変更を有効にする必要があります。  
  
     @@SERVERNAME の値がクラスター化されたインスタンスに対して適切でない場合は、クラスター アドミニストレーターを使用して名前を変更する必要があります。 詳細については、「[Always On フェールオーバー クラスター インスタンス (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
 ディストリビューター インスタンスが正しく登録されていることを確認したら、ディストリビューション データベースが **msdb..MSdistributiondbs**の一覧に表示されているかどうかを確認します。 表示されていない場合は、次の手順を実行します。  
  
1.  ディストリビューション構成のスクリプトを作成します。 詳細については、「 [Scripting Replication](../../relational-databases/replication/scripting-replication.md)」を参照してください。  
  
2.  ディストリビューションを無効化してから、再度有効化します。 詳しくは、「 [Configure Distribution](../../relational-databases/replication/configure-distribution.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
