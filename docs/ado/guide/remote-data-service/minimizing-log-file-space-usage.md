---
title: ログ ファイル領域使用量を最小限に抑える |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8dc0799fbeba24ad4725d25647ef471edad8fb7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922555"
---
# <a name="minimizing-log-file-space-usage"></a>ログ ファイルの使用領域の最小化
ログ ファイルがすぐにいっぱい (サーバーが停止するため)、SQL Server データベースでのアクティビティ量が多い場合。 ログ ファイルを設定する**チェックポイントに Truncate**データベースのログ ファイルの有効期間を大幅に拡張します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5 のチェックポイントの切り捨てを有効にするには  
  
1.  Microsoft SQL Server Enterprise Manager を起動、サーバーのツリーをオープンし、データベース デバイス ツリーを開きます。  
  
2.  この機能を有効にするデータベースの名前をダブルクリックします。  
  
3.  **データベース**] タブで [ **Truncate**します。  
  
4.  **オプション**] タブで [**チェックポイントのログを切り捨てる**、順にクリックします**OK**します。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0 でのチェックポイントの切り捨てを有効にするには  
  
1.  Microsoft SQL Server Enterprise Manager を起動、サーバーのツリーをオープンし、データベース ツリーを開きます。  
  
2.  この機能を有効になります、選択は、データベースの名前を右クリックして**プロパティ**します。  
  
3.  **オプション**] タブで [**チェックポイントのログを切り捨てる**、順にクリックします**OK**します。  
  
 詳細については、**チェックポイントに Truncate**機能、Microsoft SQL Server のマニュアルを参照してください。  
  
## <a name="see-also"></a>関連項目  
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)


