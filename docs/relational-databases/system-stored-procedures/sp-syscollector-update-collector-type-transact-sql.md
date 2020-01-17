---
title: sp_syscollector_update_collector_type (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collector_type_TSQL
- sp_syscollector_update_collector_type
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 3c414dfd-d9ca-4320-81aa-949465b967bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 393b5622964ea3f240d31a2a90c555f7020c500d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010542"
---
# <a name="spsyscollectorupdatecollectortype-transact-sql"></a>sp_syscollector_update_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  コレクション項目のコレクター型を更新します。 指定された名前およびコレクター型の GUID では、収集とアップロード パッケージ、パラメーター スキーマ、パラメーター フォーマッタ スキーマなど、コレクター型の構成を更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_update_collector_type [ @collector_type_uid = ] 'collector_type_uid' OUTPUT  
          , [ @name = ] 'name'  
          , [ @parameter_schema = ] 'parameter_schema'  
          , [ @collection_package_id = ] collection_package_id  
          , [ @upload_package_id = ] upload_package_id  
```  
  
## <a name="arguments"></a>引数  
`[ @collector_type_uid = ] 'collector_type_uid'` コレクター型の GUID です。 *collector_type_uid*は**uniqueidentifier**、しする場合は NULL それが自動的に作成され出力として返されます。  
  
`[ @name = ] 'name'` コレクター型の名前です。 *名前*は**sysname**と指定する必要があります。  
  
`[ @parameter_schema = ] 'parameter_schema'` このコレクター型の XML スキーマです。 *parameter_schema*は**xml**し、特定のコレクター型で必要になります。 必要ない場合、この引数は NULL を指定できます。  
  
`[ @collection_package_id = ] collection_package_id` ローカル一意識別子が指すは、[!INCLUDE[ssIS](../../includes/ssis-md.md)]コレクション パッケージのコレクション セットによって使用されます。 *collection_package_id*は**uniqueidentifer**必要があります。 値を取得する*collection_package_id*、msdb データベースの dbo.syscollector_collector_types システム ビューに対してクエリします。  
  
`[ @upload_package_id = ] upload_package_id` ローカル一意識別子が指すは、[!INCLUDE[ssIS](../../includes/ssis-md.md)]コレクション セットによって使用されるパッケージをアップロードします。 *upload_package_id*は**uniqueidentifier**必要があります。 値を取得する*upload_package_id*、msdb データベースの dbo.syscollector_collector_types システム ビューに対してクエリします。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **dc_admin** (EXECUTE 権限) を持つ固定データベース ロール。  
  
## <a name="example"></a>例  
 次の例では、ジェネリック T-SQL Query コレクター型を更新します (この例では、ジェネリック T-SQL Query コレクター型の既定のスキーマを使用しています)。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collector_type  
@collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
@name = 'Generic T-SQL Query Collector Type',  
@parameter_schema = '<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="DataCollectorType">  
  <xs:element name="TSQLQueryCollector">  
<xs:complexType>  
  <xs:sequence>  
<xs:element name="Query" minOccurs="1" maxOccurs="unbounded">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Value" type="xs:string" />  
  <xs:element name="OutputTable" type="xs:string" />  
</xs:sequence>  
  </xs:complexType>  
</xs:element>  
<xs:element name="Databases" minOccurs="0" maxOccurs="1">  
  <xs:complexType>  
<xs:sequence>  
  <xs:element name="Database" minOccurs="0" maxOccurs="unbounded" type="xs:string" />  
</xs:sequence>  
<xs:attribute name="UseSystemDatabases" type="xs:boolean" use="optional" />  
<xs:attribute name="UseUserDatabases" type="xs:boolean" use="optional" />  
  </xs:complexType>  
</xs:element>  
  </xs:sequence>  
</xs:complexType>  
  </xs:element>  
</xs:schema>',  
@collection_package_id = '292B1476-0F46-4490-A9B7-6DB724DE3C0B',  
@upload_package_id = '6EB73801-39CF-489C-B682-497350C939F0';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
