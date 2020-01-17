---
title: xml_schema_namespace (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb3b19e67a4a85ef3f7a26d7ad792e7e39459302
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948037"
---
# <a name="xmlschemanamespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定された XML スキーマ コレクション内のすべてのスキーマまたは特定のスキーマを再構築します。 この関数は、 **xml** データ型のインスタンスを返します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>引数  
 *Relational_schema*  
 リレーショナル スキーマ名。 *Relational_schema* は **sysname** です。  
  
 *XML_schema_collection_name*  
 再構築する XML スキーマ コレクションの名前を指定します。 *XML_schema_collection_name* は **sysname** です。  
  
 *Namespace*  
 再構築する XML スキーマの名前空間 URI です。 上限は 1,000 文字です。 名前空間 URI を指定しない場合、XML スキーマ コレクション全体が再構築されます。 *名前空間*は **nvarchar(4000)** です。  
  
## <a name="return-types"></a>戻り値の型  
 **xml**  
  
## <a name="remarks"></a>Remarks  
 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) または [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) を使用してデータベース内の XML スキーマ コンポーネントをインポートする場合、検証に使用されたスキーマの情報が保持されます。 したがって、再構築されたスキーマは、元のスキーマ ドキュメントとは構文的に同じにならない可能性があります。 特に、コメント、空白、注釈は失われ、暗黙的な型の情報が明示されます。 たとえば、\<xs:element name="e1" /> は \<xs:element name="e1" type="xs:anyType"/> になります。 また、名前空間プレフィックスは保持されません。  
  
 名前空間のパラメーターを指定した場合、結果のスキーマ ドキュメントにはその名前空間内のすべてのスキーマ コンポーネントの定義が含まれます。それらのコンポーネントが異なるスキーマ ドキュメントまたは DDL のステップ、あるいはその両方に追加された場合であっても、同様です。  
  
 この関数を使用して、XML スキーマ ドキュメントを **sys.sys** XML スキーマ コレクションから構築することはできません。  
  
## <a name="examples"></a>使用例  
 次の例では、XML スキーマ コレクション `ProductDescriptionSchemaCollection` を、`AdventureWorks` データベース内の運用リレーショナル スキーマから取得します。  
  
```  
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [格納されている XML スキーマ コレクションの表示](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
