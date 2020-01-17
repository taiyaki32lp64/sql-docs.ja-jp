---
title: '[データベースのバックアップ] ([バックアップ オプション] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdatabase.options.f1
- swb.backupdatabase.options.f1
ms.assetid: df0ddcdb-c94e-472b-b786-469ae8117b93
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c8030a0005f0f5b949a3eecd12d73f3a3aa709c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876865"
---
# <a name="back-up-database-backup-options-page"></a>[データベースのバックアップ] \([バックアップ オプション] ページ)
  **[データベースのバックアップ]** ダイアログ ボックスの **[バックアップ オプション]** ページを使用すると、データベースのバックアップのオプションを表示または変更できます。  
  
 **SQL Server Management Studio を使用してバックアップを作成するには**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  データベース メンテナンス プランを定義して、データベース バックアップを作成できます。 詳細については、「 [メンテナンス プラン](../maintenance-plans/maintenance-plans.md) 」および「 [メンテナンス プラン ウィザードの使用](../maintenance-plans/use-the-maintenance-plan-wizard.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してバックアップ タスクを指定する場合、 [!INCLUDE[tsql](../../includes/tsql-md.md)][[スクリプト]](/sql/t-sql/statements/backup-transact-sql) ボタンをクリックしてスクリプトの保存先を選択することにより、対応する **BACKUP** スクリプトを生成できます。  
  
## <a name="options"></a>および  
  
### <a name="backup-set"></a>バックアップ セット  
 **[バックアップ セット]** パネルのオプションでは、バックアップ操作で作成されるバックアップ セットに関する情報を指定できます。  
  
 **名前**  
 バックアップ セット名を指定します。 データベース名とバックアップの種類に基づいて、既定の名前が自動的に表示されます。  
  
 バックアップ セットの詳細については、「[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
 **[説明]**  
 バックアップ セットの説明を入力します。  
  
 **[バックアップ セットの有効期限]**  
 次の有効期限オプションの 1 つを選択します。 **[URL]** がバックアップ先として選択された場合、このオプションは無効です。  
  
|||  
|-|-|  
|**After**|このバックアップ セットが失効して上書きできるようになるまでの経過日数を指定します。 0 ～ 99,999 日の値を指定できます。0 日を指定すると、バックアップ セットの有効期限は無期限になります。<br /><br /> バックアップの有効期限の既定値は、 **[バックアップ メディアの既定の保有期間 (日)]** オプションの値のセットです。 このオプションを表示するには、オブジェクト エクスプローラーでサーバー名を右クリックし、 **[プロパティ]** を選択した後、 **[サーバーのプロパティ]** ダイアログ ボックスの **[データベースの設定]** ページをクリックします。|  
|**基準**|バックアップ セットが失効して上書きできるようになる特定の日を指定します。|  
  
### <a name="compression"></a>圧縮  
 [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] (またはそれ以降のバージョン) では、 [バックアップの圧縮](backup-compression-sql-server.md)がサポートされています。  
  
 **[バックアップの圧縮の設定]**  
 [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] (またはそれ以降のバージョン) で、バックアップの圧縮の値を次の中から 1 つ選択します。  
  
|||  
|-|-|  
|**[既定のサーバー設定を使用する]**|オンにすると、サーバー レベルの既定値が使用されます。<br /><br /> この既定値は、 **backup compression default** サーバー構成オプションで設定されます。 このオプションの現在の設定を表示する方法については、「 [backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)」を参照してください。|  
|**[バックアップを圧縮する]**|オンにすると、サーバー レベルの既定値に関係なく、バックアップが圧縮されます。<br /><br /> **\*\* 重要 \*\*** 既定の設定では、圧縮によって CPU 使用率が著しく増加し、圧縮処理によって CPU がさらに消費されるために、同時に実行される操作が悪影響を受ける場合があります。 このため、 [リソース ガバナー](../resource-governor/resource-governor.md)によって CPU 使用率が制限されるセッションでは、優先度の低い圧縮バックアップを作成することができます。 詳細については、「 [リソース ガバナーを使用してバックアップの圧縮による CPU 使用率を制限する方法 &#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)」を参照してください。|  
|**[バックアップを圧縮しない]**|オンにすると、サーバー レベルの既定値に関係なく、圧縮されていないバックアップが作成されます。|  
  
### <a name="encryption"></a>暗号化  
 暗号化されたバックアップを作成するには、 **[バックアップ ファイルを暗号化する]** チェック ボックスをオンにします。 暗号化手順に使用する暗号化アルゴリズムを選択し、既存の証明書または非対称キーの一覧から証明書または非対称キーを指定します。 暗号化に使用できるアルゴリズムは次のとおりです。  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   Triple DES  
  
> [!TIP]  
>  既存のバックアップ セットに追加することを選択した場合、暗号化オプションは無効になります。  
>   
>  証明書またはキーをバックアップし、暗号化されたバックアップとは別の場所に保管することをお勧めします。  
>   
>  拡張キー管理 (EKM) に存在するキーのみがサポートされます。  
  
## <a name="see-also"></a>関連項目  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [データベースが破損したときのトランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
