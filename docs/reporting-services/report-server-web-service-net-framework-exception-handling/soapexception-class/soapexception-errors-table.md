---
title: SoapException エラー テーブル | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- SoapException class
ms.assetid: 3dbf1b5a-bd2a-4385-925d-5d095d72014c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 95427ddaa6d220afe3397a138f9b5baa085f324d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62991550"
---
# <a name="soapexception-errors-table"></a>SoapException エラー テーブル
  レポート サーバーでは、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] で発生するエラーに基づいて、SOAP 例外のエラーとエラー メッセージが生成されます。 次の表は、レポート サーバー Web サービスの **SoapException** を使用してメソッドからアクセスできるエラーを示します。 例外をスローする 1 つまたは複数のメソッド別に分類されています。  
  
|メソッド|エラー コード|  
|-----------------|----------------|  
|**ALL**|**rsEvaluationCopyExpired**|  
|**ALL**|**rsFailedToDecryptConfigInformation**|  
|**ALL**|**rsInvalidRSEditionConfiguration**|  
|**ALL**|**rsReportServerNotActivated**|  
|**ALL**|**rsServerBusy**|  
|**ALL**|**rsReportServerServiceUnavailable**|  
|**ALL**|**rsReportServerDisabled**|  
|**GetPermissions**、**GetRenderResource**、**GetSystemPermissions**、**ListEvents**、および **ListSecureMethods** を除く**すべてのメソッド**|**rsAccessDenied**|  
|**CreateBatch**、**ExecuteBatch**、**GetSystemPolicies**、**GetSystemPermissions**、**GetSystemProperties**、**ListEvents**、**ListJobs**、**ListRoles**、**ListSchedules**、**ListSecureMethods**、**ListSubscriptions**、**ListSystemRoles**、**ListSystemTasks**、**ListTasks** を除く**すべてのメソッド**|**rsMissingParameter**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateReportHistorySnapshot**、**CreateResource**、**CreateSubscription**、**DeleteItem**、**DeleteReportHistorySnapshot**、**DisableDataSource**、**EnableDataSource**、**FindItems**、**FlushCache**、**GetCacheOptions**、**GetDataSourceContents**、**GetExecutionOptions**、**GetPermissions**、**GetPolicies**、**GetProperties**、**GetReportDataSourcePrompts**、**GetReportDataSources**、**GetReportDefinition**、**GetReportHistoryLimit**、**GetReportHistoryOptions**、**GetReportLink**、**GetReportParameters**、**GetResourceContents**、**GetRoleProperties**、**GetServerDateTime**、**IheritParentSecurity**、**ListChildren**、**ListLinkedReports**、**ListReportHistory**、**ListReportsUsingDataSource**、**ListSchedules**、**ListSubscriptions**、**ListSubscriptionsUsingDataSource**、**MoveItem**、**Render**、**RenderStream**、**SetCacheOptions**、**SetDataSourceContents**、**SetExecutionOptions**、**SetPolicies**、**SetProperties**、**SetReportDataSources**、**SetReportDefinition**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetReportLink**、**SetReportParameters**、**SetResourceContents**、**UpdateReportExecutionSnapshot**、**ValidateExtensionSettings**|**rsItemNotFound**|  
|**CancelBatch**、**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateReportHistorySnapshot**、**CreateResource**、**CreateRole**、**CreateSchedule**、**CreateSubscription**、**DeleteItem**、**DeleteReportHistorySnapshot**、**DeleteRole**、**DeleteSchedule**、**DeleteSubscription**、**DisableDataSource**、**EnableDataSource**、**ExecuteBatch**、**FindItems**、**FlushCache**、**GetResourceContents**、**GetServerDateTime**、**MoveItem**、**PauseSchedule**、**ResumeSchedule**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetDataSourceContents**、**SetExecutionOptions**、**SetPolicies**、**SetProperties**、**SetReportDataSources**、**SetReportDefinition**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetReportLink**、**SetReportParameters**、**SetResourceContents**、**SetRoleProperties**、**SetScheduleProperties**、**SetSubscriptionProperties**、**SetSystemPolicies**、**SetSystemProperties**、**UpdateReportExecutionSnapshot**、**ValidateExtensionSettings**|**rsBatchNotFound**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateReportHistorySnapshot**、**CreateResource**、**CreateSubscription**、**DeleteItem**、**DeleteReportHistorySnapshot**、**DisableDataSource**、**EnableDataSource**、**FindItems**、**FlushCache**、**GetCacheOptions**、**GetDataSourceContents**、**GetExecutionOptions**、**GetItemType**、**GetPermissions**、**GetPolicies**、**GetProperties**、**GetReportDataSourcePrompts**、**GetReportDataSources**、**GetReportDefinition**、**GetReportHistoryLimit**、**GetReportHistoryOptions**、**GetReportLink**、**GetResourceContents**、**GetServerDateTime**、**IheritParentSecurity**、**ListChildren**、**ListLinkedReports**、**ListReportHistory**、**ListSchedules**、**ListSubscriptionsUsingDataSource**、**MoveItem**、**Render**、**RenderStream**、**SetCacheOptions**、**SetDataSourceContents**、**SetExecutionOptions**、**SetPolicies**、**SetProperties**、**SetReportDataSources**、**SetReportDefinition**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetReportLink**、**SetReportParameters**、**SetResourceContents**、**SetSubscriptionProperties**、**UpdateReportExecutionSnapshot**、**ValidateExtensionSettings**|**rsInvalidItemPath**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateReportHistorySnapshot**、**CreateResource**、**CreateSubscription**、**DeleteReportHistorySnapshot**、**DisableDataSource**、**EnableDataSource**、**FindItems**、**FlushCache**、**GetCacheOptions**、**GetDataSourceContents**、**GetExecutionOptions**、**GetReportDataSourcePrompts**、**GetReportDataSources**、**GetReportDefinition**、**GetReportHistoryLimit**、**GetReportHistoryOptions**、**GetReportLink**、**GetReportParameters**、**GetResourceContents**、**GetServerDateTime**、**GetSystemProperties**、**ListChildren**、**ListLinkedReports**、**ListReportHistory**、**ListReportsUsingDataSource**、**ListSchedules**、**ListSubscriptions**、**ListSubscriptionsUsingDataSource**、**MoveItem**、**Render**、**RenderStream**、**SetCacheOptions**、**SetDataSourceContents**、**SetExecutionOptions**、**SetReportDataSources**、**SetReportDefinition**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetReportLink**、**SetReportParameters**、**SetResourceContents**、**UpdateReportExecutionSnapshot**、**ValidateExtensionSettings**|**rsWrongItemType**|  
|**CreateReport**、**CreateResource**、**DeleteReportHistorySnapshot**、**DeleteSchedule**、**DeleteSubscription**、**GetDataDrivenSubscriptionProperties**、**GetSubscriptionProperties**、**ListChildren**、**ListScheduledReports**、**PauseSchedule**、**Render**、**RenderStream**、**ResumeSchedule**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetScheduleProperties**、**SetSubscriptionProperties**|**rsParameterTypeMismatch**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateSchedule**、**CreateSubscription**、**FindItems**、**GetReportParameters**、**PrepareQuery**、**Render**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetDataSourceContents**、**SetPolicies**、**SetReportDataSources**、**SetReportParameters**、**SetScheduleProperties**、**SetSubscriptionProperties**、**SetSystemPolicies**|**rsMissingElement**|  
|**CreateDataDrivenSubscription**、**CreateDataSource**、**CreateSchedule**、**CreateSubscription**、**PrepareQuery**、**Render**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetDataSourceContents**、**SetProperties**、**SetReportDataSources**、**SetReportParameters**、**SetScheduleProperties**、**SetSubscriptionProperties**、**SetSystemProperties**|**rsInvalidElement**|  
|**CreateDataDrivenSubscription**、**CreateSchedule**、**CreateSubscription**、**FindItems**、**GetRenderResource**、**PrepareQuery**、**Render**、**RenderStream**、**SetCacheOptions**、**SetDataDrivenSubscriptionProperties**、**SetExecutionOptions**、**SetProperties**、**SetReportHistoryOptions**、**SetReportParameters**、**SetScheduleProperties**、**SetSubscriptionProperties**、**SetSystemProperties**|**rsElementTypeMismatch**|  
|**CreateDataSource**、**CreateRole**、**GetDataDrivenSubscriptionProperties**、**GetRenderResource**、**ListExtensions**、**Render**、**SetDataDrivenSubscriptionProperties**、**SetDataSourceContents**、**SetExecutionOptions**、**SetReportHistoryLimit**、**SetReportHistoryOptions**、**SetScheduleProperties**|**rsInvalidParameter**|  
|**CreateDataDrivenSubscription**、**CreateReportHistorySnapshot**、**CreateSubscription**、**PrepareQuery**、**SetDataDrivenSubscriptionProperties**、**SetExecutionOptions**、**SetReportHistoryOptions**、**SetSubscriptionProperties**|**rsInvalidDataSourceCredentialSetting**|  
|**CreateDataDrivenSubscriptionProperties**、**CreateReportHistorySnapshot**、**CreateSchedule**、**CreateSubscription**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**、**UpdateReportExecutionSnapshot**|**rsReportParameterValueNotSet**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**GetExtensionSettings**、**GetRenderResource**、**Render**、**RenderStream**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsMultipleExtensionsFoundInAssembly**|  
|**CreateDataDrivenSubscriptionProperties**、**CreateSubscription**、**Render**、**SetCacheOptions**、**SetExecutionOptions**、**SetReportParameters**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsReportParameterTypeMismatch**|  
|**CreateSchedule**、**CreateSubscription**、**DeleteSchedule**、**PauseSchedule**、**ResumeSchedule**、**SetCacheOptions**、**SetExecutionOptions**、**SetScheduleProperties**、**SetSubscriptionProperties**|**rsSchedulerNotResponding**|  
|**DeleteSchedule**、**GetScheduleProperties**、**ListScheduledReports**、**PauseSchedule**、**ResumeSchedule**、**SetCacheOptions**、**SetExecutionOptions**、**SetScheduleProperties**|**rsScheduleNotFound**|  
|**CreateDataDrivenSubscriptionProperties**、**CreateSubscription**、**Render**、**SetReportParameters**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsReadOnlyReportParameter**|  
|**CreateDataDrivenSubscriptionProperties**、**CreateSubscription**、**GetReportParameters**、**Render**、**SetReportParameters**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsUnknownReportParameter**|  
|**DeleteSubscription**、**GetDataDrivenSubscriptionProperties**、**GetSubscriptionProperties**、**SetDataDrivenSubscriptionProperties**、**SetExecutionOptions**、**SetSubscriptionProperties**|**rsSubscriptionNotFound**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**GetExtensionSettings**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsDeliveryExtensionNotFound**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**GetExtensionSettings**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsDeliveryError**|  
|**CreateDataDrivenSubscription**、**GetDataDrivenSubscriptionProperties**、**PrepareQuery**、**SetDataDrivenSubscriptionProperties**|**rsSecureConnectionRequired**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsCannotSubscribeToEvent**|  
|**CreateDataDrivenSubscription**、**CreateSubscription**、**FireEvent**、**SetDataDrivenSubscriptionProperties**、**SetSubscriptionProperties**|**rsUnknownEventType**|  
|**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateResource**、**MoveItem**|**rsItemPathLengthExceeded**|  
|**CopyItem**、**CreateFolder**、**CreateReport**、**CreateResource**、**DeleteItem**|**rsReservedItem**|  
|**CreateDataSource**、**SetDataSourceContents**、**SetReportDataSources**|**rsInvalidElementCombination**|  
|**SetCacheOptions**、**SetExecutionOptions**、**SetReportHistoryOptions**|**rsInvalidParameterCombination**|  
|**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateResource**、**MoveItem**|**rsInvalidItemName**|  
|**CreateDataSource**、**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateResource**、**MoveItem**|**rsItemAlreadyExists**|  
|**CreateFolder**、**CreateLinkedReport**、**CreateReport**、**CreateResource**、**SetProperties**|**rsReadOnlyProperty**|  
|**GetPolicies**、**GetSystemPolicies**、**SetPolicies**、**SetSystemPolicies**|**rsInvalidPolicyDefinition**|  
|**SetCacheOptions**、**SetDataSourceContents**、**SetReportDataSources**、**SetReportParameters**|**rsOperationPreventsUnattendedExecution**|  
|**CreateReportHistorySnapshot**、**Render**、**PrepareQuery**、**UpdateReportExecutionSnapshot**|**rsInvalidDataSourceReference**|  
|**CreateReportHistorySnapshot**、**PrepareQuery**、**Render**、**UpdateReportExecutionSnapshot**|**rsDataSourceDisabled**|  
|**CreateReport**、**PrepareQuery**、**SetReportDefinition**|**rsProcessingError**|  
|**GetRenderResource**、**Render**、**RenderStream**|**rsInvalidReportLink**|  
|**DeleteReportHistorySnapshot**、**Render**、**RenderStream**|**rsReportHistoryNotFound**|  
|**SetCacheOptions**、**SetExecutionOptions**、**SetReportHistoryOptions**|**rsReportMayNotBeScheduled**|  
|**CreateDataDrivenSubscription**、**GetDataDrivenSubscriptionProperties**、**SetDataDrivenSubscriptionProperties**|**rsOperationNotSupported**|  
|**CreateDataSource**、**SetDataSourceContents**、**SetReportDataSources**|**rsDataExtensionNotFound**|  
|**DeleteRole**、**SetPolicies**、**SetRoleProperties**|**rsRoleNotFound**|  
|**DeleteReportHistorySnapshot**、**Render**、**RenderStream**|**rsParametersNotSpecified**|  
|**GetReportParameters**、**SetReportParameters**|**rsNotSupported**|  
|**SetReportParameters**、**UpdateReportExecutionSnapshot**|**rsReportSnapshotNotEnabled**|  
|**CreateSchedule**、**SetScheduleProperties**|**rsScheduleAlreadyExists**|  
|**CreateRole**、**SetRoleProperties**|**rsTaskNotFound**|  
|**CreateRole**、**SetRoleProperties**|**rsMixedTasks**|  
|**ListSubscriptions**、**SetPolicies**|**rsUnknownUserName**|  
|**MoveItem**|**rsInvalidMove**|  
|**RenderStream**|**rsStreamNotFound**|  
|**RenderStream**|**rsMissingSessionId**|  
|**Render**|**rsReportNotReady**|  
|**Render**|**rsAssemblyNotPermissioned**|  
|**SetExecutionOptions**|**rsReportSnapshotEnabled**|  
|**FindItems**|**rsInvalidSearchOperator**|  
|**SetReportDataSources**|**rsDataSourceNotFound**|  
|**PrepareQuery**、**Render**|**rsDataSourceNoPrompt**|  
|**PrepareQuery**|**rsCannotPrepareQuery**|  
|**DeleteRole**|**rsReservedRole**|  
|**CreateRole**|**rsEmptyRole**|  
|**InheritParentSecurity**|**rsInheritedPolicy**|  
|**CreateRole**|**rsRoleAlreadyExists**|  
|**InheritParentSecurity**|**rsCannotDeleteRootPolicy**|  
|**CancelJob**|**rsJobWasCanceled**|  
|**ListSecureMethods**|**rsServerConfigurationError**|  
  
## <a name="see-also"></a>参照  
 [Reporting Services における例外処理の概要](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [エラーとイベントのリファレンス (Reporting Services)](../../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)   
 [Reporting Services SoapException クラス](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Detail プロパティを使用したエラー処理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
