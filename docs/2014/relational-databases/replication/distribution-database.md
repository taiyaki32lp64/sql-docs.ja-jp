---
title: ディストリビューション データベース | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.distributiondatabase.f1
ms.assetid: 5b42a083-7a11-41d8-9e3f-320c7c907237
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 283fd67d14d57c3d1d5d60dd9d8de2a159ca6d5e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721374"
---
# <a name="distribution-database"></a>ディストリビューション データベース
  ディストリビューション データベースには、すべての種類のレプリケーションのメタデータと履歴データ、およびトランザクション レプリケーションのトランザクションが格納されます。  
  
 多くの場合、ディストリビューション データベースは 1 つで十分です。 ただし、複数のパブリッシャーが 1 つのディストリビューターを使用する場合は、各パブリッシャーにディストリビューション データベースを作成することを検討してください。 これによって、各ディストリビューション データベースを経由するデータ フローが区別されます。 ディストリビューターに 1 つのディストリビューション データベースを指定するには、ディストリビューション構成ウィザードを使用します。 必要に応じて、 **[ディストリビューターのプロパティ]** ダイアログ ボックスで追加のディストリビューション データベースを指定できます。  
  
## <a name="options"></a>および  
 **[ディストリビューション データベース名]**  
 ディストリビューション データベースに付ける名前を入力します。 ディストリビューション データベースの既定の名前は "distribution" です。 名前を付ける場合は、128 文字以内で、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内で一意であり、識別子のルールに準拠している名前にする必要があります。 詳細については、「[データベース識別子](../databases/database-identifiers.md)」を参照してください。  
  
 **[ディストリビューション データベース ファイルのフォルダー]** と **[ディストリビューション データベース ログ ファイルのフォルダー]**  
 ディストリビューション データベース ファイルとログ ファイルのパスを入力します。 パスは、ディストリビューターにとってローカルなディスクを参照し、ローカル ドライブ名とコロン (C: など) で始まる必要があります。 マップされたドライブ名およびネットワーク パスは無効です。  
  
> [!NOTE]  
>  ディストリビューション データベース ログをディストリビューション データベースとは別のディスク ドライブに置くようにすると、トランザクションの書き込みに要する時間が短縮され、レプリケーションのパフォーマンスが向上します。  
  
## <a name="see-also"></a>参照  
 [[ディストリビューションの構成]](configure-distribution.md)   
 [パブリッシングとディストリビューションの構成](configure-publishing-and-distribution.md)   
 [ディストリビューターとパブリッシャーのプロパティの表示および変更](view-and-modify-distributor-and-publisher-properties.md)  
  
  
