---
title: rskeymgmt ユーティリティ (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- joining report server instances [SQL Server]
- report server scale-out deployments [Reporting Services]
- cryptography [Reporting Services]
- multiple report server instances
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], scale-out deployments
- encryption [Reporting Services]
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 53f1318d-bd2d-4c08-b19f-c8b698b5b3d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c9b5ca361cbfb5de42341fad8625f10d7ce3c2fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099808"
---
# <a name="rskeymgmt-utility-ssrs"></a>rskeymgmt ユーティリティ (SSRS)
  重要なレポート サーバー データを不正アクセスから保護するための対称キーを、抽出、復元、作成、および削除します。 また、このユーティリティは、レポート サーバー インスタンスをスケール アウト配置に追加する場合にも使用されます。 *レポート サーバーのスケール アウト配置* とは、複数のレポート サーバー インスタンスが 1 つのレポート サーバー データベースを共有する状態を表しています。  
  
## <a name="syntax"></a>構文  
  
```  
  
      rskeymgmt {-?}  
{-eextract}  
{-aapply}  
{-ddeleteall}  
{-srecreatekey}  
{-rremoveinstancekey}  
{-jjoinfarm}  
{-iinstance}  
{-ffile}  
{-pencryptionpassword}  
{-mremotecomputer}  
{-ninstancenameofremotecomputer}  
{-uadministratoruseraccount}  
{-vadministratorpassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>引数  
 **-?**  
 **rskeymgmt** の引数の構文を表示します。  
  
 **-e**  
 レポート サーバー インスタンスのデータを暗号化したり、暗号化の解除を行うための対称キーを抽出します。このキーにより、ファイルへのデータのコピーが可能になります。  
  
 この引数は値を取りません。 ただし、抽出を完了するには、コマンド ラインに他の引数を追加する必要があります。 指定する必要のある引数は、`-f` および `-p` です。  
  
 **-a**  
 既存の対称キーを、パスワードで保護されたバックアップ ファイル内に作成したコピーと置き換えます。 対称キーのすべてのインスタンスが更新されます。  
  
 この引数は値を取りません。 ただし、適用するキーを含むファイルを選択するには、コマンド ラインに他の引数を追加する必要があります。 指定できる引数は、`-f` および `-p` です。  
  
 **-d**  
 レポート サーバー データベース内にある、すべての対称キー インスタンスと暗号化されたデータを削除します。 この引数は値を取りません。  
  
 `-s`  
 新規の対称キーを生成し、この新規のキーを使用してすべての暗号化された内容を再暗号化します。 対称キーのすべてのインスタンスが再生成されます。  
  
 `-j`  
 リモート レポート サーバー インスタンスが、ローカル レポート サーバー インスタンスによって使用されるレポート サーバー データベースを共有するように構成します。  
  
 **-r**  *installationID*  
 特定のレポート サーバー インスタンスに対する対称キー情報を削除します。これにより、レポート サーバーはスケールアウト配置から削除されます。 *installationID* は、RSReportserver.config ファイルにある GUID 値です。  
  
 `-f`  *ファイル*  
 対称キーのバックアップ コピーが格納されるファイルへの完全修飾パスを指定します。  
  
 **rskeymgmt -e**を使用すると、対称キーは指定したファイルに書き込まれます。  
  
 **rskeymgmt -a**を使用すると、ファイルに格納された対称キーの値がレポート サーバー インスタンスに適用されます。  
  
 `-p`  *パスワード*  
 (`-f` を使用する場合は必須) 対称キーのバックアップや適用に使用されるパスワードを指定します。 この値は空にできません。  
  
 `-i`  
 ローカル レポート サーバー インスタンスを指定します。 レポート サーバーを既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにインストールした場合、この引数は省略できます (`-i` の既定値は MSSQLSERVER)。 レポート サーバーを名前付きインスタンスとしてインストールした場合は、`-i` は必須です。  
  
 `-m`  
 レポート サーバー インスタンスをレポート サーバーのスケール アウト配置に追加する場合、このレポート サーバー インスタンスをホストするリモート コンピューターの名前を指定します。 ネットワーク上で識別されるコンピューターの名前を使用します。  
  
 `-n`  
 リモート コンピューター上のレポート サーバー インスタンスの名前を指定します。 レポート サーバーを既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにインストールした場合、この引数は省略できます (`-n` の既定値は MSSQLSERVER)。 レポート サーバーを名前付きインスタンスとしてインストールした場合は、`-n` は必須です。  
  
 `-u`  *ユーザーアキュン*  
 スケールアウト配置に追加するリモート コンピューター上の管理者アカウントを指定します。 アカウントが指定されない場合は、現在のユーザーの資格情報が使用されます。  
  
 `-v`  *パスワード*  
 (`-u` を使用する場合は必須) スケールアウト配置に追加するリモート コンピューター上の管理者アカウントのパスワードを指定します。  
  
 **-t**  *trace*  
 エラー メッセージをトレース ログに出力します。 この引数は値を取りません。 詳細については、「 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 このツールを実行するには、ローカル管理者であることが必要です。また、このツールは、レポート サーバーをホストするコンピューター上でローカルに実行する必要があります。 rskeymgmt ユーティリティは、ローカルのレポート サーバー Windows インスタンスと連動します (このユーティリティはレポート サーバー Windows サービスのリモート インスタンスに接続できないので、このユーティリティを使用してリモート レポート サーバー インスタンスの暗号化キーを管理することはできません)。  
  
> [!NOTE]  
>  `-u` 引数と `-v` 引数を使用する場合、リモート コンピューターに対する管理者権限を持つアカウントを指定する必要があります。  
  
## <a name="examples"></a>使用例  
 次の例は、 **rskeymgmt**の使用方法を示しています。 これらの例では、暗号化キーの抽出、復元、削除の実行、およびレポート サーバーのスケールアウト配置の構成を行います。  
  
#### <a name="extracting-encryption-keys"></a>暗号化キーの抽出  
 次の例では、暗号化キーのバックアップ コピーを作成し、そのコピーをパスワードで保護されたファイルとしてフロッピー ディスク上に保存します。 レポート サーバーが名前付きインスタンスとしてインストールされている場合は、`-i` 引数を追加します。  
  
```  
rskeymgmt -e -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="restoring-encryption-keys"></a>暗号化キーの復元  
 次の例では、暗号化キーを置き換えます。 キーのバックアップ コピーの場所およびファイルのロックを解除するパスワードを指定する必要があります。  
  
```  
rskeymgmt -a -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="deleting-encryption-keys-and-encrypted-content"></a>暗号化キーおよび暗号化された内容の削除  
 次の例では、レポート サーバーに格納されたすべての暗号化キーを削除します。 インストール環境がレポート サーバーのスケール アウト配置になっている場合は、この配置に含まれているすべてのレポート サーバー インスタンスに対する暗号化キーが削除されます。 また、暗号化キーを削除すると、レポート サーバー データベースにある既存の暗号化された値はすべて削除されます。 暗号化されたコンテンツの詳細については、「[暗号化されたレポート サーバー データの格納 (SSRS 構成マネージャー)](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)」を参照してください。  
  
```  
rskeymgmt -d  
```  
  
#### <a name="joining-a-remote-report-server-named-instance-to-a-scale-out-deployment"></a>スケール アウト配置へのリモート レポート サーバー名前付きインスタンスの追加  
 次の例では、リモート コンピューターにインストールされたレポート サーバー インスタンスを、レポート サーバーのスケール アウト配置に追加します。 このコマンドは、共有データベースの使用が既に構成されているコンピューターのいずれかで実行する必要があります。 このコマンドの引数には、スケール アウト配置に追加するリモート レポート サーバー インスタンスを指定します。  
  
```  
rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
```  
  
> [!NOTE]  
>  レポート サーバーのスケール アウト配置とは、複数のレポート サーバー インスタンスが同じレポート サーバー データベースを共有する配置モデルのことです。 対称キーをデータベースに格納するレポート サーバー インスタンスであれば、レポート サーバー データベースを使用することができます。 たとえば、レポート サーバー データベースが 3 つのレポート サーバー インスタンスに対するキー情報を含んでいる場合、3 つすべてのインスタンスは、同じスケール アウト配置のメンバーと見なされます。  
  
#### <a name="joining-report-server-instances-on-the-same-computer"></a>同じコンピューター上の複数のレポート サーバー インスタンスの追加  
 同じコンピューターにインストールされている複数のレポート サーバー インスタンスから、スケール アウト配置を作成できます。 ローカルにインストールされているレポート サーバー インスタンスを追加する場合、`-u` および `-v` 引数は設定しないでください。 `-u` および `-v` 引数は、リモート コンピューターからインスタンスを追加する場合にのみ使用します。 引数を指定する場合は、次のエラーが表示されます。「ユーザーの資格情報は、ローカル接続に使用することはできません」。  
  
 次の例は、複数のローカル インスタンスを使用してスケール アウト配置を作成する構文です。 この例で <`initializedinstance`> に、レポート サーバー データベースを使用して、既に初期化されているインスタンスの名前を指定し、<`newinstance`> 展開に追加するインスタンスの名前を指定します。  
  
```  
rskeymgmt -j -i <initializedinstance> -m <computer name> -n <newinstance>  
```  
  
#### <a name="removing-encryption-keys-for-a-single-report-server-in-a-scale-out-deployment"></a>スケール アウト配置に含まれる 1 つのレポート サーバーに対する暗号化キーの削除  
 次の例では、レポート サーバーのスケール アウト配置に含まれている 1 つのレポート サーバーに対する暗号化キーを削除します。 これらのキーは、レポート サーバー データベースから削除されます。 レポート サーバー インスタンスに対するキーが削除されると、そのレポート サーバー インスタンスはデータベース内の暗号化されたデータにはアクセスできなくなるため、スケール アウト配置からの削除が効率的に行われます。  
  
 レポート サーバー インスタンスをスケールアウト配置から削除するには、インストール ID を指定する必要があります。 インストール ID とは、暗号化キーを削除するレポート サーバー インスタンスの RSReportserver.config ファイルに格納されている GUID のことです。 スケール アウト配置から削除するコンピューター上で次のコマンドを実行する必要があります。 レポート サーバーが名前付きインスタンスとしてインストールされている場合は、`-i` 引数を使用してインスタンスを指定します。 詳しくは、「 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)」をご覧ください。  
  
```  
rskeymgmt -r <installationID>  
```  
  
## <a name="file-location"></a>ファイルの場所  
 Rskeymgmt.exe is は、**\<*ドライブ*>:\Program Files\Microsoft SQL Server\110\Tools\Binn** または **\<*ドライブ*>:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn** にあります。 このユーティリティは、ファイル システム上の任意のフォルダーから実行できます。  
  
## <a name="remarks"></a>コメント  
 レポート サーバーは、格納された資格情報および接続情報を暗号化します。 データの暗号化には、公開キーおよび対称キーが使用されます。 レポート サーバーを実行するには、レポート サーバー データベースに有効なキーが含まれている必要があります。 キーのバックアップ、削除、復元を行うには **rskeymgmt** を使用します。 このツールには、キーを復元できない場合に、使用できなくなった暗号化されたコンテンツを削除する方法が用意されています。  
  
 セットアップや初期化の際に定義されるキーのセットを管理するには、 **rskeymgmt** ユーティリティを使用します。 このユーティリティは、リモート プロシージャ呼び出し (RPC) エンドポイントを介して、ローカルのレポート サーバー Windows サービスに接続されます。 このユーティリティが動作するには、レポート サーバー Windows サービスが実行されている必要があります。  
  
 暗号化キーの詳細については、「[暗号化キーの構成と管理 (SSRS 構成マネージャー)](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」および「[レポート サーバーの初期化 (SSRS 構成マネージャー)](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ネイティブ モード レポート サーバーのスケールアウト配置の構成 (SSRS 構成マネージャー)](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](../report-server/reporting-services-report-server-native-mode.md)   
 [レポート サーバーのコマンド プロンプト ユーティリティ (SSRS)](report-server-command-prompt-utilities-ssrs.md)   
 [暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
