---
title: FOR JSON での特殊文字のエスケープと制御文字
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5654a27a5457fe1d89fe76241c576f831dc9bf55
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095787"
---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>FOR JSON での特殊文字のエスケープと制御文字 (SQL Server)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  このトピックでは、SQL Server **SELECT** ステートメントの **FOR JSON** 句が JSON 出力で特殊文字をどのようにエスケープするか、また制御文字をどのように表すかについて説明します。  

> [!IMPORTANT]
> このページでは、Microsoft SQL Server の JSON の組み込みサポートについて説明します。 JSON のエスケープとエンコードの全般情報については、JSON RFC - [https://www.ietf.org/rfc/rfc4627.txt](https://www.ietf.org/rfc/rfc4627.txt) のセクション 2.5 を参照してください。

## <a name="escaping-of-special-characters"></a>特殊文字のエスケープ  
ソース データに特殊文字が含まれる場合、**FOR JSON** 句は JSON 出力の特殊文字を `\` でエスケープします。次の表をご覧ください。 このエスケープは、プロパティの名前と値の両方で行われます。  
  
|**特殊文字**|**エスケープされた出力**|  
|---------------------------|--------------------------|  
|引用符 (")|\\"|  
|円記号 (\\)|\\\\|  
|スラッシュ (/)|\\/|  
|バックスペース|\b|  
|改ページ|\f|  
|改行|\n|  
|キャリッジ リターン|\r|  
|水平タブ|\t|  
  
## <a name="control-characters"></a>制御文字。  
ソース データに制御文字が含まれる場合、**FOR JSON** 句は JSON 出力の制御文字を `\u<code>` 形式でエンコードします。次の表をご覧ください。  
  
|**制御文字**|**エンコードされた出力**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|[...]|[...]|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>例  
 次は、特殊文字と制御文字の両方を含むソース データの **FOR JSON** 出力の例です。  
  
 クエリ:  
  
```sql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 結果:  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>参照  
 [FOR JSON を使用してクエリ結果を JSON として書式設定する &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[FOR 句](../../t-sql/queries/select-for-clause-transact-sql.md)
