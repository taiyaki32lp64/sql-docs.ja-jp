---
title: OLE DB のプロパティについて |Microsoft Docs
description: OLE DB プロパティについて
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- OLE DB Driver for SQL Server, properties
- properties [OLE DB]
- property values [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 53d34483d8af029dd147b82da7611ddec616d641
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995055"
---
# <a name="about-ole-db-properties"></a>OLE DB プロパティについて
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  コンシューマーは、プロパティ値を設定することで、特定のオブジェクトの動作を要求します。 たとえば、プロパティを使用して、行セットによって公開されるインターフェイスを指定します。 コンシューマーは、プロパティ値を取得して、行セット、セッション、データ ソース オブジェクトなど、オブジェクトの機能を判断します。  
  
 各プロパティには、値、データ型、説明、および読み取り/書き込み属性があります。また、行セット プロパティの場合は、列単位で適用できるかどうかを示すインジケーターがあります。  
  
 プロパティは GUID およびプロパティ ID を表す整数によって識別されます。 プロパティ セットは、同じ GUID を共有するすべてのプロパティのセットです。 OLE DB Driver for SQL Server には、あらかじめ定義されている OLE DB プロパティ セットに加えて、プロバイダー固有のプロパティ セットと、そのセット内のプロパティが実装されています。 各プロパティは、1 つ以上のプロパティ グループに属しています。 プロパティ グループは、特定のオブジェクトに適用されるすべてのプロパティをグループ化したものです。 プロパティ グループには、初期化プロパティ グループ、データ ソース プロパティ グループ、セッション プロパティ グループ、行セット プロパティ グループ、テーブル プロパティ グループ、列プロパティ グループなどがあります。 これらの各プロパティ グループに、プロパティが含まれています。  
  
 プロパティ値を設定するには、次の手順を実行します。  
  
1.  値を設定するプロパティを決定します。  
  
2.  目的のプロパティを含むプロパティ セットを決定します。  
  
3.  目的のプロパティ セットごとに 1 つ、DBPROPSET 構造体の配列を割り当てます。  
  
4.  プロパティ セットごとに DBPROP 構造体の配列を割り当てます。 各配列の要素数は、そのプロパティ セットに属するプロパティ (手順 1. で特定したプロパティ) の個数です。  
  
5.  プロパティごとに DBPROP 構造体に値を設定します。  
  
6.  プロパティ セットごとに DBPROPSET 構造体に情報 (プロパティ セット GUID、要素数、および対応する DBPROP 配列を指すポインター) を設定します。  
  
7.  要素数と DBPROPSET 構造体の配列を渡してメソッドを呼び出し、プロパティを設定します。  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のアプリケーションの作成](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [プロパティ [OLE DB]](https://go.microsoft.com/fwlink/?LinkId=112207)  
  
  
