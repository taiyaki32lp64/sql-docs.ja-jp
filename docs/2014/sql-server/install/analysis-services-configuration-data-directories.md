---
title: Analysis Services の構成 - データ ディレクトリ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ef732855-b7af-4f40-a619-5573c1c354bb
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 4ff1cd03eb260d892c22c36285fa07d912994510
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096808"
---
# <a name="analysis-services-configuration---data-directories"></a>Analysis Services の構成 - データ ディレクトリ
  次の表にある既定のディレクトリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ中にユーザーが構成できます。 これらのファイルにアクセスする権限は、ローカル管理者と、セットアップ中に作成されて準備される SQLServerMSASUser$\<インスタンス> セキュリティ グループのメンバーに付与されます。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
  
|説明|既定のディレクトリ|推奨事項|  
|-----------------|-----------------------|---------------------|  
|データ ルート ディレクトリ|C:\Program files \microsoft SQL Server\MSAS12 します。\<InstanceID > \OLAP\Data\|\Program files\Microsoft の SQL server \ フォルダーが権限の制限により保護されていることを確認します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のパフォーマンスは、多くの構成で、データ ディレクトリが配置されているストレージのパフォーマンスに依存します。 このディレクトリは、システムに割り当てられている中でパフォーマンスが最も高いストレージに配置してください。 フェールオーバー クラスターのインストールの場合は、データ ディレクトリが共有ディスク上に配置されるようにしてください。|  
|ログ ファイル ディレクトリ|C:\Program files \microsoft SQL Server\MSAS12 します。\<InstanceID > \OLAP\Log\|これは、ディレクトリの[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ログ ファイル、およびその FlightRecorder ログが含まれています。 フライト レコーダーの時間を増加する場合、ログ ディレクトリに十分な容量があることを確認してください。|  
|Temp ディレクトリ|C:\Program files \microsoft SQL Server\MSAS12 します。\<InstanceID > \OLAP\Temp\|Temp ディレクトリは、高パフォーマンス記憶域サブシステムに配置します。|  
|バックアップ ディレクトリ|C:\Program files \microsoft SQL Server\MSAS12 します。\<InstanceID > \OLAP\Backup\|これは、ディレクトリの[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]既定のバックアップ ファイル。 PowerPivot for SharePoint のインストールでは、ここは PowerPivot System サービスが PowerPivot データ ファイルをキャッシュする場所でもあります。<br /><br /> データの損失を防ぐために適切な権限を設定し、バックアップ ディレクトリに書き込むための適切な権限が [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サービスのユーザー グループに付与されるようにしてください。 マップされたドライブをバックアップ ディレクトリに使用することはサポートされていません。|  
  
## <a name="notes"></a>メモ  
  
-   SharePoint ファームに配置された [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスは、アプリケーション ファイル、データ ファイル、およびコンテンツ データベースのプロパティとサービス アプリケーション データベースのプロパティを格納します。  
  
-   既存のインストールに機能を追加する場合、前にインストールした機能の場所は変更できません。また、新しい機能のインストール場所を指定することもできません。  
  
-   既定以外のインストール ディレクトリを指定する場合は、インストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンス内の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは、別のディレクトリにインストールする必要もあります。  
  
-   次の状況では、プログラム ファイルとデータ ファイルをインストールすることができません。  
  
    -   リムーバブル ディスク ドライブ  
  
    -   圧縮を使用したファイル システム  
  
    -   システム ファイルが配置されているディレクトリ  
  
## <a name="see-also"></a>参照  
 [SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
  
