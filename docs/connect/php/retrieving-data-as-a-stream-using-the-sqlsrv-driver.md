---
title: SQLSRV ドライバーを使用してデータをストリームとして取得する | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 17dc9129-04cd-430c-b5b3-82824116425d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b83188359489759f50b2929de769721d627c15d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992899"
---
# <a name="retrieving-data-as-a-stream-using-the-sqlsrv-driver"></a>SQLSRV ドライバーを使用してデータをストリームとして取得する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

ストリームとしてのデータの取得は、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の SQLSRV ドライバーでのみ使用でき、PDO_SQLSRV ドライバーでは使用できません。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] は、大量のデータを取得するためにストリームを利用します。 このセクションのトピックでは、データをストリームとして取得する方法について詳しく説明します。  
  
次の手順に、データをストリームとして取得する方法をまとめています。  
  
1.  [sqlsrv_query](../../connect/php/sqlsrv-query.md) または [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md) の組み合わせで Transact-SQL クエリを準備して実行します。  
  
2.  [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) を使用して、結果セットの次の行に移動します。  
  
3.  [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) を使用して、行からフィールドを取得します。 関数呼び出しの 3 番目のパラメーターとして **SQLSRV_PHPTYPE_STREAM(<encoding>)** を使用して、データをストリームとして取得することを指定します。 次の表は、エンコーディングおよびそれらの記述を指定するために使用する定数を示しています。  
  
    |SQLSRV 定数|[説明]|  
    |-------------------|---------------|  
    |SQLSRV_ENC_BINARY|データは、エンコードまたは変換されず、生のバイト ストリームとしてサーバーから返されます。|  
    |SQLSRV_ENC_CHAR|データは、システムの Windows ロケール設定のコード ページで指定されている 8 ビット文字で返されます。 任意のマルチバイト文字またはこのコード ページにマップされていない文字は、1 バイトの疑問符 (?) 文字に置き換えられます。|  
  
> [!NOTE]  
> 一部のデータ型は、既定ではストリームとして返されます。 詳細については、「 [Default PHP Data Types](../../connect/php/default-php-data-types.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|---------|---------------|  
|[SQLSRV ドライバーを使用したストリームでのデータ型のサポート](../../connect/php/data-types-with-stream-support-using-the-sqlsrv-driver.md)|ストリームとして取得できる SQL Server データ型を一覧表示します。|  
|[方法: SQLSRV ドライバーを使用したストリームとしての文字データの取得](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)|文字データをストリームとして取得する方法を説明します。|  
|[方法: SQLSRV ドライバーを使用してバイナリ データをストリームとして取得する](../../connect/php/how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver.md)|バイナリ データをストリームとして取得する方法を説明します。|  
  
## <a name="see-also"></a>参照  
[データの取得](../../connect/php/retrieving-data.md)

[定数 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
