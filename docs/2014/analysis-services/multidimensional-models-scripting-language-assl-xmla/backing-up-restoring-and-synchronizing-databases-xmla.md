---
title: バックアップ、復元、およびデータベース (XMLA) の同期 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6163a538c4e8872016f7ec572e4c177cfe92de94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702276"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>データベースのバックアップ、復元、および同期 (XMLA)
  XML for Analysis には、データベースのバックアップ、復元、および同期を行う 3 つのコマンドがあります。  
  
-   [バックアップ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)コマンドでバックアップを[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベースを使用して、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]バックアップ ファイル (.abf) をセクションで説明した[データベースのバックアップ](#backing_up_databases)します。  
  
-   [復元](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)コマンドは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  セクションで説明されているデータベースを .abf ファイルから[データベースの復元](#restoring_databases)します。  
  
-   [同期](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)コマンドでは、1 つは同期[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、セクションで説明した別のデータベースのメタデータとデータでデータベース[データベースの同期](#synchronizing_databases)します。  
  
##  <a name="backing_up_databases"></a> データベースのバックアップ  
 上で述べたように、`Backup` コマンドは指定された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースをバックアップ ファイルにバックアップします。 `Backup` コマンドには、バックアップするデータベースや使用するバックアップ ファイル、セキュリティ定義のバックアップ方法、およびバックアップするリモート パーティションを指定するためのさまざまなプロパティがあります。  
  
> [!IMPORTANT]  
>  Analysis Services サービス アカウントには、各ファイルに指定されたバックアップ場所に対する書き込み権限が必要です。 また、ユーザーが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの管理者ロールを持っているか、バックアップするデータベースに対してフル コントロール (管理者) 権限を持つデータベース ロールのメンバーである必要があります。  
  
### <a name="specifying-the-database-and-backup-file"></a>データベースとバックアップ ファイルの指定  
 バックアップするデータベースを指定する設定、[オブジェクト](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)のプロパティ、`Backup`コマンド。 `Object` プロパティには、データベースを表すオブジェクト識別子を含める必要があります。含まれていない場合、エラーが発生します。  
  
 作成して、バックアップ プロセスによって使用されるファイルを指定する設定、[ファイル](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla)のプロパティ、`Backup`コマンド。 `File` プロパティは、作成するバックアップ ファイルの UNC パスとファイル名に設定する必要があります。  
  
 バックアップに使用するファイルの指定に加えて、指定したバックアップ ファイルに対する以下のオプションを設定できます。  
  
-   設定した場合、 [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla)プロパティを true に、`Backup`コマンドでは、指定したファイルが既に存在する場合、バックアップ ファイルが上書きされます。 `AllowOverwrite` プロパティを false に設定した場合、指定されたバックアップ ファイルが既に存在すると、エラーが発生します。  
  
-   設定した場合、 [ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla)ファイルを作成した後、プロパティを true に、バックアップ ファイルが圧縮されています。  
  
-   設定した場合、[パスワード](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla)任意の空白以外の値、バックアップ ファイルにプロパティが指定したパスワードを使用して暗号化します。  
  
    > [!IMPORTANT]  
    >  `ApplyCompression` および `Password` プロパティが指定されない場合、バックアップ ファイルには接続文字列に含まれるユーザー名とパスワードがクリア テキストで格納されます。 クリア テキストで格納されたデータは、取得される可能性があります。 セキュリティを強化するためには、`ApplyCompression` および `Password` 設定を使用して、バックアップの圧縮と暗号化の両方を行ってください。  
  
### <a name="backing-up-security-settings"></a>セキュリティ設定のバックアップ  
 [セキュリティ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla)プロパティを決定するかどうか、`Backup`コマンドで定義された、ロールや権限など、セキュリティ定義をバックアップ、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベース。 `Security` プロパティは、バックアップ ファイルに、セキュリティ定義のメンバーとして Windows ユーザー アカウントとグループを含めるかどうかも決定します。  
  
 `Security` プロパティの値は、次の表の一覧に示す文字列のいずれかに限定されています。  
  
|値|説明|  
|-----------|-----------------|  
|*skipMembership*|バックアップ ファイルにセキュリティ定義を含めますが、メンバーシップ情報は除外します。|  
|*CopyAll*|バックアップ ファイルにセキュリティ定義とメンバーシップ情報を含めます。|  
|*IgnoreSecurity*|バックアップ ファイルからセキュリティ定義を除外します。|  
  
### <a name="backing-up-remote-partitions"></a>リモート パーティションのバックアップ  
 リモート パーティションをバックアップする、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 、データベースを設定する、 [BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla)のプロパティ、`Backup`コマンドを true に設定します。 この設定を行うと、`Backup` コマンドは、データベースのリモート パーティションを格納するために使用するリモート バックアップ ファイルを、各リモート データ ソースに対して作成します。  
  
 バックアップする各リモート データ ソースを含めることによって、対応するバックアップ ファイルを指定することができます、[場所](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla)内の要素、[場所](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla)のプロパティ、`Backup`コマンド。 `Location`要素があります、`File`プロパティが、リモート バックアップ ファイルの UNC パスとファイル名に設定し、その[DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)データベースで定義されているプロパティが、リモート データ ソースの識別子に設定します。  
  
##  <a name="restoring_databases"></a> データベースの復元  
 `Restore` コマンドは、指定された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースをバックアップ ファイルから復元します。 `Restore` コマンドには、復元するデータベースや使用するバックアップ ファイル、セキュリティ定義の復元方法、復元するリモート パーティション、およびリレーショナル OLAP (ROLAP) オブジェクトの再配置を指定するためのさまざまなプロパティがあります。  
  
> [!IMPORTANT]  
>  バックアップ ファイルごとに、復元コマンドを実行するユーザーは、各ファイルに指定されたバックアップ場所から読み取る権限を持っている必要があります。 サーバーにインストールされていない [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを復元する場合、ユーザーは、その [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのサーバー ロールのメンバーであることも必要です。 上書きする、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データベース、ユーザーには、次のロールのいずれかが必要: サーバー ロールのメンバー、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンスまたは復元するデータベースに対してフル コントロール (管理者) 権限を持つデータベース ロールのメンバー。  
  
> [!NOTE]  
>  既存のデータベースを復元すると、データベースを復元したユーザーは、復元されたデータベースにアクセスできなくなる可能性があります。 バックアップの実行時に、ユーザーがサーバー ロールのメンバー、またはフル コントロール (管理者) 権限を持つデータベース ロールのメンバーではなかった場合、このようにアクセスできなくなることがあります。  
  
### <a name="specifying-the-database-and-backup-file"></a>データベースとバックアップ ファイルの指定  
 `DatabaseName` コマンドの `Restore` プロパティには、データベースを表すオブジェクト識別子を含める必要があります。含まれていない場合、エラーが発生します。 指定されたデータベースが既に存在する場合、既存のデータベースを上書きするかどうかは、`AllowOverwrite` プロパティによって決定されます。 `AllowOverwrite` プロパティが false に設定されている場合、指定されたデータベースが既に存在すると、エラーが発生します。  
  
 `File` コマンドの `Restore` プロパティは、指定されたデータベースに復元するバックアップ ファイルの UNC パスとファイル名に設定する必要があります。 指定されたバックアップ ファイルに対して `Password` プロパティを設定することもできます。 `Password` プロパティを空白以外の任意の値に設定すると、指定されたパスワードを使用してバックアップ ファイルが暗号化解除されます。 バックアップ ファイルが暗号化されていない場合、または指定されたパスワードがバックアップ ファイルの暗号化に使用されたパスワードと一致しない場合は、エラーが発生します。  
  
### <a name="restoring-security-settings"></a>セキュリティ設定の復元  
 `Security` プロパティは、ロールや権限などの、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースで定義されているセキュリティ定義を `Restore` コマンドが復元するかどうかを決定します。 `Security` プロパティは、`Restore` コマンドが復元プロセスの一部として、Windows ユーザー アカウントとグループをセキュリティ定義のメンバーに含めるかどうかも決定します。  
  
 この要素の値は、次の表の一覧に示す文字列のいずれかに限定されています。  
  
|値|説明|  
|-----------|-----------------|  
|*skipMembership*|データベースにセキュリティ定義を含めますが、メンバーシップ情報は除外します。|  
|*CopyAll*|データベースにセキュリティ定義とメンバーシップ情報を含めます。|  
|*IgnoreSecurity*|データベースからセキュリティ定義を除外します。|  
  
### <a name="restoring-remote-partitions"></a>リモート パーティションの復元  
 以前の `Backup` コマンドの実行時に作成された各リモート バックアップ ファイルについては、`Location` コマンドの `Locations` プロパティに `Restore` 要素を含めることによって、それに関連付けられているリモート パーティションを復元することができます。 [%Datasourcetype](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)プロパティごとに`Location`要素を除外または明示的に設定する必要があります*リモート*します。  
  
 指定された各 `Location` 要素に関して、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスは、`DataSourceID` プロパティで指定されたリモート データ ソースにアクセスし、`File` プロパティで指定されたリモート バックアップ ファイルで定義されているパーティションを復元します。 `DataSourceID` および `File` プロパティに加えて、リモート パーティションを復元するために使用される各 `Location` 要素では、以下のプロパティを使用できます。  
  
-   `DataSourceID` 要素の `ConnectionString` プロパティを別の接続文字列に設定すると、`Location` で指定されたリモート データ ソースへの接続文字列をオーバーライドできます。 その場合、`Restore` コマンドは、`ConnectionString` プロパティに含まれる接続文字列を使用します。 `ConnectionString` が指定されていない場合、`Restore` コマンドは、指定されたリモート データ ソースのバックアップ ファイルに格納されている接続文字列を使用します。 `ConnectionString` 設定を使用すると、リモート パーティションを別のリモート インスタンスに移動することができます。 ただし、`ConnectionString` 設定を使用して、復元されるデータベースを含む同じインスタンスにリモート パーティションを復元することはできません。 つまり、`ConnectionString` プロパティを使用してリモート パーティションをローカル パーティションにすることはできません。  
  
-   リモート データ ソースにリモート パーティションを格納するために使用元フォルダーごとに指定することができます、[フォルダー](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla)元のフォルダーに格納されているすべてのリモート パーティションを復元するための新しいフォルダーを示す要素。 `Folder` 要素が指定されていない場合、`Restore` コマンドは、リモート バックアップ ファイルに含まれるリモート パーティションに対して指定されている元のフォルダーを使用します。  
  
### <a name="relocating-rolap-objects"></a>ROLAP オブジェクトの再配置  
 `Restore` コマンドでは、ROLAP ストレージを使用するオブジェクトの集計やデータを復元できません。そのような情報は、基になるリレーショナル データ ソースのテーブルに格納されているためです。 ただし、ROLAP オブジェクトのメタデータは復元できます。 ROLAP オブジェクトのメタデータを復元するために、`Restore` コマンドはリレーショナル データ ソースのテーブル構造を再作成します。  
  
 `Location` コマンドで `Restore` 要素を使用すると、ROLAP オブジェクトの再配置を行えます。 各`Location`、データ ソースを配置する場合に使用される要素、`DataSourceType`プロパティ明示的に設定する必要があります*ローカル*します。 また、`ConnectionString` 要素の `Location` プロパティを、新しい場所の接続文字列に設定する必要があります。 復元の実行時に、`Restore` コマンドは、`DataSourceID` 要素の `Location` プロパティによって識別されるデータ ソースへの接続文字列を、`ConnectionString` 要素の `Location` プロパティの値に置き換えます。  
  
##  <a name="synchronizing_databases"></a> データベースの同期  
 `Synchronize` コマンドは、指定された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのデータとメタデータを別のデータベースと同期させます。 `Synchronize` コマンドには、同期元データベースやセキュリティ定義の同期方法、同期するリモート パーティション、および ROLAP オブジェクトの同期を指定するためのさまざまなプロパティがあります。  
  
> [!NOTE]  
>  `Synchronize` コマンドを実行できるのは、サーバー管理者とデータベース管理者だけです。 同期元データベースと同期先のデータベースの両方の互換性レベルが同じであることが必要です。  
  
### <a name="specifying-the-source-database"></a>同期元データベースの指定  
 [ソース](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)のプロパティ、`Synchronize`コマンドには、2 つのプロパティが含まれています。`ConnectionString`と`Object`します。 `ConnectionString` プロパティには同期元データベースを含むインスタンスの接続文字列が含まれ、`Object` プロパティには同期元データベースのオブジェクト識別子が含まれます。  
  
 同期先データベースは、`Synchronize` コマンドが実行されるセッションでの現在のデータベースです。  
  
 `ApplyCompression` コマンドの `Synchronize` プロパティが true に設定されている場合、同期元データベースから同期先データベースへ送信される情報は、送信前に圧縮されます。  
  
### <a name="synchronizing-security-settings"></a>セキュリティ設定の同期  
 [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla)プロパティかどうか、`Synchronize`コマンドは、ソース データベースで定義されたアクセス許可、ロールなど、セキュリティ定義を同期します。 `SynchronizeSecurity` プロパティは、`Sychronize` コマンドが Windows ユーザー アカウントとグループをセキュリティ定義のメンバーに含めるかどうかも決定します。  
  
 この要素の値は、次の表の一覧に示す文字列のいずれかに限定されています。  
  
|値|説明|  
|-----------|-----------------|  
|*skipMembership*|同期先データベースにセキュリティ定義を含めますが、メンバーシップ情報は除外します。|  
|*CopyAll*|同期先データベースにセキュリティ定義とメンバーシップ情報を含めます。|  
|*IgnoreSecurity*|同期先データベースからセキュリティ定義を除外します。|  
  
### <a name="synchronizing-remote-partitions"></a>リモート パーティションの同期  
 同期元データベース上に存在する各リモート データ ソースについては、`Location` コマンドの `Locations` プロパティに `Synchronize` 要素を含めることによって、それぞれに関連付けられているリモート パーティションを同期させることができます。 各`Location`要素、`DataSourceType`プロパティを除外または明示的に設定する必要があります*リモート*します。  
  
 同期先データベースのリモート データ ソースを定義してそれに接続するために、`Synchronize` コマンドでは、`ConnectionString` 要素の `Location` プロパティで定義されている接続文字列を使用します。 `Synchronize` コマンドはその後、`DataSourceID` 要素の `Location` プロパティを使用して、同期させるリモート パーティションを識別します。 `Synchronize`コマンドで指定されたリモート データ ソース上のリモート パーティションを同期する、`DataSourceID`プロパティで指定されたリモート データ ソースとソース データベースで、`DataSourceID`先データベースのプロパティ。  
  
 同期先データベースのリモート データ ソース上のリモート パーティションを格納するために使用されている元の各フォルダーについて、`Folder` 要素に `Location` 要素を指定することもできます。 `Folder` 要素は、リモート データ ソース上の元のフォルダーに格納されているすべてのリモート パーティションを同期させるための、同期先データベースに対する新しいフォルダーを示します。 `Folder` 要素が指定されていない場合、Synchronize コマンドは、同期元データベースに含まれるリモート パーティションに対して指定されている元のフォルダーを使用します。  
  
### <a name="synchronizing-rolap-objects"></a>ROLAP オブジェクトの同期  
 `Synchronize` コマンドでは、ROLAP ストレージを使用するオブジェクトの集計やデータを同期できません。そのような情報は、基になるリレーショナル データ ソースのテーブルに格納されているためです。 ただし、ROLAP オブジェクトのメタデータは同期できます。 メタデータを同期させるために、`Synchronize` コマンドはリレーショナル データ ソースのテーブル構造を再作成します。  
  
 Synchronize コマンドで `Location` 要素を使用すると、ROLAP オブジェクトの同期を行えます。 各`Location`、データ ソースを配置する場合に使用される要素、`DataSourceType`プロパティ明示的に設定する必要があります*ローカル*します。 . また、`ConnectionString` 要素の `Location` プロパティを、新しい場所の接続文字列に設定する必要があります。 同期の実行時に、`Synchronize` コマンドは、`DataSourceID` 要素の `Location` プロパティによって識別されるデータ ソースへの接続文字列を、`ConnectionString` 要素の `Location` プロパティの値に置き換えます。  
  
## <a name="see-also"></a>参照  
 [Backup 要素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Restore 要素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Synchronize 要素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Analysis Services データベースのバックアップと復元](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
