---
title: '[バックアップ先の選択] | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a3642d349fd9d6df39651e38b8b1789dd935c49
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840380"
---
# <a name="select-backup-destination"></a>[バックアップ先の選択]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **[バックアップ先の選択]** ダイアログ ボックスを使用すると、バックアップ先としてデバイスを選択できます。 バックアップ先として、ディスクまたは論理バックアップ デバイスを使用できます。  
  
 **SQL Server Management Studio を使用してデータベースをバックアップするには**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>[変数]  
 このダイアログ ボックスのオプションは、ディスクまたはテープのどちらをバックアップ先として選択しているかによって異なります。  
  
 **[ディスクのバックアップ先]**  
 バックアップ先を指定するには、次のオプションのいずれかを選択します。  
  
|||  
|-|-|  
|**[ファイル名]**|ローカル ファイルまたはリモート ファイルをバックアップ先としてテキスト ボックスに入力するには、このオプションを選択します。<br /><br /> ローカル ファイルを指定するには、テキスト ボックスの右側にある参照ボタンをクリックし、サーバーを実行しているコンピューターの固定ディスク上のファイルに移動するか、完全なパスとファイル名を直接入力します (例 : `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`)。<br /><br /> バックアップ先としてリモート ファイルを指定するには、完全修飾の汎用名前付け規則 (UNC) 名を入力します。 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md))。<br /><br /> <br /><br /> **\*\* 重要 \*\*** ネットワークを経由してデータをバックアップすると、ネットワーク エラーが発生する可能性があります。バックアップ終了後にバックアップ操作を確認することをお勧めします。 詳細については、「[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)」をご覧ください。|  
|**バックアップ デバイス**|論理バックアップ デバイスを選択するには、このオプションを選択します。<br /><br /> 注: ディスク バックアップ デバイスを作成する方法の詳細については、「[ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)」を参照してください。|  
  
 **[テープのバックアップ先]**  
 サーバー (つまり、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンス) を実行しているコンピューターに、物理的に接続されているテープ ドライブ上のバックアップ先を指定します。 次のオプションの 1 つを選択します。  
  
|||  
|-|-|  
|**[テープ ドライブ]**|サーバー インスタンスを実行しているコンピューターに物理的に接続されているテープ ドライブの一覧から、バックアップ先としてテープ ドライブを選択するには、このオプションを選択します。<br /><br /> 注: リモート コンピューターのテープ バックアップ デバイスは、有効なバックアップ先ではありません。|  
|**バックアップ デバイス**|既存の論理バックアップ デバイスを選択するには、このオプションを選択します。 これらの論理バックアップ デバイスは、サーバー インスタンスを実行しているコンピューターに物理的に接続されているテープ ドライブに対応しています。<br /><br /> 注: テープバックアップ デバイスを作成する方法の詳細については、「[テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
