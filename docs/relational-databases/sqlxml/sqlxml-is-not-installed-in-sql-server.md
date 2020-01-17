---
title: SQL Server で SQLXML がインストールされない
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c666d02449190ca6a88ac43c96ab7aee9676be4d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242653"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQL Server で SQLXML がインストールされない
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] より前のバージョンでは、SQLXML 4.0 は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に付属してリリースされ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのバージョン ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] を除く) の既定のインストールに含まれていました。 
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、SQLXML の最新バージョン (SQLXML 4.0 SP1) が含まれないようになりました。 SQLXML 4.0 SP1 をインストールするには、 [sqlxml 4.0 sp1 のインストール場所](https://www.microsoft.com/download/details.aspx?id=30403)からダウンロードします。  
  
 アプリケーションがで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]実行され、sqlxml 4.0 が必要な場合は、SQLXML 4.0 SP1 をダウンロードしてインストールする必要があります。  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>SQLOLEDB および SQL Server Native Client OLE DB プロバイダーを使用した場合の新しいデータ型による SQLXML 4.0 SP1 の動作  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]では次のデータ型が導入されました。 SQLXML を使用する開発者は、を使用することをお勧めします。  
  
-   **予定**  
  
-   **ごと**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 SQLOLEDB または Native Client OLE DB のいずれか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]SQLXML 4.0 SP1 を使用する場合、これらの型は開発者に文字列として表示されます。 SQLXML 4.0 SP1 では、Native Client OLE DB Provider 11.0 以降で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用する場合に、これら4つの新しいデータ型を組み込みスカラー型として有効にします。 SQLXML 4.0 SP1 をダウンロードしないと、これらの型を文字列以外の型にマッピングした場合、一部のデータが切り捨てられる可能性があります。 たとえば、 **DateTime2**を**xsd: date**にマッピングすると、データは3.33 ミリ秒[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]の**DateTime**有効桁数に切り捨てられます。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0 のプログラミング概念](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
