---
title: '&lt;xsd:redefine&gt; 要素 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8d7fe9246e0b689335d43a124c4a2391778f127a
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2018
ms.locfileid: "48905022"
---
# <a name="the-ltxsdredefinegt-element"></a>&lt;xsd:redefine&gt; 要素
  W3C XSD の **redefine** 要素は、スキーマ コンポーネントの再定義をサポートします。 ただし、このディレクティブは、パフォーマンス コストがかかる可能性があるともする必要がありますをサポート[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのインスタンスを再検証、`xml`再定義されたスキーマに関連付けられているデータ型。 このため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこれらの要素をサポートしません。 **\<xsd:redefine>** 要素を含む XML スキーマはサーバーに拒否されます。  
  
 スキーマまたはスキーマ コンポーネントを更新するには、代わりに次の方法を使用できます。  
  
1.  変更されたスキーマ コンポーネントを使用して新しい XML スキーマ コレクションを作成します。  
  
2.  すべてを再入力`xml`代わりに、新しい XML スキーマ コレクションを使用する再定義する XML スキーマ コレクションを使用するデータ型 (XML DT)。 そのためには、ALTER TABLE コマンドの ALTER COLUMN オプションを使用して列の型を再指定するか、変数やパラメーターの XML スキーマ コレクション制約を変更します。  
  
3.  古いバージョンの XML スキーマ コレクションを削除します。  
  
## <a name="see-also"></a>参照  
 [サーバー上の XML スキーマ コレクションの要件と制限](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
