---
title: テーブル値パラメーター (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67991d5bd50b9612b8f3eaff01d37eef581b22f5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761639"
---
# <a name="table-valued-parameters-ole-db"></a>テーブル値パラメーター (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ここでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでのテーブル値パラメーターのサポートについて説明します。 その他の概要については、「[テーブル値パラメーター &#40;&#41;SQL Server Native Client](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)」を参照してください。 サンプルについては、「[テーブル値パラメーター &#40;の&#41;使用 OLE DB](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 現時点では、複数行データを、パラメーター セット (**ICommand::Execute** の DBPARAMS パラメーター) と共にプロシージャのパラメーターとしてサーバーに送信できます。 パラメーター セットを使用する場合、セットの各要素は、個別のリモート プロシージャ コール (RPC) の要求でサーバーに送信する必要があります。 テーブル値パラメーターの機能は似ていますが、サーバーとの統合はより緊密になっています。 これにより、RPC 要求の数が減少し、サーバーでセットベースの操作が可能になります。  
  
 テーブル値パラメーターは OLE DB**行セット**オブジェクトとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでサポートされています。 コンシューマーが任意の**行セット**オブジェクト ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを使用するクライアントアプリケーション) を、テーブル値パラメーターのパラメーターのプレースホルダーとして提供できます。 テーブル値パラメーターは、他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パラメーターの型と同じように扱われます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって、作成、検索、指定、バインド、およびスキーマのインターフェイスが提供されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [テーブル値パラメーターの行セットの作成](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [テーブル値パラメーターの型探索](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [テーブル値パラメーターを含むコマンドの実行](../../relational-databases/native-client-ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [テーブル値パラメーターへのデータの挿入](../../relational-databases/native-client-ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [OLE DB テーブル値パラメーター向けに変更されたスキーマ行セット](../../relational-databases/native-client-ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB テーブル値パラメーターの型のサポート](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB テーブル値パラメーターの型のサポート (メソッド)](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB テーブル値パラメーターの型のサポート (プロパティ)](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;OLE DB&#41; ](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
