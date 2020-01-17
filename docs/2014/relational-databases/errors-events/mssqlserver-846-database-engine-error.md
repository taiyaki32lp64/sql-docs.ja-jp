---
title: MSSQLSERVER_846 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 846 (Database Engine error)
ms.assetid: ccf367eb-06b0-42b8-b4d6-2b88f4a502d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6e25752cd1f12143f4d05b8b4b02f138784a72a1
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874576"
---
# <a name="mssqlserver_846"></a>MSSQLSERVER_846
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|846|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|なし|  
|メッセージ テキスト|バッファー ラッチを待機中にタイムアウトが発生しました。型 %d、BP %p、ページ %d:%d、状態 %#x、データベース ID: %d、アロケーション ユニット ID: %I64d%ls、タスク 0x%p : %d、待機時間 %d、フラグ 0x%I64x、所有しているタスク 0x%p。 待機は続行されません。|  
  
## <a name="explanation"></a>説明  
 コンピューターが応答を停止したか、タイムアウトまたは通常の操作の中断が発生した[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ときに、バッファーラッチエラーが[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エラーログに書き込まれます。  
  
 メッセージの状態フィールドの値 0x04 がオンの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は I/O 操作を待機しています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログにメッセージ [MSSQLSERVER_833](mssqlserver-833-database-engine-error.md) を受信する場合もあります。  
  
 メッセージの状態フィールドの値 0x04 がオフの場合、ページに対して多数の競合が存在します。 オブジェクトがデータ ページの場合、非効率なコード デザインに起因している可能性があります。 データ以外のページの場合、ハードウェア リソースの不足など、サーバーのボトルネックによってエラーが発生した可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 この問題を回避するには、環境に応じて次の 1 つ以上の手順を実行します。これにより、エラー メッセージの発生を回避または減らすことができる可能性があります。  
  
-   ハードウェアにボトルネックがあるかどうかを判断します。 必要な場合、使用している環境の構成、クエリ、および負荷要件がサポートされるように、ハードウェアをアップグレードします。 ボトルネックの詳細については、「[Identify Bottlenecks](../performance/identify-bottlenecks.md)」 (ボトルネックの特定) を参照してください。  
  
-   記録されたエラーを確認し、ハードウェア ベンダーの提供する診断を実行します。  
  
-   ディスク ドライブが圧縮されていないことを確認してください。 データ ファイルやログ ファイルを圧縮ドライブに格納することはできません。 物理的ファイルの詳細については、「[Database Files and Filegroups](../databases/database-files-and-filegroups.md)」 (データベース ファイルとファイル グループ) をご覧ください。  
  
-   次のオプションをオフに設定して、エラー メッセージが消えるかどうかを確認します。  
  
    -   SQL Server の priority boost 構成オプション  
  
    -   簡易プーリング (ファイバー モード) オプション  
  
    -   set working set size オプション  
  
    > [!NOTE]  
    >  これらの設定を既定のオフから変更すると、多くの場合、効率が悪化します。 詳細については、「[Server Configuration Options &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」 (サーバー構成オプション (SQL Server)) を参照してください。  
  
-   クエリをチューニングして、システムで使用するリソースを削減します。 パフォーマンス チューニングは、システム負荷の削減と、個々のクエリの応答時間改善に役立ちます。  
  
-   AUTO_SHRINK オプションをオフにして、データベース サイズに対する変更のオーバーヘッドを軽減します。  
  
-   FILEGROWTH オプションに、頻繁になりすぎないように十分な大きさを持った増分値を設定するようにします。 データベース内で使用可能な領域を確認するジョブをスケジュールし、ピーク時以外にデータベース サイズを大きくします。  
  
  
