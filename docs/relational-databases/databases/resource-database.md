---
title: Resource データベース | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- system objects [SQL Server]
- read-only databases
- mssqlsystemresource.mdf file
- Resource database [SQL Server]
ms.assetid: d592b2b4-bc36-4eb9-9385-8fe4dff0dced
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5f6b63e0ff79f44b2900fb0f727436ed36401ee2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127457"
---
# <a name="resource-database"></a>Resource データベース
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Resource データベースは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に搭載されているすべてのシステム オブジェクトを格納する読み取り専用のデータベースです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム オブジェクト (sys.objects など) は、物理的には Resource データベースに保存されていますが、すべてのデータベースの sys スキーマに論理的に表示されます。 Resource データベースには、ユーザーのデータやユーザーのメタデータは保持されません。  
  
 Resource データベースが実装されたことで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいバージョンへのアップグレードを簡単かつ迅速に実行できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の以前のバージョンでは、アップグレードを行う場合、システム オブジェクトを削除してから再度作成する必要がありました。 現在は、すべてのシステム オブジェクトが Resource データベース ファイルに格納されるため、Resource データベース ファイルをローカル サーバーにコピーするだけで、アップグレードを完了できます。  
  
## <a name="physical-properties-of-resource"></a>Resource データベースの物理プロパティ  
 Resource データベースの物理ファイル名は、mssqlsystemresource.mdf および mssqlsystemresource.ldf です。 これらのファイルは \<*drive*>:\Program Files\Microsoft SQL Server\MSSQL\<version>.\<*instance_name*>\MSSQL\Binn\ に位置しており、移動してはなりません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各インスタンスには、関連する mssqlsystemresource.mdf ファイルが 1 つだけあり、このファイルが共有されることはありません。  
  
> [!WARNING]  
>  アップグレードとサービス パックにより、新しいリソース データベースが提供されることがあります。これは BINN フォルダーにインストールされます。 リソース データベースの場所の変更はサポートされておらず、お勧めしません。  
  
## <a name="backing-up-and-restoring-the-resource-database"></a>Resource データベースのバックアップと復元  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Resource データベースをバックアップできません。 ファイル ベースまたはディスク ベースのバックアップは、mssqlsystemresource.mdf ファイルをデータベース ファイルではなくバイナリ (.EXE) ファイルのように実行できますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用してバックアップを復元することはできません。 mssqlsystemresource.mdf のバックアップ コピーの復元は手動でのみ実行できます。また、現在の Resource データベースを古いバージョンや安全でない可能性のあるバージョンで上書きしないように注意する必要があります。  
  
> [!IMPORTANT]  
>  mssqlsystemresource.mdf のバックアップを復元した後、それ以降のすべての更新を適用し直す必要があります。  
  
## <a name="accessing-the-resource-database"></a>Resource データベースへのアクセス  
 Resource データベースの変更は、マイクロソフト カスタマー サポート サービス (CSS) のサポート スタッフの指示がある場合にのみ行ってください。 Resource データベースの ID は、常に 32767 です。 Resource データベースに関する他の重要な値には、バージョン番号とデータベースの最終更新時刻があります。  
  
 Resource **データベースの** **バージョン番号を確認するには、次のステートメントを使用します** 。  
  
```  
SELECT SERVERPROPERTY('ResourceVersion');  
GO  
```  
  
 Resource **データベースの** **最終更新時刻を確認するには、次のステートメントを使用します**。  
  
```  
SELECT SERVERPROPERTY('ResourceLastUpdateDateTime');  
GO  
```  
  
 **システム オブジェクトの SQL 定義にアクセスするには、次のように OBJECT_DEFINITION 関数を使用します。**  
  
```  
SELECT OBJECT_DEFINITION(OBJECT_ID('sys.objects'));  
GO  
```  
  
## <a name="related-content"></a>関連コンテンツ  
 [システム データベース](../../relational-databases/databases/system-databases.md)  
  
 [データベース管理者用の診断接続](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)  
  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
 [シングル ユーザー モードでの SQL Server の起動](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
