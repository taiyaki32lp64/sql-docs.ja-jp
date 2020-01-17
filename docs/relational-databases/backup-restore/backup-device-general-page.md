---
title: '[バックアップ デバイス] ([全般] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backupdevice.general.f1
ms.assetid: c557e37d-319e-4adb-a0c1-94189b15d2ac
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0d37918c0ca2be62c2e620faa8034548df2b4592
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940824"
---
# <a name="backup-device-general-page"></a>[バックアップ デバイス]\([全般] ページ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[全般]** ページを使用すると、論理バックアップ デバイスの全般プロパティを指定したり、表示したりできます。  
  
 **SQL Server Management Studio を使用してバックアップ デバイスの内容を表示するには**  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>オプション  
 **[デバイス名]**  
 既存の論理バックアップ デバイスの名前を表示するか、新しい論理バックアップ デバイスの名前を指定します。  
  
 **Tape**  
 **[テープ]** の一覧からバックアップ先テープ デバイスを表示したり、選択したりします。 このオプションは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスが動作しているコンピューターにテープ ドライブが装着されている場合のみ使用できます。  
  
> [!NOTE]  
>  リモート コンピューターのテープ バックアップ デバイスは、有効なバックアップ先ではありません。  
  
 **[最近使ったファイル]**  
 既存の論理バックアップ デバイスのバックアップ先ファイルを表示するか、新しい論理バックアップ デバイスのバックアップ先ファイルを指定します。  
  
-   既存の論理バックアップ デバイスを使用する場合、バックアップ ファイルのパスが表示されます。 **[ファイル]** フィールドは編集できません。また、参照ボタンは使用できません。  
  
-   新しい論理バックアップ デバイスでは、論理バックアップ デバイスを定義しているバックアップ ファイルのパスを設定する必要があります。 このファイルは、まだ存在していなくてもかまいません。  
  
     ローカル バックアップ ファイルを指定するには、 **[ファイル]** ボックスの右の参照ボタンをクリックできます。 その後、 **[データベース ファイルの検索]** ダイアログ ボックスを使用して、サーバー インスタンスを実行しているコンピューターの固定ドライブの任意の場所に移動できます。 バックアップ ファイルが存在しない場合、ダイアログ ボックスの **[ファイル名]** に使用するファイル名を入力する必要があります。  
  
     **[ファイル]** を手動で編集して、既定のパス、ファイル名、および拡張子をオーバーライドすることもできます。 バックアップ先としてリモート ファイルを指定するには、完全修飾の汎用名前付け規則 (UNC) 名を入力してください。 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)のインスタンスが動作しているコンピューターにテープ ドライブが装着されている場合のみ使用できます。  
  
    > [!IMPORTANT]  
    >  ネットワークを経由してデータをバックアップすると、ネットワーク エラーが発生する可能性があります。バックアップ終了後にバックアップ操作を確認することをお勧めします。 詳細については、「[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
 単一または一連のバックアップ デバイス上にあるバックアップによって、1 つのメディア セットが構成されます。 *メディア セット* とは、テープやディスク ファイルなどのバックアップ メディアに順番を付けてまとめたものです。バックアップ メディアには、1 回以上のバックアップ操作によって、固定型の複数のバックアップ デバイスを使用して書き込まれます。 メディア セットの詳細については、「 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)のインスタンスが動作しているコンピューターにテープ ドライブが装着されている場合のみ使用できます。  
  
 論理バックアップ デバイスに対応している物理バックアップ デバイスは、メディア セットの最初のバックアップを論理バックアップ デバイスに書き込むときに初期化されます。 物理バックアップ デバイスが、まだ存在していないファイルの場合は、この時点で作成されます。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ディスク ファイルの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [バックアップ先としてディスクまたはテープを指定する &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [バックアップ デバイスの削除 &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [バックアップの有効期限の設定 &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [バックアップ セットに含まれているデータ ファイルおよびログ ファイルの表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [デバイスからのバックアップ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
