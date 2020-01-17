---
title: '[バックアップ先の選択] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d9b4a0e07f32e074ff7e8875c263615bcebc12d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874878"
---
# <a name="select-backup-destination"></a>[バックアップ先の選択]
  **[バックアップ先の選択]** ダイアログ ボックスを使用すると、バックアップ先としてデバイスを選択できます。 バックアップ先として、ディスクまたは論理バックアップ デバイスを使用できます。  
  
 **SQL Server Management Studio を使用してデータベースをバックアップするには**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>および  
 このダイアログ ボックスのオプションは、ディスクまたはテープのどちらをバックアップ先として選択しているかによって異なります。  
  
 **[ディスクのバックアップ先]**  
 バックアップ先を指定するには、次のオプションのいずれかを選択します。  
  
|||  
|-|-|  
|**[ファイル名]**|ローカル ファイルまたはリモート ファイルをバックアップ先としてテキスト ボックスに入力するには、このオプションを選択します。<br /><br /> ローカル ファイルを指定するには、テキスト ボックスの右側にある参照ボタンをクリックしますと、サーバーを実行しているコンピューターの固定ドライブでのファイルに移動または直接、完全なパスとファイル名を入力してください。たとえば、`C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`します。<br /><br /> バックアップ先としてリモート ファイルを指定するには、完全修飾の汎用名前付け規則 (UNC) 名を入力してください。 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)の別のインスタンスで作成された場合、これは必須です。<br /><br /> **\*\* 重要 \*\*** ネットワークを経由してデータをバックアップすると、ネットワーク エラーが発生する可能性があります。バックアップ終了後にバックアップ操作を確認することをお勧めします。 詳細については、「[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)」をご覧ください。|  
|**バックアップ デバイス**|論理バックアップ デバイスを選択するには、このオプションを選択します。<br /><br /> 注:ディスク バックアップ デバイスを作成する方法については、次を参照してください。[ディスク ファイルの論理バックアップ デバイスを定義&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)します。|  
  
 **[テープのバックアップ先]**  
 サーバー (つまり、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンス) を実行しているコンピューターに、物理的に接続されているテープ ドライブ上のバックアップ先を指定します。 次のオプションの 1 つを選択します。  
  
|||  
|-|-|  
|**[テープ ドライブ]**|サーバー インスタンスを実行しているコンピューターに物理的に接続されているテープ ドライブの一覧から、バックアップ先としてテープ ドライブを選択するには、このオプションを選択します。<br /><br /> 注:リモート コンピューターのテープ バックアップ デバイスは、有効なバックアップ先ではありません。|  
|**バックアップ デバイス**|既存の論理バックアップ デバイスを選択するには、このオプションを選択します。 これらの論理バックアップ デバイスは、サーバー インスタンスを実行しているコンピューターに物理的に接続されているテープ ドライブに対応しています。<br /><br /> 注:テープ バックアップ デバイスを作成する方法については、次を参照してください。[テープ ドライブの論理バックアップ デバイスを定義する&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)します。|  
  
## <a name="see-also"></a>関連項目  
 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
