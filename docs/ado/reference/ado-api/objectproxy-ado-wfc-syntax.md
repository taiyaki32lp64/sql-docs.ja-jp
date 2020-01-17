---
title: ObjectProxy (ADO - WFC 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 485d011fa6762acd04cad54ff7fffc8d8136e063
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917957"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO - WFC 構文)
**ObjectProxy**オブジェクトは、サーバーを表しており、によって返される、 **createObject**のメソッド、 [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)オブジェクト。 ObjectProxy クラスが 1 つのメソッド、**呼び出す**サーバーでメソッドを呼び出すし、呼び出しから結果のオブジェクトを返すことができます。  
  
 **package com.ms.wfc.data**  
  
## <a name="methods"></a>メソッド  
  
### <a name="call-method-adowfc-syntax"></a>Call メソッド (ADO と WFC 構文)  
 ObjectProxy によって表されるサーバー上のメソッドを呼び出します。 必要に応じて、メソッドの引数は、オブジェクトの配列として渡すことがあります。  
  
#### <a name="syntax"></a>構文  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>戻り値  
 オブジェクト  
 メソッドを呼び出し、結果のオブジェクト。  
  
#### <a name="parameters"></a>パラメーター  
 *ObjectProxy*  
 **ObjectProxy**サーバーを表すオブジェクト。  
  
 *method*  
 サーバーで呼び出すメソッドの名前を含む文字列。  
  
 *引数*  
 任意。 サーバー上のメソッドの引数であるオブジェクトの配列。 Java データ型は、サーバー上の使用に適したデータ型に自動的に変換されます。
