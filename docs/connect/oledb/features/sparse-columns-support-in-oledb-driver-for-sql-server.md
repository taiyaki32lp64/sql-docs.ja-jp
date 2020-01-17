---
title: OLE DB Driver for SQL Server のスパース列のサポート | Microsoft Docs
description: OLE DB Driver for SQL Server のスパース列のサポート
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7b617ecdbf2977372dbb006baaec4c791b988ef8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988906"
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server のスパース列のサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server では、スパース列がサポートされています。 の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]スパース列の詳細については、「[スパース列の使用](../../../relational-databases/tables/use-sparse-columns.md)」および「[列セットの使用](../../../relational-databases/tables/use-column-sets.md)」を参照してください。  
  
 OLE DB Driver for SQL Server でのスパース列のサポートの詳細については、[スパース列は OLE DB &#40;&#41;をサポート](../../oledb/ole-db/sparse-columns-support-ole-db.md)しています。  
  
 この機能を説明するサンプル アプリケーションについては、「[SQL Server データ プログラミング サンプル](https://msftdpprodsamples.codeplex.com/)」を参照してください。  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>スパース列のユーザーシナリオと SQL Server 用の OLE DB ドライバー  
 次の表は、スパース列を使用する SQL Server ユーザーの OLE DB ドライバーに関する一般的なユーザーシナリオをまとめたものです。  
  
|シナリオ|動作|  
|--------------|--------------|  
|**select\* from table**または IOpenRowset:: OpenRowset。|スパース **column_set** のメンバーでないすべての列と、スパース **column_set** のメンバーであるすべての NULL 以外の列の値を含む XML 列が返されます。|  
|名前で列を参照する。|スパース列かどうか、**column_set** のメンバーであるかどうかに関係なく、列を参照できます。|  
|XML 計算列を通じて **column_set** メンバー列にアクセスする。|スパース **column_set** のメンバーである列に、名前で **column_set** を選択してアクセスし、**column_set** 列の XML を更新して値を挿入および更新できます。<br /><br /> 値は、**column_set** 列のスキーマに準拠している必要があります。|  
|列制限のない DBSCHEMA_COLUMNS スキーマ行セットを使用して、テーブル内のすべての列のメタデータを取得します (OLE DB)。|**column_set** のメンバーでないすべての列について 1 つの行が返されます。 テーブルにスパース **column_set** がある場合は、そのスパースについて 1 つの行が返されます。<br /><br /> この場合、**column_set** のメンバーである列のメタデータは返されないことに注意してください。|  
|スパース列かどうか、**column_set** のメンバーかどうかに関係なく、すべての列のメタデータを取得する。 この場合、大量の行が返される可能性があります。|DBSCHEMA_COLUMNS_EXTENDED スキーマ行セットの IDBSchemaRowset:: GetRowset を呼び出します。|  
|**column_set** のメンバーである列についてのみメタデータを取得する。 この場合、大量の行が返される可能性があります。|DBSCHEMA_SPARSE_COLUMN_SET スキーマ行セットの IDBSchemaRowset:: GetRowset を呼び出します。|  
|列がスパース列かどうかを確認する。|DBSCHEMA_COLUMNS スキーマ行セットの SS_IS_SPARSE 列を調べます (OLE DB)。|  
|列が**column_set**であるかどうかを判断します。|DBSCHEMA_COLUMNS スキーマ行セットの SS_IS_COLUMN_SET 列を調べます。 または、IColumnsRowset:: GetColumnsRowset によって返された行セットの IColumnsinfo:: GetColumnInfo または DBCOLUMNFLAGS によって返された*dwFlags*を参照してください。 **column_set** 列の場合は DBCOLUMNFLAGS_SS_ISCOLUMNSET が設定されます。|  
|**column_set** を含まないテーブルに対して BCP でスパース列をインポートおよびエクスポートする。|以前のバージョンの OLE DB Driver for SQL Server の動作は変更されていません。|  
|**column_set** を含むテーブルに対して BCP でスパース列をインポートおよびエクスポートする。|**Column_set**は XML と同じ方法でインポートおよびエクスポートされます。つまり、 **varbinary (max)** としてバイナリ型としてバインドされている場合、または**char**型または**wchar**型としてバインドされている場合は**nvarchar (max)** として。<br /><br /> スパース **column_set** のメンバーである列は個別の列としてはエクスポートされず、**column_set** の値でのみエクスポートされます。|  
|BCP の**queryout**動作。|以前のバージョンの OLE DB Driver for SQL Server から明示的に名前付けされた列を処理することは、変更されていません。<br /><br /> スキーマが異なる列の間のインポートおよびエクスポートを含むシナリオでは、特別な処理が必要になる場合があります。<br /><br /> BCP の詳細については、後の「一括コピー (BCP) によるスパース列のサポート」を参照してください。|  
  
## <a name="down-level-client-behavior"></a>下位クライアントの動作  
 下位クライアントでは、SQLColumns および DBSCHMA_COLUMNS でメタデータが返されるのは、スパース **column_set** のメンバーでない列のみです。
  
 下位クライアントでは、スパース **column_set** のメンバーである列に名前でアクセスできます。[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] クライアントでは、XML 列として **column_set** 列にアクセスできます。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>一括コピー (BCP) によるスパース列のサポート  
 OLE DB の BCP API には、スパース列や **column_set** 機能のための変更はありません。  
  
 テーブルに **column_set** がある場合、スパース列は個別の列として処理されません。 すべてのスパース列の値は、XML 列と同じ方法でエクスポートされる**column_set**の値に含まれます。つまり、 **varbinary (max)** はバイナリ型としてバインドされます。 **char**型または**wchar**型としてバインドされている場合は、 **nvarchar (max)** として。 インポート時には、 **column_set**値が**column_set**のスキーマに準拠している必要があります。  
  
 **queryout** の操作については、明示的に参照されている列の処理方法は変更されていません。 **column_set** 列の動作は XML 列と同じで、名前で参照されているスパース列の処理には、列がスパース列であることの影響はありません。  
  
 ただし、**queryout** をエクスポートに使用する場合に、スパース列セットのメンバーであるスパース列を名前で参照すると、同じ構造のテーブルへの直接インポートができなくなります。 これは、BCP では **select \*** 操作と一貫したメタデータがインポートのために使用され、そのメタデータを **column_set** メンバー列と対応させることはできないからです。 **column_set** メンバー列を個別にインポートするには、目的の **column_set** 列を参照するテーブルのビューを定義して、そのビューを使用してインポート操作を行う必要があります。  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server](../../oledb/oledb-driver-for-sql-server.md)  
  
  
