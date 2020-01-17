---
title: Teradata データ型のサポート |Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f83f028772a93dbd2104d9f449fcd7aa3b1be0d8
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543010"
---
# <a name="data-type-support"></a>データ型のサポート

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

SSIS コンポーネントでは、Teradata Parallel Transporter API (TPT API) を使用して Teradata データベースとの間でデータを読み込み、転送します。そのため、SSIS では、TPT API でサポートされているデータ型のみを使用できます。

> [!NOTE]
>
> Teradata の TIME、TIMESTAMP、INTERVAL データ型は、固定サイズの文字列として TPT API によって処理されます。 これらは、Teradata 用の SSIS コンポーネントによって文字列として処理されます。

## <a name="data-type-mapping"></a>データ型マッピング

次の表は、Teradata データベースのデータ型と、SSIS データ型に対する既定のマッピングを示しています。 サポートされていない Teradata データ型についても示されています。

|SQL データ型|SSIS データ型|
|:-|:-|
|DECIMAL、NUMERIC|DT_NUMERIC|
|BYTEINT|DT_I1|
|SMALLINT|DT_I2|
|INTEGER|DT_I4|
|FLOAT、REAL、DOUBLE PRECISION|DT_R8|
|DATE|DT_DBDATE|
|TIME<br>TIME(n)|DT_STR|
|timestamp<br>TIMESTAMP (n)|DT_STR|
|TIME WITH TIMEZONE<br>TIME(n) WITH TIMEZONE|DT_STR|
|TIMESTAMP WITH TIMEZONE<br>TIMESTAMP(n) WITH TIMEZONE|DT_STR|
|INTERVAL YEAR<br>INTERVAL YEAR (n)|DT_STR|
|INTERVAL YEAR TO MONTH<br>INTERVAL YEAR (n) TO MONTH|DT_STR|
|INTERVAL MONTH<br>INTERVAL MONTH (n)|DT_STR|
|INTERVAL DAY<br>INTERVAL DAY (n)|DT_STR|
|INTERVAL DAY TO HOUR<br>INTERVAL DAY (n) TO HOUR|DT_STR|
|INTERVAL DAY TO MINUTE<br>INTERVAL DAY (n) TO MINUTE|DT_STR|
|INTERVAL DAY TO SECOND<br>INTERVAL DAY (n) TO SECOND<br>INTERVAL DAY TO SECOND (m)<br>INTERVAL DAY (n) TO SECOND (m)|DT_STR|
|INTERVAL HOUR<br>INTERVAL HOUR (n)|DT_STR|
|INTERVAL HOUR TO MINUTE<br>INTERVAL HOUR (n) TO MINUTE|DT_STR
|INTERVAL HOUR TO SECOND<br>INTERVAL HOUR (n) TO SECOND<br>INTERVAL HOUR TO SECOND (m)<br>INTERVAL HOUR (n) TO SECOND (m)|DT_STR|
|INTERVAL MINUTE<br>INTERVAL MINUTE (n)|DT_STR|
|INTERVAL MINUTE TO SECOND<br>INTERVAL MINUTE (n) TO SECOND<br>INTERVAL MINUTE TO SECOND (m)<br>INTERVAL MINUTE (n) TO SECOND (m)|DT_STR|
|INTERVAL SECOND<br>INTERVAL SECOND (n)<br>INTERVAL SECOND (n,m)|DT_STR|
|PERIOD(DATE)|DT_STR|
|PERIOD(TIME)|DT_STR|
|NUMBER|DT_STR|
|CHARACTER|DT_STR|
|VARCHAR|DT_STR (Unicode 文字セットの場合は DT_WSTR)<br>**注**:<br> サポートされている VARCHAR の最大長は 32000 です。 <br> DT_STR の許容最大長は 8000 文字、DT_WSTR は 4000 文字です。 これを超えた場合、データは切り捨てられます。|
|LONG VARCHAR|サポートされていません|
|CLOB|サポートされていません|
|BYTE|DT_BYTES<br>**注**:許容最大長は 8000 バイトです。 これを超えた場合、データは切り捨てられます。|
|VARBYTE|DT_BYTES<br>**注**:許容最大長は 8000 バイトです。 これを超えた場合、データは切り捨てられます。|
|BLOB|サポートされていません|

## <a name="next-steps"></a>次のステップ

- [Teradata 接続マネージャー](teradata-connection-manager.md)を構成する
- [Teradata ソース](teradata-source.md)を構成する
- [Teradata 転送先](teradata-destination.md)を構成する
- ご質問がある場合は、[Tech Community](https://aka.ms/AA6iwdw) を参照してください。
