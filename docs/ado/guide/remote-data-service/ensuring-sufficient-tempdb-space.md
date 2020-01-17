---
title: 十分な TempDB 領域を確保 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe377cd15f2b95577a561e6784f78113b2843d07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922655"
---
# <a name="ensuring-sufficient-tempdb-space"></a>十分な TempDB 領域の確保
処理中にエラーが発生した場合[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Microsoft SQL Server 6.5 の領域を処理する必要があるオブジェクトの場合は、TempDB のサイズを大きく必要があります。 (いくつかのクエリが一時的な処理容量が必要ですたとえば、ORDER BY 句を使用してクエリには、並べ替えが必要です。 の、 **Recordset**、いくつかの一時領域必要があります。)。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
> [!IMPORTANT]
>  として簡単に展開されていると、デバイスを圧縮することがないため、操作を実行する前に、この手順を読みます。  
  
> [!NOTE]
>  形状の既定で SQL Server 7.0 以降、TempDB が自動的に拡大に応じて設定されます。 そのため、この手順は、7.0 より前のバージョンを実行するサーバーで必要のみにあります。  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>SQL Server 6.5 で TempDB の領域を増やす  
  
1.  Microsoft SQL Server Enterprise Manager を起動、サーバーのツリーをオープンし、データベース デバイス ツリーを開きます。  
  
2.  展開し、マスターなど (物理) デバイスを選択し、開くデバイスをダブルクリックして、**データベース デバイスの編集** ダイアログ ボックス。  
  
     このダイアログ ボックスには、現在のデータベースを使用している領域の量が表示されます。  
  
3.  **サイズ**ボックスに、必要な量 (たとえば、50 メガバイト (MB) のハード_ディスク領域) にデバイスを大ききます。  
  
4.  クリックして**今すぐ変更**を (論理) の TempDB の拡張可能領域の量を増やします。  
  
5.  サーバーで、データベースのツリーを開き、ダブルクリック**TempDB**を開く、**データベースの編集** ダイアログ ボックス。 **データベース**タブには、TempDB に現在割り当てられている領域の量が一覧表示されます (**データ サイズ**)。 既定では、2 MB になります。  
  
6.  で、**サイズ**グループで、**展開**します。 グラフの各物理デバイスに使用できる割り当て領域を表示します。 茶色のバーでは、使用可能な領域を表します。  
  
7.  選択、**ログ デバイス**、マスターで使用可能なサイズを表示するなど、**サイズ (MB)** ボックス。  
  
8.  をクリックして**今すぐ展開**TempDB データベースにその領域を割り当てます。  
  
     **データベースの編集** ダイアログ ボックスが表示されます、新しい TempDB のサイズに割り当てられます。  
  
 詳細については、このトピックでは、「データベースの [展開] ダイアログ ボックス」は、Microsoft SQL Server Enterprise Manager のヘルプ ファイルを検索します。  
  
## <a name="see-also"></a>関連項目  
 [RDS の基礎](../../../ado/guide/remote-data-service/rds-fundamentals.md)


