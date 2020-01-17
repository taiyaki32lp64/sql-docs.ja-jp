---
title: 大きな XML スキーマ コレクションとメモリ不足状態 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- out-of-memory conditions
- XML schema collections [SQL Server], large
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 513e95798062f85484b5693d5c75e6aef3efcc82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63285546"
---
# <a name="large-xml-schema-collections-and-out-of-memory-conditions"></a>大きな XML スキーマ コレクションとメモリ不足状態
  大きな XML スキーマ コレクションで組み込み XML_SCHEMA_NAMESPACE() 関数を呼び出しているとき、または大きな XML スキーマ コレクションを削除するときに、メモリが不足することがあります。 次に示すのは、このような状態に対処する際に使用できる解決策です。  
  
-   システムの負荷が低い場合は、DROP_XML_SCHEMA_COLLECTION コマンドを使用します。 この操作が失敗する場合は、ALTER DATABASE ステートメントを使用し、DROP XML SCHEMA COLLECTION を再試行してデータベースをシングル ユーザー モードにします。 XML スキーマ コレクションが **master**、 **model**、または **tempdb**に存在する場合は、シングル ユーザー モードにするためにサーバーを再起動する必要があります。  
  
-   XML_SCHEMA_NAMESPACE を呼び出す場合、単一の XML スキーマ名前空間の取得、システムの負荷低下時の呼び出し、またはシングル ユーザー モードでの呼び出しを試行することができます。  
  
## <a name="see-also"></a>関連項目  
 [サーバー上の XML スキーマ コレクションの要件と制限](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
