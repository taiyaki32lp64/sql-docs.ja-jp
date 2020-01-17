---
title: メモリ不足状態と大きな XML スキーマ コレクション | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- out-of-memory conditions
- XML schema collections [SQL Server], large
ms.assetid: 29b9d839-aaaf-48fb-be17-840c751f36f1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 085a59ce8861c3f38e5c7540d4d56201c896ccea
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257651"
---
# <a name="large-xml-schema-collections-and-out-of-memory-conditions"></a>大きな XML スキーマ コレクションとメモリ不足状態
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  大きな XML スキーマ コレクションで組み込み XML_SCHEMA_NAMESPACE() 関数を呼び出しているとき、または大きな XML スキーマ コレクションを削除するときに、メモリが不足することがあります。 次に示すのは、このような状態に対処する際に使用できる解決策です。  
  
-   システムの負荷が低い場合は、DROP_XML_SCHEMA_COLLECTION コマンドを使用します。 この操作が失敗する場合は、ALTER DATABASE ステートメントを使用し、DROP XML SCHEMA COLLECTION を再試行してデータベースをシングル ユーザー モードにします。 XML スキーマ コレクションが **master**、 **model**、または **tempdb**に存在する場合は、シングル ユーザー モードにするためにサーバーを再起動する必要があります。  
  
-   XML_SCHEMA_NAMESPACE を呼び出す場合、単一の XML スキーマ名前空間の取得、システムの負荷低下時の呼び出し、またはシングル ユーザー モードでの呼び出しを試行することができます。  
  
## <a name="see-also"></a>参照  
 [サーバー上の XML スキーマ コレクションの要件と制限](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
