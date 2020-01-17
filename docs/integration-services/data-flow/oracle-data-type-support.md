---
title: Microsoft Connector for Oracle でのデータ型のサポート | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c28efd8106056ea900fef0cd57791837cf79e21a
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553228"
---
# <a name="microsoft-connector-for-oracle-data-type-support"></a>Microsoft Connector for Oracle でのデータ型のサポート

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Oracle 用の SSIS コンポーネントでは、Oracle のすべてのデータ型はサポートされていません。 SSDT でパッケージを設計するとき、サポートされていないデータ型の列には警告が表示され、列のマッピングから削除されます。 サポートされていないデータ型の列にデータを読み込むことはできません。

## <a name="data-type-mapping"></a>データ型マッピング

次の表は、Oracle データベースのデータ型と、SSIS データ型に対する既定のマッピングを示しています。 サポートされていない Oracle データ型についても示されています。

|Oracle データベース データ型|SSIS データ型|コメント|
|:-|:-|:-|
|VARCHAR2|DT_STR||
|NVARCHAR2|DT_WSTR||
|CHAR|DT_STR||
|NUMBER|DT_R8|これは、特定の有効桁数と小数点以下桁数を持つ DT_NUMERIC に変更できます。 有効桁数と小数点以下桁数は、ユーザーが必要に応じて定義します。 出力は、固定有効桁数と小数点以下桁数を持つ数値としての列データになります。|
|NUMBER(P, S)| 小数点以下桁数が 0 の場合、有効桁数 (P) に従います。 <li> DT_I1 <Li> DT_I2 <Li> DT_I4 <Li> DT_NUMBERIC(P,0)||
||DT_NUMERIC(P,S)||
|DATE|DT_DBTIMESTAMP||
|<li>timestamp <li>TIMESTAMP WITH TIME ZONE <li>INTERVAL YEAR TO MONTH <li>INTERVAL DAY TO SECOND <li>TIMESTAMP WITH LOCAL TIME ZONE|DT_STR||
|RAW|DT_BYTES||
|CLOB|DT_TEXT|CLOB、NCLOB、および BLOB の各データ型は配列モードでのみサポートされ、高速読み込みモードではサポートされていません。|
|NCLOB|DT_NTEXT||
|BLOB|DT_IMAGE||
|UROWID|サポートされていません||
|REF|サポートされていません||
|BFILE|サポートされていません||
|LONG|サポートされていません||
|LONG RAW|サポートされていません||
|ROWID|サポートされていません||
|ユーザー定義型 (オブジェクト型、VARRAY、入れ子になったテーブル)|サポートされていません||

## <a name="next-steps"></a>次の手順

- [Oracle 接続マネージャー](oracle-connection-manager.md)を構成する。
- [Oracle ソース](oracle-source.md)を構成する。
- [Oracle 変換先](oracle-destination.md)を構成する。
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA5u35j)を参照してください。
