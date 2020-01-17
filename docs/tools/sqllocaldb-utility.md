---
title: SqlLocalDB Utility |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- SqlLocalDB utility [SQL Server]
- local database runtime utility
- LocalDB, SqlLocalDB Utility
ms.assetid: d785cdb7-1ea0-4871-bde9-1ae7881190f5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 78358b6477208dcb7aecb4c031ee25318eab9e05
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065462"
---
# <a name="sqllocaldb-utility"></a>SqlLocalDB ユーティリティ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssExpCurrent](../includes/ssexpcurrent-md.md)] **LocalDB** のインスタンスを作成するには、**SqlLocalDB** ユーティリティを使用します。 **SqlLocalDB** ユーティリティ (SqlLocalDB.exe) は、ユーザーおよび開発者が [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB** のインスタンスを作成および管理できるようにするシンプルなコマンド ライン ツールです。 **LocalDB**の使用方法の詳細については、「 [SQL Server 2016 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
SqlLocalDB.exe   
{  
      [ create   | c ] \<instance-name>  \<instance-version> [-s ]  
    | [ delete   | d ] \<instance-name>  
    | [ start    | s ] \<instance-name>  
    | [ stop     | p ] \<instance-name>  [ -i ] [ -k ]  
    | [ share    | h ] [" <user_SID> " | " <user_account> " ] " \<private-name> " " \<shared-name> "  
    | [ unshare  | u ] " \<shared-name> "  
    | [ info     | i ] \<instance-name>  
    | [ versions | v ]  
    | [ trace    | t ] [ on | off ]  
    | [ help     | -? ]  
}  
```  
  
## <a name="arguments"></a>引数  
 [ **create** | **c** ] *\<instance-name>* *\<instance-version>* **[-s]**  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB** の新しいインスタンスを作成します。 **SqlLocalDB** では、 *\<instance-version>* 引数で指定された [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] バイナリのバージョンを使用します。 バージョン番号は、1 桁以上の 10 進数の数値書式で指定します。 マイナー バージョン番号 (サービス パック) は省略可能です。 たとえば、11.0 と 11.0.1186 という 2 つのバージョン番号のどちらも使用できます。 指定したバージョンがコンピューターにインストールされている必要があります。 指定しなかった場合、バージョン番号は既定で **SqlLocalDB** ユーティリティのバージョンに設定されます。 **-s** を追加した場合、**LocalDB** の新しいインスタンスが起動します。  
  
 [ **share** | **h** ]  
 指定された共有名を使用して、 **LocalDB** の指定されたプライベート インスタンスを共有します。 ユーザー SID またはアカウント名を省略した場合、既定で現在のユーザーになります。  
  
 [ **unshared** | **u** ]  
 **LocalDB**の指定した共有インスタンスの共有を停止します。  
  
 [ **delete** | **d** ] *\<instance-name>*  
 指定した [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB** のインスタンスを削除します。  
  
 [ **start** | **s** ] " *\<instance-name>* "  
 指定した [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB** のインスタンスを起動します。 成功した場合、ステートメントから **LocalDB**の名前付きパイプ アドレスが返されます。  
  
 [ **stop** | **p** ] *\<instance-name>* **[-i]** **[-k]**  
 指定した [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB** のインスタンスを停止します。 **-i** を追加した場合、**NOWAIT** オプション付きでインスタンスのシャットダウンを要求します。 **-k** を追加した場合は、インスタンス プロセスに通知することなく、そのプロセスを停止します。  
  
 [ **info** | **i** ] [ *\<instance-name>* ]  
 現在のユーザーが所有する [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB** のすべてのインスタンスを一覧表示します。  
  
 *\<instance-name>* を指定すると、[!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** の指定したインスタンスの名前、バージョン、状態 (Running または Stopped)、および最後の起動時刻に加え、**LocalDB** のローカル パイプ名が返されます。  
  
 [ **trace** | **t** ] **on** | **off**  
 **trace on** を指定すると、現在のユーザーに対して **SqlLocalDB** の API 呼び出しのトレースが有効になります。 **trace off** はトレースを無効にします。  
  
 **-?**  
 各 **SqlLocalDB** オプションの簡単な説明が返されます。  
  
## <a name="remarks"></a>Remarks  
 引数 *instance name* は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別子のルールに従っているか、二重引用符で囲む必要があります。  
  
 引数を指定せずに SqlLocalDB を実行すると、ヘルプ テキストが返されます。  
  
 start 以外の操作は、現在ログインしているユーザーに属するインスタンスでのみ実行できます。 SQLLOCALDB インスタンスを共有している場合、そのインスタンスの開始と停止は所有者のみが実行できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-an-instance-of-localdb"></a>A. LocalDB のインスタンスを作成する  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] バイナリを使用して `DEPARTMENT` という名前の [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB** のインスタンスを作成し、そのインスタンスを起動する例を次に示します。  
  
```  
SqlLocalDB.exe create "DEPARTMENT" 12.0 -s  
```  
  
### <a name="b-working-with-a-shared-instance-of-localdb"></a>B. LocalDB の共有インスタンスを操作する  
 管理者権限を使用してコマンド プロンプトを開きます。  
  
```  
SqlLocalDB.exe create "DeptLocalDB"  
SqlLocalDB.exe share "DeptLocalDB" "DeptSharedLocalDB"  
SqlLocalDB.exe start "DeptLocalDB"  
SqlLocalDB.exe info "DeptLocalDB"  
REM The previous statement outputs the Instance pipe name for the next step  
sqlcmd -S np:\\.\pipe\LOCALDB#<use your pipe name>\tsql\query  
CREATE LOGIN NewLogin WITH PASSWORD = 'Passw0rd!!@52';   
GO  
CREATE USER NewLogin;  
GO  
EXIT  
```  
  
 次のコードを実行して、 **ログインを使用して、** LocalDB `NewLogin` の共有インスタンスに接続します。  
  
```  
sqlcmd -S (localdb)\.\DeptSharedLocalDB -U NewLogin -P Passw0rd!!@52  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server 2016 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
[コマンド ライン管理ツール: SqlLocalDB.exe](../relational-databases/express-localdb-instance-apis/command-line-management-tool-sqllocaldb-exe.md)  
  
