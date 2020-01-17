---
title: データベース エンジンの構成 - データ ディレクトリ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9b1fa0fc-623b-479a-afc3-4f13bd850487
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfb62ec0bbd16a2b77e2f05f64d36ef31498a100
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095899"
---
# <a name="database-engine-configuration---data-directories"></a>データベース エンジンの構成 - データ ディレクトリ
  このページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] のプログラムおよびデータ ファイルのインストール場所を指定します。 インストールの種類により、サポートされるストレージにはローカル ディスク、共有ストレージ、または SMB ファイル サーバーが含まれる場合があります。  
  
 SMB ファイル共有をディレクトリとして指定するには、サポートされている UNC パスを手動で入力する必要があります。 SMB ファイル共有を参照して指定することはできません。 SMB ファイル共有のサポートされる UNC パス形式は、" \\\Servername\ShareName\\..." です。  
  
## <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンス  
 次の表は、サポートされているストレージの種類と、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスで使用される既定のディレクトリの一覧です。これらのディレクトリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ中にユーザーが構成できます。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
  
|説明|サポートされているストレージの種類|既定のディレクトリ|推奨事項|  
|-----------------|----------------------------|-----------------------|---------------------|  
|データ ルート ディレクトリ|ローカル ディスク、SMB ファイル サーバー、共有記憶域<sup>1</sup>|C:\Program Files\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \| [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の Acl を構成するセットアップ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ディレクトリと構成の一部として継承します。|  
|ユーザー データベース ディレクトリ|ローカル ディスク、SMB ファイル サーバー、共有記憶域<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data|ユーザー データ ディレクトリのベスト プラクティスは、ワークロードとパフォーマンスの要件によって異なります。|  
|ユーザー データベース ログ ディレクトリ|ローカル ディスク、SMB ファイル サーバー、共有記憶域<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data|ログ ディレクトリに十分な領域があることを確認してください。|  
|一時データベース ディレクトリ|ローカル ディスク、SMB ファイル サーバー、共有記憶域<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data|Temp ディレクトリのベスト プラクティスは、ワークロードとパフォーマンスの要件によって異なります。|  
|一時データベース ログ ディレクトリ|ローカル ディスク、SMB ファイル サーバー、共有記憶域<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Data|ログ ディレクトリに十分な領域があることを確認してください。|  
|バックアップ ディレクトリ|ローカル ディスク、SMB ファイル サーバー、共有記憶域<sup>1</sup>|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Backup|データの損失を防ぐために適切な権限を設定して、バックアップ ディレクトリに書き込むための適切な権限が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのユーザー アカウントにあることを確認してください。 マップされたドライブをバックアップ ディレクトリに使用することはサポートされていません。|  
  
 <sup>1</sup>のスタンドアロン インスタンスで推奨される方法ではない共有ディスクはサポートされていますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
## <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフェールオーバー クラスター インスタンス  
 次の表は、サポートされているストレージの種類と、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフェールオーバー クラスター インスタンスで使用される既定のディレクトリの一覧です。これらのディレクトリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ中にユーザーが構成できます。  
  
|説明|サポートされているストレージの種類|既定のディレクトリ|推奨事項|  
|-----------------|----------------------------|-----------------------|---------------------|  
|データ ルート ディレクトリ|共有ストレージ、SMB ファイル サーバー|\<ドライブ>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> ヒント: **[クラスター ディスクの選択]** ページで共有ディスクを選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しなかった場合、このフィールドの既定値は空白になります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリの ACL が構成され、構成の一部として継承が無効になります。|  
|ユーザー データベース ディレクトリ|共有ストレージ、SMB ファイル サーバー|\<ドライブ: > Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.\< 。InstanceID > \MSSQL\Data<br /><br /> ヒント: **[クラスター ディスクの選択]** ページで共有ディスクを選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しなかった場合、このフィールドの既定値は空白になります。|ユーザー データ ディレクトリのベスト プラクティスは、ワークロードとパフォーマンスの要件によって異なります。|  
|ユーザー データベース ログ ディレクトリ|共有ストレージ、SMB ファイル サーバー|\<ドライブ: > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.\< 。InstanceID > \MSSQL\Data<br /><br /> ヒント: **[クラスター ディスクの選択]** ページで共有ディスクを選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しなかった場合、このフィールドの既定値は空白になります。|ログ ディレクトリに十分な領域があることを確認してください。|  
|一時データベース ディレクトリ|ローカル ディスク、共有ストレージ、SMB ファイル サーバー|\<ドライブ: > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.\< 。InstanceID > \MSSQL\Data<br /><br /> ヒント: **[クラスター ディスクの選択]** ページで共有ディスクを選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しなかった場合、このフィールドの既定値は空白になります。|指定したディレクトリがすべてのクラスター ノードで有効であることを確認してください。 フェールオーバー中に、tempdb のディレクトリがフェールオーバーのターゲット ノード上で利用できない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースはオンラインへの移行に失敗します。|  
|一時データベース ログ ディレクトリ|ローカル ディスク、共有ストレージ、SMB ファイル サーバー|\<ドライブ: > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.\< 。InstanceID > \MSSQL\Data<br /><br /> ヒント: **[クラスター ディスクの選択]** ページで共有ディスクを選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しなかった場合、このフィールドの既定値は空白になります。|指定したディレクトリがすべてのクラスター ノードで有効であることを確認してください。 フェールオーバー中に、tempdb のディレクトリがフェールオーバーのターゲット ノード上で利用できない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースはオンラインへの移行に失敗します。|  
|バックアップ ディレクトリ|ローカル ディスク、共有ストレージ、SMB ファイル サーバー|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\<InstanceID>\MSSQL\Backup<br /><br /> ヒント: **[クラスター ディスクの選択]** ページで共有ディスクを選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しなかった場合、このフィールドの既定値は空白になります。|データの損失を防ぐために適切な権限を設定して、バックアップ ディレクトリに書き込むための適切な権限が SQL Server サービスのユーザー アカウントにあることを確認してください。 マップされたドライブをバックアップ ディレクトリに使用することはサポートされていません。|  
  
## <a name="security-considerations"></a>セキュリティに関する考慮事項  
 セットアップにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリの ACL が構成され、構成の一部として継承が無効になります。  
  
 次の推奨事項は SMB ファイル サーバーに当てはまります。  
  
-   SMB ファイル サーバーを使用する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントはドメイン アカウントである必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに使用するアカウントには、データ ディレクトリとして使用する SMB ファイル共有フォルダーに対するフル コントロールの NTFS 権限が必要です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに使用するアカウントには、SMB ファイル サーバーに対する SeSecurityPrivilege 特権を付与する必要があります。 この特権を付与するには、ファイル サーバーで [ローカル セキュリティ ポリシー] コンソールを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査とセキュリティ ログの管理 **ポリシーに** セットアップ アカウントを追加します。 この設定は、 **[ローカル セキュリティ ポリシー]** コンソールの **[ローカル ポリシー]** にある **[ユーザー権利の割り当て]** セクションで行うことができます。  
  
## <a name="notes"></a>メモ  
  
-   既存のインストールに機能を追加する場合、前にインストールした機能の場所は変更できません。また、新しい機能のインストール場所を指定することもできません。  
  
-   既定以外のインストール ディレクトリを指定する場合は、インストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンス内の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは、別のディレクトリにインストールする必要もあります。  
  
-   次の状況では、プログラム ファイルとデータ ファイルをインストールすることができません。  
  
    -   リムーバブル ディスク ドライブ  
  
    -   圧縮を使用したファイル システム  
  
    -   システム ファイルが配置されているディレクトリ  
  
    -   フェールオーバー クラスター インスタンス上のマップされたネットワーク ドライブ  
  
## <a name="see-also"></a>参照  
 [SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [ファイル サーバーの共有アクセス許可と NTFS アクセス許可](https://go.microsoft.com/fwlink/?LinkID=206571)  
  
  
