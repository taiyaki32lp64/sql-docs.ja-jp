---
title: '[バックアップ デバイス] ([メディアの内容] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdevice.contents.f1
ms.assetid: 5fc7bd22-b6d8-4af1-8a58-2e7d0b994d08
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 524e6d8e5ec987a20d693cb1f7e06b30bc27c0b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876694"
---
# <a name="backup-device-media-contents-page"></a>[バックアップ デバイス] \([メディアの内容] ページ)
  **[バックアップ デバイス]** ダイアログ ボックスを使用すると、バックアップの情報が表示されます。 ここでは、デバイス、メディア、メディア セット、バックアップ セットの情報が得られます。  
  
 **SQL Server Management Studio を使用してバックアップ デバイスの内容を表示するには**  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>および  
 個々のメディア、メディア セット、バックアップ セットに関する情報を表示します。  
  
 **メディア**  
 バックアップ情報が保存されるディスク、またはテープのセットです。  
  
 **[メディア シーケンス]**  
 メディア シーケンス番号、ファミリ シーケンス番号、ミラー識別子を一覧表示します (それぞれ存在する場合)。 物理的なバックアップ メディアには、メディアが使用された順序を示すメディア シーケンス番号がそれぞれに付けられます。 最初のバックアップ メディアには 1 が割り当てられ、2 番目のメディア (つまり最初の後続テープ) には 2 が割り当てられます。 バックアップ セットを復元する際に、このシーケンス番号を使用することで、適切なメディアを適切な順序でマウントできます。  
  
 **[作成日]**  
 メディア セットが作成された日付と時刻を表示します。  
  
 **[メディア セット]**  
 メディア セットとは、一定の数のバックアップ デバイスを使用し、1 回以上のバックアップ操作で書き込まれたバックアップ メディアを番号順に並べた集合体です。  
  
 **名前**  
 メディア セットの名前を表示します (メディア セットが存在する場合)。  
  
 **[説明]**  
 メディア セットの説明を表示します (メディア セットが存在する場合)。  
  
 **[メディア ファミリ数]**  
 メディア セット内のファミリの数を表示します。 各メディア セットは、1 つ以上のメディア ファミリの集合体です。 特定の 1 つのバックアップ デバイス (またはミラーリングされるバックアップ デバイスのグループ) に対するすべての出力が、1 つのメディア ファミリを形成します。 各メディア セットには、単独のデバイス (またはミラーリングされるデバイスのグループ) ごとに 1 つのメディア ファミリが含まれます。たとえば、メディア セットでミラーリングされないバックアップ デバイスが 2 つ使用されている場合、このメディア セットには 2 つのメディア ファミリが含まれます。  
  
 **[バックアップ セット]**  
 メディアに収められているバックアップ セットに関する情報を表示します。 バックアップ セットとは、正常に完了したバックアップ操作の結果です。バックアップ セットの内容は、一連のバックアップ デバイスのメディアに分散されます。  
  
|[ヘッダー]|値|  
|------------|------------|  
|**名前**|バックアップ セットの名前です。|  
|**型**|オブジェクトのバックアップ:データベース、ファイル、または *\<空白 >* (トランザクション ログ用)。|  
|**コンポーネント**|実行するバックアップの種類: 差分バックアップまたはトランザクション ログはいっぱいです。|  
|**[サーバー]**|バックアップ操作を実行した [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスの名前。|  
|**[データベース]**|バックアップされたデータベースの名前。|  
|**[位置]**|ボリューム内でのバックアップ セットの位置。|  
|**Date**|バックアップ操作が完了したときの日付と時刻。クライアントの地域設定で表示されます。|  
|**Size**|バックアップ セットのサイズ (バイト単位) です。|  
|**[ユーザー名]**|バックアップ操作を実行したユーザーの名前。|  
|**[有効期限]**|バックアップ セットの期限が切れる日付と時刻。|  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [バックアップ先としてディスクまたはテープを指定する &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [バックアップ デバイスの削除 &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [バックアップの有効期限の設定 &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [バックアップ セットに含まれているデータ ファイルおよびログ ファイルの表示 &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [デバイスからのバックアップ復元 &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
