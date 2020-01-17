---
title: アップデート グラムのセキュリティに関する考慮事項 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- security [SQLXML], updategrams
- updategrams [SQLXML], security
ms.assetid: 00dc6cf4-a2e8-4cca-bdd6-d5122102a82d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12354329d51bbe13930fc6edefca1fcf84171e33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66015055"
---
# <a name="updategram-security-considerations-sqlxml-40"></a>アップデートグラムのセキュリティに関する注意点 (SQLXML 4.0)
  次に、アップデートグラムを使用する場合のセキュリティに関するガイドラインを示します。  
  
-   アップデートグラムを使用してデータを更新する場合、既定のマッピングは使用しないでください。 既定のマッピングを使用すると、アップデートグラム内の要素名はテーブル名にマップされ、属性名は列にマップされます。 この方法では、データベース内のデータベース テーブルと列の情報が公開され、セキュリティが脅かされる可能性があります。 代わりに、独自のマッピング スキーマでアップデートグラムの要素および属性をデータベース テーブルおよび列にマップすれば、アップデートグラムの要素および属性には任意の名前を指定でき、スキーマによってこれらの名前のデータベース テーブルおよび列への必要なマッピングが行われます。 こうすると、アップデートグラムでデータベース情報は公開されません。  
  
-   アップデートグラムの作成と実行をユーザーに許可しないでください。 アップデートグラムはテンプレートとしてサーバーに置いておくことをお勧めします。ASP 型のアプリケーションでアップデートグラムを動的に作成すると、データベースのデータが保護されない危険性があります。 ユーザーには、アップデートグラムをテンプレートとして提供し、このアップデートグラム経由でのみデータへのアクセスを許可すれば、この危険を回避できます。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0 でのアップデートグラムを使用したデータの変更](../updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
  
  
