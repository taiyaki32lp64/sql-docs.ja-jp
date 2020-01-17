---
title: SQL Server のバイナリ データと大きな値のデータ
description: SQL Server で大きな値のデータを操作する方法について説明します。
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 0a38d90a810f9ca3ee376562eaabf6e713267b27
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452052"
---
# <a name="sql-server-binary-and-large-value-data"></a>SQL Server のバイナリ データと大きな値のデータ

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server には `max` 指定子が用意されており、`varchar`、`nvarchar`、および `varbinary` データ型のストレージ容量を拡張します。 `varchar(max)`、`nvarchar(max)`、`varbinary(max)` は、総称して*大きな値のデータ型*と呼びます。 大きな値のデータ型を使用すると、最大で 2^31-1 バイトのデータを格納できます。  
  
SQL Server 2008 では、FILESTREAM 属性が導入されています。これはデータ型ではなく、列で定義できる属性であるため、大きな値のデータをデータベースではなくファイルシステムに格納できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
[ADO.NET での大きな値 (max) データの変更](modify-large-value-max-data.md)  
大きな値のデータ型を操作する方法について説明します。  
  
[FILESTREAM データ](filestream-data.md)  
FILESTREAM 属性を使用して SQL Server 2008 に格納されている大きな値のデータを操作する方法について説明します。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server のデータ型と ADO.NET](sql-server-data-types.md)
- [ADO.NET での SQL Server のデータ操作](sql-server-data-operations.md)
