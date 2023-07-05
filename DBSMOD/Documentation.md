# DBSMOD 說明文件

_更新於 2023-05-22T03:31:36.338Z_

`DBSMOD` 類別是封裝資料庫查詢作業的模組。  
在根類別 `DBSMOD` 中包含了基本的資料庫查詢的方法，  
繼承 `DBSMOD` 的子類別的目標則是將資料庫查詢作業封裝為一個方法。 

例如，新增產品時會進行多次資料庫查詢
- `PDTIFO` 新增產品資料
- `RT_PDTIFOTYP_PDTIFO` 新增產品類別與產品的關聯
- `PDTIFOTYP` 更新項目計數

因此 `DBSMOD_PDT::Create` 便會包含這三項作業。

&#x1F4D9; _注意！本文件由程式自動產生，若需要修改文件，請直接修改程式碼源檔案中的 PHP Document。_


# Table of Contents

<!-- toc -->

- [1. abstract Config](#1-abstract-config)
  * [1.1 SetMultiCaseVariables](#11-setmulticasevariables)
  * [1.2 Validate](#12-validate)
- [2. ConfigDatabase extends Config](#2-configdatabase-extends-config)
  * [2.1 Properties](#21-properties)
  * [2.2 __construct](#22-__construct)
  * [2.3 FromENV(static)](#23-fromenvstatic)
  * [2.4 Deploy](#24-deploy)
- [3. ConfigInit extends Config](#3-configinit-extends-config)
  * [3.1 Properties](#31-properties)
  * [3.2 __construct](#32-__construct)
  * [3.3 FromENV(static)](#33-fromenvstatic)
  * [3.4 Deploy](#34-deploy)
- [4. ConfigLanguage extends Config](#4-configlanguage-extends-config)
  * [4.1 Properties](#41-properties)
  * [4.2 __construct](#42-__construct)
  * [4.3 Deploy](#43-deploy)
- [5. ConfigPath extends Config](#5-configpath-extends-config)
  * [5.1 Properties](#51-properties)
  * [5.2 __construct](#52-__construct)
  * [5.3 FromENV(static)](#53-fromenvstatic)
  * [5.4 Deploy](#54-deploy)
- [6. ConfigRedis extends Config](#6-configredis-extends-config)
  * [6.1 Properties](#61-properties)
  * [6.2 __construct](#62-__construct)
  * [6.3 FromENV(static)](#63-fromenvstatic)
  * [6.4 Deploy](#64-deploy)
- [7. ConfigSMS extends Config](#7-configsms-extends-config)
  * [7.1 Properties](#71-properties)
  * [7.2 __construct](#72-__construct)
  * [7.3 Deploy](#73-deploy)
  * [7.4 Validate](#74-validate)
- [8. ConfigSMTP extends Config](#8-configsmtp-extends-config)
  * [8.1 Properties](#81-properties)
  * [8.2 __construct](#82-__construct)
  * [8.3 FromENV(static)](#83-fromenvstatic)
  * [8.4 SetMailProxy](#84-setmailproxy)
  * [8.5 SetMailService](#85-setmailservice)
  * [8.6 Deploy](#86-deploy)
  * [8.7 Validate](#87-validate)
  * [8.8 GetProxyURL](#88-getproxyurl)
  * [8.9 GetSMTPArray](#89-getsmtparray)
- [9. ConfigTableName extends Config](#9-configtablename-extends-config)
  * [9.1 Properties](#91-properties)
  * [9.2 __construct](#92-__construct)
  * [9.3 Deploy](#93-deploy)
- [10. ConfigTrade extends Config](#10-configtrade-extends-config)
  * [10.1 Properties](#101-properties)
  * [10.2 __construct](#102-__construct)
  * [10.3 FromENV(static)](#103-fromenvstatic)
  * [10.4 Deploy](#104-deploy)
- [11. abstract DBSMOD](#11-abstract-dbsmod)
  * [11.1 Properties](#111-properties)
  * [11.2 __construct](#112-__construct)
  * [11.3 SetTables(protected)](#113-settablesprotected)
  * [11.4 DBSSelect(protected)](#114-dbsselectprotected)
  * [11.5 DBSInsert(protected)](#115-dbsinsertprotected)
  * [11.6 DBSUpdate(protected)](#116-dbsupdateprotected)
  * [11.7 DBSDelete(protected)](#117-dbsdeleteprotected)
  * [11.8 DataExist(protected)](#118-dataexistprotected)
  * [11.9 ReadFlag](#119-readflag)
  * [11.10 WriteFlag](#1110-writeflag)
  * [11.11 GetTables](#1111-gettables)
- [12. DBSMOD_Assignment extends DBSMOD_DOC](#12-dbsmod_assignment-extends-dbsmod_doc)
  * [12.1 SetTables(protected)](#121-settablesprotected)
  * [12.2 SelectHandIn](#122-selecthandin)
  * [12.3 CreateHandIn](#123-createhandin)
  * [12.4 UpdateHandIn](#124-updatehandin)
  * [12.5 DeleteHandIn](#125-deletehandin)
  * [12.6 AppendCourse](#126-appendcourse)
  * [12.7 RemoveCourse](#127-removecourse)
  * [12.8 Export](#128-export)
- [13. DBSMOD_BulletinDOC extends DBSMOD_DOC](#13-dbsmod_bulletindoc-extends-dbsmod_doc)
  * [13.1 SetTables(protected)](#131-settablesprotected)
  * [13.2 AppendCourse](#132-appendcourse)
  * [13.3 RemoveCourse](#133-removecourse)
- [14. DBSMOD_Course extends DBSMOD](#14-dbsmod_course-extends-dbsmod)
  * [14.1 Properties](#141-properties)
  * [14.2 SetTables(protected)](#142-settablesprotected)
  * [14.3 Select](#143-select)
  * [14.4 Create](#144-create)
  * [14.5 Update](#145-update)
  * [14.6 Delete](#146-delete)
  * [14.7 SelectTYP](#147-selecttyp)
  * [14.8 CreateTYP](#148-createtyp)
  * [14.9 UpdateTYP](#149-updatetyp)
  * [14.10 DeleteTYP](#1410-deletetyp)
  * [14.11 SelectTOCItem](#1411-selecttocitem)
  * [14.12 CreateTOCItem](#1412-createtocitem)
  * [14.13 UpdateTOCItem](#1413-updatetocitem)
  * [14.14 DeleteTOCItem](#1414-deletetocitem)
  * [14.15 AppendTextbook](#1415-appendtextbook)
  * [14.16 RemoveTextbook](#1416-removetextbook)
  * [14.17 UpdateTYPIFOCNT(protected)](#1417-updatetypifocntprotected)
  * [14.18 GetInitStatusFlag(protected)](#1418-getinitstatusflagprotected)
- [15. DBSMOD_CUS extends DBSMOD](#15-dbsmod_cus-extends-dbsmod)
  * [15.1 SetTables(protected)](#151-settablesprotected)
  * [15.2 Select](#152-select)
  * [15.3 Create](#153-create)
  * [15.4 Update](#154-update)
  * [15.5 Delete](#155-delete)
  * [15.6 SelectTYP](#156-selecttyp)
  * [15.7 CreateTYP](#157-createtyp)
  * [15.8 UpdateTYP](#158-updatetyp)
  * [15.9 DeleteTYP](#159-deletetyp)
  * [15.10 UpdateTYPIFOCNT(protected)](#1510-updatetypifocntprotected)
- [16. DBSMOD_DOC extends DBSMOD](#16-dbsmod_doc-extends-dbsmod)
  * [16.1 Properties](#161-properties)
  * [16.2 SetTables(protected)](#162-settablesprotected)
  * [16.3 Select](#163-select)
  * [16.4 Create](#164-create)
  * [16.5 Update](#165-update)
  * [16.6 Approve](#166-approve)
  * [16.7 AccumulateCNT](#167-accumulatecnt)
  * [16.8 Delete](#168-delete)
  * [16.9 CreateDraftFromDOC](#169-createdraftfromdoc)
  * [16.10 CopyToTable](#1610-copytotable)
  * [16.11 SelectTYP](#1611-selecttyp)
  * [16.12 CreateTYP](#1612-createtyp)
  * [16.13 UpdateTYP](#1613-updatetyp)
  * [16.14 DeleteTYP](#1614-deletetyp)
  * [16.15 UpdateTYPIFOCNT(protected)](#1615-updatetypifocntprotected)
  * [16.16 GetInitStatusFlag(protected)](#1616-getinitstatusflagprotected)
  * [16.17 GetORIDOCField(protected)](#1617-getoridocfieldprotected)
  * [16.18 AppendMultilingualIndex](#1618-appendmultilingualindex)
  * [16.19 RemoveMultilingualIndex](#1619-removemultilingualindex)
- [17. DBSMOD_DOC_enUS extends DBSMOD_DOC](#17-dbsmod_doc_enus-extends-dbsmod_doc)
  * [17.1 SetTables(protected)](#171-settablesprotected)
- [18. DBSMOD_DSCDOC extends DBSMOD_DOC](#18-dbsmod_dscdoc-extends-dbsmod_doc)
  * [18.1 SetTables(protected)](#181-settablesprotected)
  * [18.2 Create](#182-create)
  * [18.3 SelectTopic](#183-selecttopic)
  * [18.4 CreateTopic](#184-createtopic)
  * [18.5 UpdateTopic](#185-updatetopic)
  * [18.6 DeleteTopic](#186-deletetopic)
  * [18.7 SelectReply](#187-selectreply)
  * [18.8 CreateReply](#188-createreply)
  * [18.9 UpdateReply](#189-updatereply)
  * [18.10 DeleteReply](#1810-deletereply)
  * [18.11 AppendCourse](#1811-appendcourse)
  * [18.12 RemoveCourse](#1812-removecourse)
- [19. DBSMOD_File extends DBSMOD](#19-dbsmod_file-extends-dbsmod)
  * [19.1 Properties](#191-properties)
  * [19.2 SetTables(protected)](#192-settablesprotected)
  * [19.3 Select](#193-select)
  * [19.4 Create](#194-create)
  * [19.5 Update](#195-update)
  * [19.6 Delete](#196-delete)
  * [19.7 SetPermission(protected)](#197-setpermissionprotected)
  * [19.8 SetUserPermission](#198-setuserpermission)
  * [19.9 SetGroupPermission](#199-setgrouppermission)
  * [19.10 AlterSinglePermission(protected)](#1910-altersinglepermissionprotected)
  * [19.11 AlterUserReadPermission](#1911-alteruserreadpermission)
  * [19.12 AlterGroupReadPermission](#1912-altergroupreadpermission)
  * [19.13 AlterUserWritePermission](#1913-alteruserwritepermission)
  * [19.14 AlterGroupWritePermission](#1914-altergroupwritepermission)
  * [19.15 AlterUserDeletePermission](#1915-alteruserdeletepermission)
  * [19.16 AlterGroupDeletePermission](#1916-altergroupdeletepermission)
- [20. DBSMOD_Goods extends DBSMOD](#20-dbsmod_goods-extends-dbsmod)
  * [20.1 SetTables(protected)](#201-settablesprotected)
  * [20.2 Select](#202-select)
  * [20.3 Create](#203-create)
  * [20.4 Update](#204-update)
  * [20.5 Delete](#205-delete)
  * [20.6 CreateStock](#206-createstock)
  * [20.7 SelectStockByGoodsID](#207-selectstockbygoodsid)
  * [20.8 UpdateStockByGoodsID](#208-updatestockbygoodsid)
  * [20.9 UpdateStockNewQTY](#209-updatestocknewqty)
  * [20.10 UpdateStockNewQTYByProductID](#2010-updatestocknewqtybyproductid)
  * [20.11 SelectTYP](#2011-selecttyp)
  * [20.12 CreateTYP](#2012-createtyp)
  * [20.13 UpdateTYP](#2013-updatetyp)
  * [20.14 DeleteTYP](#2014-deletetyp)
  * [20.15 UpdateTYPIFOCNT(protected)](#2015-updatetypifocntprotected)
  * [20.16 AppendRLVProduct](#2016-appendrlvproduct)
  * [20.17 RemoveRLVProduct](#2017-removerlvproduct)
- [21. DBSMOD_INV extends DBSMOD](#21-dbsmod_inv-extends-dbsmod)
  * [21.1 Properties](#211-properties)
  * [21.2 __construct](#212-__construct)
  * [21.3 SetTables(protected)](#213-settablesprotected)
  * [21.4 Select](#214-select)
  * [21.5 Create](#215-create)
  * [21.6 Update](#216-update)
  * [21.7 Delete](#217-delete)
  * [21.8 UpdateItem](#218-updateitem)
  * [21.9 CreateItem(protected)](#219-createitemprotected)
  * [21.10 GetInitStatusFlag(protected)](#2110-getinitstatusflagprotected)
  * [21.11 GetInvoiceForReceipt(protected)](#2111-getinvoiceforreceiptprotected)
- [22. DBSMOD_Link extends DBSMOD](#22-dbsmod_link-extends-dbsmod)
  * [22.1 SetTables(protected)](#221-settablesprotected)
  * [22.2 Select](#222-select)
  * [22.3 Create](#223-create)
  * [22.4 Update](#224-update)
  * [22.5 Delete](#225-delete)
- [23. DBSMOD_Link_enUS extends DBSMOD_Link](#23-dbsmod_link_enus-extends-dbsmod_link)
  * [23.1 SetTables(protected)](#231-settablesprotected)
- [24. DBSMOD_Monitor extends DBSMOD](#24-dbsmod_monitor-extends-dbsmod)
  * [24.1 Properties](#241-properties)
  * [24.2 SetTables(protected)](#242-settablesprotected)
  * [24.3 Select](#243-select)
  * [24.4 Create](#244-create)
  * [24.5 Update](#245-update)
  * [24.6 Delete](#246-delete)
  * [24.7 SelectLog](#247-selectlog)
  * [24.8 CreateLog](#248-createlog)
  * [24.9 UpdateLog](#249-updatelog)
  * [24.10 DeleteLog](#2410-deletelog)
  * [24.11 SelectITM](#2411-selectitm)
  * [24.12 CreateITM](#2412-createitm)
  * [24.13 UpdateITM](#2413-updateitm)
  * [24.14 DeleteITM](#2414-deleteitm)
  * [24.15 SelectDEV](#2415-selectdev)
  * [24.16 CreateDEV](#2416-createdev)
  * [24.17 UpdateDEV](#2417-updatedev)
  * [24.18 DeleteDEV](#2418-deletedev)
  * [24.19 SelectDEVTYP](#2419-selectdevtyp)
  * [24.20 CreateDEVTYP](#2420-createdevtyp)
  * [24.21 UpdateDEVTYP](#2421-updatedevtyp)
  * [24.22 DeleteDEVTYP](#2422-deletedevtyp)
  * [24.23 UpdateDEVTYPIFOCNT(protected)](#2423-updatedevtypifocntprotected)
  * [24.24 CreateLogItem](#2424-createlogitem)
  * [24.25 ClearExpiredLogItemCache](#2425-clearexpiredlogitemcache)
- [25. DBSMOD_OAuthToken extends DBSMOD](#25-dbsmod_oauthtoken-extends-dbsmod)
  * [25.1 Properties](#251-properties)
  * [25.2 SetTables(protected)](#252-settablesprotected)
  * [25.3 CreateToken](#253-createtoken)
  * [25.4 CheckToken](#254-checktoken)
  * [25.5 DeleteToken](#255-deletetoken)
  * [25.6 GenerateID(protected)](#256-generateidprotected)
  * [25.7 IsRevoked(protected)](#257-isrevokedprotected)
- [26. DBSMOD_PDT extends DBSMOD](#26-dbsmod_pdt-extends-dbsmod)
  * [26.1 Properties](#261-properties)
  * [26.2 __construct](#262-__construct)
  * [26.3 SetTables(protected)](#263-settablesprotected)
  * [26.4 Select](#264-select)
  * [26.5 Create](#265-create)
  * [26.6 Update](#266-update)
  * [26.7 Delete](#267-delete)
  * [26.8 AppendRLVTYP](#268-appendrlvtyp)
  * [26.9 RemoveRLVTYP](#269-removerlvtyp)
  * [26.10 SelectTYP](#2610-selecttyp)
  * [26.11 CreateTYP](#2611-createtyp)
  * [26.12 UpdateTYP](#2612-updatetyp)
  * [26.13 DeleteTYP](#2613-deletetyp)
  * [26.14 UpdateTYPIFOCNT(protected)](#2614-updatetypifocntprotected)
  * [26.15 AppendRLVCNR](#2615-appendrlvcnr)
  * [26.16 RemoveRLVCNR](#2616-removerlvcnr)
  * [26.17 SelectCNR](#2617-selectcnr)
  * [26.18 CreateCNR](#2618-createcnr)
  * [26.19 UpdateCNR](#2619-updatecnr)
  * [26.20 DeleteCNR](#2620-deletecnr)
  * [26.21 SelectCNRTYP](#2621-selectcnrtyp)
  * [26.22 CreateCNRTYP](#2622-createcnrtyp)
  * [26.23 UpdateCNRTYP](#2623-updatecnrtyp)
  * [26.24 DeleteCNRTYP](#2624-deletecnrtyp)
  * [26.25 UpdateCNRTYPIFOCNT(protected)](#2625-updatecnrtypifocntprotected)
- [27. DBSMOD_PHSSAL extends DBSMOD](#27-dbsmod_phssal-extends-dbsmod)
  * [27.1 Properties](#271-properties)
  * [27.2 __construct](#272-__construct)
  * [27.3 SetTables(protected)](#273-settablesprotected)
  * [27.4 Select](#274-select)
  * [27.5 Create](#275-create)
  * [27.6 Update](#276-update)
  * [27.7 Delete](#277-delete)
  * [27.8 UpdateItem](#278-updateitem)
  * [27.9 CreateItem(protected)](#279-createitemprotected)
  * [27.10 GetInitStatusFlag(protected)](#2710-getinitstatusflagprotected)
- [28. DBSMOD_PMO extends DBSMOD](#28-dbsmod_pmo-extends-dbsmod)
  * [28.1 SetTables(protected)](#281-settablesprotected)
  * [28.2 Select](#282-select)
  * [28.3 Create](#283-create)
  * [28.4 Update](#284-update)
  * [28.5 Delete](#285-delete)
  * [28.6 SelectTYP](#286-selecttyp)
  * [28.7 CreateTYP](#287-createtyp)
  * [28.8 UpdateTYP](#288-updatetyp)
  * [28.9 DeleteTYP](#289-deletetyp)
  * [28.10 SelectPMOPDTDCN](#2810-selectpmopdtdcn)
  * [28.11 CreatePMOPDTDCN](#2811-createpmopdtdcn)
  * [28.12 UpdatePMOPDTDCN](#2812-updatepmopdtdcn)
  * [28.13 DeletePMOPDTDCN](#2813-deletepmopdtdcn)
- [29. DBSMOD_PMSGRP extends DBSMOD](#29-dbsmod_pmsgrp-extends-dbsmod)
  * [29.2 Select](#292-select)
  * [29.3 Create](#293-create)
  * [29.4 Update](#294-update)
  * [29.5 Delete](#295-delete)
  * [29.6 SelectPMSScope](#296-selectpmsscope)
  * [29.7 CreatePMSScope](#297-createpmsscope)
  * [29.8 UpdatePMSScope](#298-updatepmsscope)
  * [29.9 DeletePMSScope](#299-deletepmsscope)
  * [29.10 AppendPMSScope](#2910-appendpmsscope)
  * [29.11 RemovePMSScope](#2911-removepmsscope)
  * [29.12 AppendPMSScopeByDCP](#2912-appendpmsscopebydcp)
  * [29.13 RemovePMSScopeByDCP](#2913-removepmsscopebydcp)
  * [29.14 CheckUser](#2914-checkuser)
- [30. DBSMOD_RSCDOC extends DBSMOD_DOC](#30-dbsmod_rscdoc-extends-dbsmod_doc)
  * [30.1 SetTables(protected)](#301-settablesprotected)
  * [30.2 AppendCourseTOCItem](#302-appendcoursetocitem)
  * [30.3 RemoveCourseTOCItem](#303-removecoursetocitem)
  * [30.4 AppendTextbookTOCItem](#304-appendtextbooktocitem)
  * [30.5 RemoveTextbookTOCItem](#305-removetextbooktocitem)
- [31. DBSMOD_SALODR extends DBSMOD](#31-dbsmod_salodr-extends-dbsmod)
  * [31.1 Properties](#311-properties)
  * [31.2 __construct](#312-__construct)
  * [31.3 SetTables(protected)](#313-settablesprotected)
  * [31.4 Select](#314-select)
  * [31.5 Create](#315-create)
  * [31.6 Update](#316-update)
  * [31.7 Delete](#317-delete)
  * [31.8 SelectItems](#318-selectitems)
  * [31.9 UpdateItem](#319-updateitem)
  * [31.10 CreateItem](#3110-createitem)
  * [31.11 ProcessAmount(protected)](#3111-processamountprotected)
  * [31.12 GetInitStatusFlag(protected)](#3112-getinitstatusflagprotected)
  * [31.13 FireStatusEvent(protected)](#3113-firestatuseventprotected)
  * [31.14 SendStatusNotice(protected)](#3114-sendstatusnoticeprotected)
  * [31.15 CreateReturnFromSALODR](#3115-createreturnfromsalodr)
  * [31.16 CreatePHSSALFromSALODR(protected)](#3116-createphssalfromsalodrprotected)
  * [31.17 CreateINVFromSALODR(protected)](#3117-createinvfromsalodrprotected)
  * [31.18 OnWaitingDeal(protected)](#3118-onwaitingdealprotected)
  * [31.19 OnDeal(protected)](#3119-ondealprotected)
  * [31.20 OnWaitingPayment(protected)](#3120-onwaitingpaymentprotected)
  * [31.21 OnPayment(protected)](#3121-onpaymentprotected)
  * [31.22 OnWaitingDelivery(protected)](#3122-onwaitingdeliveryprotected)
  * [31.23 OnDelivery(protected)](#3123-ondeliveryprotected)
  * [31.24 OnWaitingReturn(protected)](#3124-onwaitingreturnprotected)
  * [31.25 OnReturn(protected)](#3125-onreturnprotected)
  * [31.26 OnWaitingRefund(protected)](#3126-onwaitingrefundprotected)
  * [31.27 OnRefund(protected)](#3127-onrefundprotected)
  * [31.28 OnWaitingClose(protected)](#3128-onwaitingcloseprotected)
  * [31.29 OnClose(protected)](#3129-oncloseprotected)
- [32. DBSMOD_Textbook extends DBSMOD](#32-dbsmod_textbook-extends-dbsmod)
  * [32.1 SetTables(protected)](#321-settablesprotected)
  * [32.2 Select](#322-select)
  * [32.3 Create](#323-create)
  * [32.4 Update](#324-update)
  * [32.5 Delete](#325-delete)
  * [32.6 SelectTYP](#326-selecttyp)
  * [32.7 CreateTYP](#327-createtyp)
  * [32.8 UpdateTYP](#328-updatetyp)
  * [32.9 DeleteTYP](#329-deletetyp)
  * [32.10 UpdateTYPIFOCNT(protected)](#3210-updatetypifocntprotected)
  * [32.11 SelectTOCItem](#3211-selecttocitem)
  * [32.12 CreateTOCItem](#3212-createtocitem)
  * [32.13 UpdateTOCItem](#3213-updatetocitem)
  * [32.14 DeleteTOCItem](#3214-deletetocitem)
- [33. DBSMOD_User extends DBSMOD](#33-dbsmod_user-extends-dbsmod)
  * [33.1 Properties](#331-properties)
  * [33.2 SetTables(protected)](#332-settablesprotected)
  * [33.3 Select](#333-select)
  * [33.4 Create](#334-create)
  * [33.5 Update](#335-update)
  * [33.6 Delete](#336-delete)
  * [33.7 SelectTYP](#337-selecttyp)
  * [33.8 CreateTYP](#338-createtyp)
  * [33.9 UpdateTYP](#339-updatetyp)
  * [33.10 DeleteTYP](#3310-deletetyp)
  * [33.11 SelectAUT](#3311-selectaut)
  * [33.12 SelectCUS](#3312-selectcus)
  * [33.13 UpdateCUS](#3313-updatecus)
  * [33.14 ProcessPIN(protected)](#3314-processpinprotected)
  * [33.15 ProcessAUTVRF(protected)](#3315-processautvrfprotected)
  * [33.16 Login](#3316-login)
  * [33.17 SendNotice](#3317-sendnotice)
  * [33.18 ActivateEMLVRF](#3318-activateemlvrf)
  * [33.19 ChangeAUTVRF(protected)](#3319-changeautvrfprotected)
  * [33.20 ProcessEMLVRF](#3320-processemlvrf)
  * [33.21 ProcessEMLVRFByUserID](#3321-processemlvrfbyuserid)
  * [33.22 ResetPIN](#3322-resetpin)
  * [33.23 ActivateOTP](#3323-activateotp)
  * [33.24 ProcessOTP](#3324-processotp)
  * [33.25 UpdateTYPIFOCNT(protected)](#3325-updatetypifocntprotected)
- [34. DBSMOD_UserGRP extends DBSMOD](#34-dbsmod_usergrp-extends-dbsmod)
  * [34.1 SetTables(protected)](#341-settablesprotected)
  * [34.2 Select](#342-select)
  * [34.3 Create](#343-create)
  * [34.4 Update](#344-update)
  * [34.5 Delete](#345-delete)
  * [34.6 SelectRole](#346-selectrole)
  * [34.7 CreateRole](#347-createrole)
  * [34.8 UpdateRole](#348-updaterole)
  * [34.9 DeleteRole](#349-deleterole)
  * [34.10 AppendUser](#3410-appenduser)
  * [34.11 RemoveUser](#3411-removeuser)
- [35. DBSMOD_UserToken extends DBSMOD](#35-dbsmod_usertoken-extends-dbsmod)
  * [35.1 Properties](#351-properties)
  * [35.2 SetTables(protected)](#352-settablesprotected)
  * [35.3 ClearExpiredTokenOnTable(protected)](#353-clearexpiredtokenontableprotected)
  * [35.4 DeleteByTokenOnTable(protected)](#354-deletebytokenontableprotected)
  * [35.5 DeleteByUserOnTable(protected)](#355-deletebyuserontableprotected)
  * [35.6 CreateTokenOnTable(protected)](#356-createtokenontableprotected)
  * [35.7 CheckTokenOnTable(protected)](#357-checktokenontableprotected)
  * [35.8 CreateToken](#358-createtoken)
  * [35.9 CreateTMPToken](#359-createtmptoken)
  * [35.10 DeleteToken](#3510-deletetoken)
  * [35.11 DeleteTMPToken](#3511-deletetmptoken)
  * [35.12 DeleteTokenByUser](#3512-deletetokenbyuser)
  * [35.13 DeleteTMPTokenByUser](#3513-deletetmptokenbyuser)
  * [35.14 CheckToken](#3514-checktoken)
  * [35.15 CheckTMPToken](#3515-checktmptoken)
  * [35.16 Hash(protected)](#3516-hashprotected)
  * [35.17 GetRandomToken(protected)](#3517-getrandomtokenprotected)
  * [35.18 GetUserSource](#3518-getusersource)
- [36. DBSMOD_ViewSchema extends DBSMOD](#36-dbsmod_viewschema-extends-dbsmod)
  * [36.1 SetTables(protected)](#361-settablesprotected)
  * [36.2 Select](#362-select)
  * [36.3 Create](#363-create)
  * [36.4 Update](#364-update)
  * [36.5 Delete](#365-delete)
  * [36.6 SelectTYP](#366-selecttyp)
  * [36.7 CreateTYP](#367-createtyp)
  * [36.8 UpdateTYP](#368-updatetyp)
  * [36.9 DeleteTYP](#369-deletetyp)
  * [36.10 UpdateTYPIFOCNT(protected)](#3610-updatetypifocntprotected)
  * [36.11 MergeCommonSchema](#3611-mergecommonschema)
- [37. ACSTokenEntity](#37-acstokenentity)
  * [37.1 Properties](#371-properties)
  * [37.2 __construct](#372-__construct)
  * [37.3 FromArray(static)](#373-fromarraystatic)
  * [37.4 ToArray](#374-toarray)
- [38. Archive](#38-archive)
  * [38.1 __construct](#381-__construct)
  * [38.2 GetFileInfo](#382-getfileinfo)
- [39. DBSTableEntity](#39-dbstableentity)
  * [39.1 Properties](#391-properties)
  * [39.2 __construct](#392-__construct)
  * [39.3 SetFields](#393-setfields)
  * [39.4 GetFields](#394-getfields)
  * [39.5 ValidateFields](#395-validatefields)
- [40. JWTEntity](#40-jwtentity)
  * [40.1 ToString](#401-tostring)
  * [40.2 GetJTI](#402-getjti)
  * [40.3 SetJTI](#403-setjti)
  * [40.4 GetSUB](#404-getsub)
  * [40.5 SetSUB](#405-setsub)
  * [40.6 GetISS](#406-getiss)
  * [40.7 SetISS](#407-setiss)
  * [40.8 GetAUD](#408-getaud)
  * [40.9 SetAUD](#409-setaud)
  * [40.10 GetEXP](#4010-getexp)
  * [40.11 SetEXP](#4011-setexp)
  * [40.12 GetIAT](#4012-getiat)
  * [40.13 SetIAT](#4013-setiat)
  * [40.14 GetNBF](#4014-getnbf)
  * [40.15 SetNBF](#4015-setnbf)
  * [40.16 GetScopes](#4016-getscopes)
  * [40.17 SetScopes](#4017-setscopes)
- [41. MailEntity](#41-mailentity)
  * [41.1 Properties](#411-properties)
  * [41.2 __construct](#412-__construct)
  * [41.3 FromArray(static)](#413-fromarraystatic)
  * [41.4 ToArray](#414-toarray)
- [42. SiteSettingsEntity](#42-sitesettingsentity)
  * [42.1 Properties](#421-properties)
  * [42.2 __construct](#422-__construct)
  * [42.3 FromArray(static)](#423-fromarraystatic)
  * [42.4 ToArray](#424-toarray)
- [43. SMSEntity](#43-smsentity)
  * [43.1 Properties](#431-properties)
  * [43.2 __construct](#432-__construct)
  * [43.3 FromArray(static)](#433-fromarraystatic)
  * [43.4 ToArray](#434-toarray)
- [44. Spreadsheet](#44-spreadsheet)
  * [44.1 Properties](#441-properties)
  * [44.2 __construct](#442-__construct)
  * [44.3 Move](#443-move)
  * [44.4 GetFileInfo](#444-getfileinfo)
- [45. UploadFileInfo extends \SplFileInfo](#45-uploadfileinfo-extends-splfileinfo)
  * [45.1 Properties](#451-properties)
  * [45.2 FromPost(static)](#452-frompoststatic)
  * [45.3 getUploadFilename](#453-getuploadfilename)
  * [45.4 setUploadFilename](#454-setuploadfilename)
  * [45.5 getUploadType](#455-getuploadtype)
  * [45.6 setUploadType](#456-setuploadtype)
  * [45.7 getUploadExtension](#457-getuploadextension)
  * [45.8 setUploadExtension](#458-setuploadextension)
  * [45.9 rename](#459-rename)
  * [45.10 remove](#4510-remove)
- [46. Crypt {](#46-crypt-)
  * [46.1 Properties](#461-properties)
  * [46.2 __construct](#462-__construct)
  * [46.3 Encrypt](#463-encrypt)
  * [46.4 Decrypt](#464-decrypt)
  * [46.5 SetCipherMethod](#465-setciphermethod)
  * [46.6 GetCipherMethod](#466-getciphermethod)
  * [46.7 SetPassPhrase](#467-setpassphrase)
  * [46.8 GetPassPhrase](#468-getpassphrase)
- [47. DBSAction](#47-dbsaction)
  * [47.1 Properties](#471-properties)
  * [47.2 __construct](#472-__construct)
  * [47.3 AddSelect](#473-addselect)
  * [47.4 AddPreSelect](#474-addpreselect)
  * [47.5 AddUpdate](#475-addupdate)
  * [47.6 AddPreUpdate](#476-addpreupdate)
  * [47.7 AddInsert](#477-addinsert)
  * [47.8 AddPreInsert](#478-addpreinsert)
  * [47.9 AddCommand](#479-addcommand)
  * [47.10 AddOrder](#4710-addorder)
  * [47.11 AddCondition](#4711-addcondition)
  * [47.12 AddPreCondition](#4712-addprecondition)
  * [47.13 AddJoinOn](#4713-addjoinon)
  * [47.14 AddGroupBy](#4714-addgroupby)
  * [47.15 AddHaving](#4715-addhaving)
  * [47.16 AddLimit](#4716-addlimit)
  * [47.17 ClearSQL](#4717-clearsql)
  * [47.18 MergeCondition(protected)](#4718-mergeconditionprotected)
  * [47.19 MergeHaving(protected)](#4719-mergehavingprotected)
  * [47.20 RenderSQL](#4720-rendersql)
  * [47.21 ExecuteCommand](#4721-executecommand)
  * [47.22 ExecuteSQL](#4722-executesql)
  * [47.23 Count](#4723-count)
  * [47.24 RowCount](#4724-rowcount)
  * [47.25 ShowDatabases](#4725-showdatabases)
  * [47.26 ShowTables](#4726-showtables)
  * [47.27 ShowColumns](#4727-showcolumns)
  * [47.28 ShowPrimaryKey](#4728-showprimarykey)
  * [47.29 DBSSearch](#4729-dbssearch)
  * [47.30 ThrowError(protected)](#4730-throwerrorprotected)
- [48. DBSConsistency](#48-dbsconsistency)
  * [48.1 Properties](#481-properties)
- [49. EZReceipt](#49-ezreceipt)
  * [49.1 Properties](#491-properties)
  * [49.2 __construct](#492-__construct)
  * [49.3 Request(private)](#493-requestprivate)
  * [49.4 GenEndPoint(private)](#494-genendpointprivate)
  * [49.5 PostToEndpoint(private)](#495-posttoendpointprivate)
  * [49.6 Login](#496-login)
  * [49.7 InvoiceCreate](#497-invoicecreate)
- [50. FileSet](#50-fileset)
  * [50.1 Properties](#501-properties)
  * [50.2 __construct](#502-__construct)
  * [50.3 ValidateLoop(protected)](#503-validateloopprotected)
  * [50.4 ValidateElement](#504-validateelement)
  * [50.5 Get](#505-get)
  * [50.6 Set](#506-set)
  * [50.7 GetElementSchema](#507-getelementschema)
  * [50.8 Append](#508-append)
  * [50.9 AppendExist](#509-appendexist)
  * [50.10 Remove](#5010-remove)
  * [50.11 GetURLs](#5011-geturls)
  * [50.12 HandleUpload](#5012-handleupload)
- [51. Notice](#51-notice)
  * [51.1 Properties](#511-properties)
  * [51.2 __construct](#512-__construct)
  * [51.3 ReplaceDOC(protected)](#513-replacedocprotected)
  * [51.4 SetDetailFromDOC](#514-setdetailfromdoc)
  * [51.5 SetSubjectFromDOC](#515-setsubjectfromdoc)
  * [51.6 Send](#516-send)
  * [51.7 SendEmail(protected)](#517-sendemailprotected)
  * [51.8 SendSMS(protected)](#518-sendsmsprotected)
  * [51.9 SendMailByProxy](#519-sendmailbyproxy)
  * [51.10 SendMailByService](#5110-sendmailbyservice)
- [52. PICSet extends FileSet](#52-picset-extends-fileset)
  * [52.1 Properties](#521-properties)
  * [52.2 Append](#522-append)
  * [52.3 AppendExist](#523-appendexist)
  * [52.4 CopyResizeImage(protected)](#524-copyresizeimageprotected)
  * [52.5 GetMaxWidth](#525-getmaxwidth)
  * [52.6 SetMaxWidth](#526-setmaxwidth)
- [53. RedisAction](#53-redisaction)
  * [53.1 Properties](#531-properties)
  * [53.2 __construct](#532-__construct)
  * [53.3 FromConnection(static)](#533-fromconnectionstatic)
  * [53.4 GetKey(protected)](#534-getkeyprotected)
  * [53.5 SetError(protected)](#535-seterrorprotected)
  * [53.6 Set](#536-set)
  * [53.7 Get](#537-get)
  * [53.8 Delete](#538-delete)
  * [53.9 Exists](#539-exists)
  * [53.10 Expire](#5310-expire)
  * [53.11 Ping](#5311-ping)
  * [53.12 GetType](#5312-gettype)
  * [53.13 ListPush](#5313-listpush)
  * [53.14 ListGet](#5314-listget)
  * [53.15 ListRemove](#5315-listremove)
  * [53.16 SetGet](#5316-setget)
  * [53.17 SetAdd](#5317-setadd)
  * [53.18 SetRemove](#5318-setremove)
  * [53.19 SetExists](#5319-setexists)
- [54. Utility](#54-utility)
  * [54.1 DebugPrint(static)](#541-debugprintstatic)
  * [54.2 DebugShow(static)](#542-debugshowstatic)
  * [54.3 GetDBSID(static)](#543-getdbsidstatic)
  * [54.4 GetDBSSERNO(static)](#544-getdbssernostatic)
  * [54.5 GetRandom36(static)](#545-getrandom36static)
  * [54.6 ValidateEmail(static)](#546-validateemailstatic)
  * [54.7 ValidateNationalID(static)](#547-validatenationalidstatic)
  * [54.8 LinkURL(static)](#548-linkurlstatic)
  * [54.9 LinkURLSwal(static)](#549-linkurlswalstatic)
  * [54.10 SafeSQL(static)](#5410-safesqlstatic)
  * [54.11 SafeScript(static)](#5411-safescriptstatic)
  * [54.12 SafeXSS(static)](#5412-safexssstatic)
  * [54.13 CheckMethod(static)](#5413-checkmethodstatic)
  * [54.14 ReplaceTPL(static)](#5414-replacetplstatic)
  * [54.15 ConvertDBSPICToURI(static)](#5415-convertdbspictouristatic)
  * [54.16 ConvertDBSFileToURI(static)](#5416-convertdbsfiletouristatic)
  * [54.17 ConvertDBSPathToURI(static)](#5417-convertdbspathtouristatic)
  * [54.18 GetTimeDiff(static)](#5418-gettimediffstatic)
  * [54.19 ReadFlag(static)](#5419-readflagstatic)
  * [54.20 WriteFlag(static)](#5420-writeflagstatic)
  * [54.21 FilterSensitiveIFO(static)](#5421-filtersensitiveifostatic)
  * [54.22 ConvertDataTimeToTimestamp(static)](#5422-convertdatatimetotimestampstatic)
  * [54.23 ConvertTimestampToDataTime(static)](#5423-converttimestamptodatatimestatic)
  * [54.24 TryDecodeJson(static)](#5424-trydecodejsonstatic)
  * [54.25 TryEncodeJson(static)](#5425-tryencodejsonstatic)
  * [54.26 GetChineseWeekday(static)](#5426-getchineseweekdaystatic)
  * [54.27 GetEmbedYoutubeURL(static)](#5427-getembedyoutubeurlstatic)
  * [54.28 ReplaceBlank(static)](#5428-replaceblankstatic)
  * [54.29 ConvertNumToLetter(static)](#5429-convertnumtoletterstatic)
  * [54.30 ConvertLetterToNum(static)](#5430-convertlettertonumstatic)
  * [54.31 ConvertNumToChinese(static)](#5431-convertnumtochinesestatic)
  * [54.32 ConvertNewLine(static)](#5432-convertnewlinestatic)
  * [54.33 ReplaceLinkInText(static)](#5433-replacelinkintextstatic)
  * [54.34 GetLanguagePack(static)](#5434-getlanguagepackstatic)
  * [54.35 ParseRawHttpRequest(static)](#5435-parserawhttprequeststatic)
  * [54.36 HandleRequestData(static)](#5436-handlerequestdatastatic)
  * [54.37 GetLanguage(static)](#5437-getlanguagestatic)

<!-- tocstop -->

# 1. abstract Config


## 1.1 SetMultiCaseVariables

```php
public function SetMultiCaseVariables($Key, $Value, &$Scope = null)
```

宣告不同命名規則的變數：給予變數的蛇形命名法(小寫)及其值，  
自動在指定的陣列中宣告蛇形、全大寫蛇形、小駝峰、大駝峰等四種命名規則的變數

| Param | Type | Description |
|:--|:--|:--|
| `$Key` | `string` | 蛇形命名法(小寫)的變數名稱 |
| `$Value` | `mixed` | 變數的值 |
| `$Scope` | `array` | 變數作用的陣列，預設為 $GLOBALS |



## 1.2 Validate

```php
public function Validate()
```

驗證設定完整性

**回傳**

`bool`



# 2. ConfigDatabase extends Config


## 2.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Host` | `string` | 資料庫主機的域名或IP位置，如 `localhost` 或 `100.111.112.1` |
| `$Name` | `string` | 資料庫名稱 |
| `$User` | `string` | 資料庫使用者名稱 |
| `$Password` | `string` | 資料庫使用者密碼 |
| `$Link` | `\PDO` | 資料庫連線 PDO 物件 |


## 2.2 __construct

```php
public function __construct($Host, $Name, $User, $Password = null)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Host` | `string` | 伺服器 |
| `$Name` | `string` | 資料庫名稱 |
| `$User` | `string` | 使用者名稱 |
| `$Password` | `string` | 使用者密碼 |



## 2.3 FromENV(static)

```php
static public function FromENV()
```

從環境變數建構

**回傳**

ConfigDatabase



## 2.4 Deploy

```php
public function Deploy()
```

部署設定



# 3. ConfigInit extends Config


## 3.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$ErrorReporting` | `int` | 錯誤回報等級，詳見 https://www.php.net/manual/en/errorfunc.constants.php |
| `$TimeZone` | `string` | 時區，詳見 https://www.php.net/manual/en/timezones.php |


## 3.2 __construct

```php
public function __construct($ErrorLevel = 0, $TimeZone = 'Asia/Taipei')
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$ErrorLevel` | `int` | 錯誤回報等級，詳見 https://www.php.net/manual/en/errorfunc.constants.php |
| `$TimeZone` | `string` | 時區，詳見 https://www.php.net/manual/en/timezones.php |



## 3.3 FromENV(static)

```php
static public function FromENV()
```

從環境變數建構

**回傳**

ConfigInit



## 3.4 Deploy

```php
public function Deploy()
```

部署設定



# 4. ConfigLanguage extends Config


## 4.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$LanguageCode` | `string` | 語系代碼 |
| `$LanguageFile` | `string` | 語言包檔案路徑 |


## 4.2 __construct

```php
public function __construct($LanguageCode, $LanguageFile)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$LanguageCode` | `string` | 語系代碼，如 `zh-tw` |
| `$LanguageFile` | `string` | 語言包檔案路徑 |



## 4.3 Deploy

```php
public function Deploy()
```

部署設定



# 5. ConfigPath extends Config


## 5.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$SiteName` | `string` | 專案名稱|網站名稱 |
| `$ProjectDIR` | `string` | 專案根目錄，如 `/var/www/misa_manage` |
| `$SchemaRootDIR` | `string` | 專案存放用戶端 `schema` 檔案的資料夾路徑，如 `/var/www/misa_manage/site/schema` |
| `$ModeDIR` | `string` | `MISA-MOD` 資源庫的存放路徑，如 `/var/www/allen_mode/gold/v4.1.1/` |
| `$RootDIR` | `string` | 專案用戶端的根目錄路徑，如 `/var/www/misa_manage/site` |
| `$DIRPath` | `string` | 營運端上傳的檔案存放的目錄路徑，如 `/var/www/misa_manage/site/data/cht` |
| `$JSONPath` | `string` | 專案存放快取的路徑，如 `/var/www/misa_manage/site/data` |
| `$RootURL` | `string` | 專案用戶端目錄的網址，如 `http://localhost/misa_manage/site` |
| `$URLPath` | `string` | 營運端上傳的檔案存放的目錄的網址，如 `http://localhost/misa_manage/site/data/cht` |


## 5.2 __construct

```php
public function __construct($SiteName, $ProjectDIR, $ModeDIR, $Protocol = 'https', $HostPath = 'localhost/site')
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$SiteName` | `string` | 專案名稱 |
| `$ProjectDIR` | `string` | 專案目錄 |
| `$ModeDIR` | `string` | 模式目錄 |
| `$Protocol` | `string` | 網址協定 |
| `$HostPath` | `string` | 主機名稱與路徑 |



## 5.3 FromENV(static)

```php
static public function FromENV()
```

從環境變數建構

**回傳**

ConfigPath



## 5.4 Deploy

```php
public function Deploy()
```

部署設定



# 6. ConfigRedis extends Config


## 6.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Host` | `string` | Redis 伺服器位址 |
| `$Password` | `string` | Redis 伺服器密碼，無密碼時請傳入空字串 |
| `$Port` | `int` | Redis 伺服器埠號，預設為 `6379` |
| `$Link` | `\Predis\Client` | Redis 資料庫驅動 |


## 6.2 __construct

```php
public function __construct($Host, $Password = null, $Port = 6379)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Host` | `string` | 伺服器 |
| `$Password` | `string` | 使用者密碼 |
| `$Port` | `int` | 使用者密碼 |



## 6.3 FromENV(static)

```php
static public function FromENV()
```

從環境變數建立 ConfigRedis 物件

**回傳**

ConfigRedis



## 6.4 Deploy

```php
public function Deploy()
```

部署設定



# 7. ConfigSMS extends Config


## 7.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Username` | `string` | 簡訊服務社帳號 |
| `$Password` | `string` | 簡訊服務社密碼 |
| `$AppURL` | `string` | 簡訊服務社簡訊發送網址 |


## 7.2 __construct

```php
public function __construct($Username, $Password, $URL)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Service` | `string` | 簡訊服務社 |
| `$Username` | `string` | 簡訊服務社帳號 |
| `$Password` | `string` | 簡訊服務社密碼 |
| `$URL` | `string` | 簡訊服務社簡訊發送網址 |



## 7.3 Deploy

```php
public function Deploy()
```

部署設定



## 7.4 Validate

```php
public function Validate()
```

驗證設定完整性

**回傳**

`bool`



# 8. ConfigSMTP extends Config


## 8.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Host` | `string` | 伺服器的域名或IP位置，如 `smtp.gmail.com` 或 `100.111.112.1` |
| `$User` | `string` | 伺服器的用戶名稱 |
| `$Password` | `string` | 伺服器的密碼 |
| `$From` | `string` | 寄件人的電子郵件地址 |
| `$FromName` | `string` | 寄件人的名稱 |
| `$ProxyAppID` | `string` | 郵件代理服務應用程式名稱 |
| `$ProxyCryptPassPhrase` | `string` | 郵件代理加密密碼片語 |
| `$ProxyPath` | `string` | 郵件代理服務的 API 網址 |
| `$ProxyURL` | `string` | **(protected)** 郵件代理服務的完整 API 網址 |


## 8.2 __construct

```php
public function __construct($Host, $User, $Password, $From, $FromName)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Host` | `string` | 伺服器 |
| `$User` | `string` | 使用者名稱 |
| `$Password` | `string` | 使用者密碼 |
| `$From` | `string` | 寄件者 |
| `$FromName` | `string` | 寄件者名稱 |



## 8.3 FromENV(static)

```php
static public function FromENV($AddProxyQueue = true)
```

從環境變數建構，如果環境變數包含 `EMAIL_PROXY_APP_ID`，則會一併設定郵件代理服務

| Param | Type | Description |
|:--|:--|:--|
| `$AddProxyQueue` | `bool` | 是否加入佇列，預設為 `true` |

**回傳**

ConfigSMTP



## 8.4 SetMailProxy

```php
public function SetMailProxy($ProxyAppID, $ProxyCryptPassPhrase, $ProxyRoot, $AddQueue = true)
```

設定郵件代理服務

| Param | Type | Description |
|:--|:--|:--|
| `$ProxyAppID` | `string` | 郵件代理服務應用程式名稱 |
| `$ProxyCryptPassPhrase` | `string` | 郵件加密密碼片語 |
| `$ProxyRoot` | `string` | 郵件代理服務的 API 網址 |
| `$AddQueue` | `bool` | 是否加入佇列 |



## 8.5 SetMailService

```php
public function SetMailService($AppId, $CryptPassPhrase, $AppPath, $AddQueue = true)
```

設定郵件代理服務 (舊版，請改用 `SetMailProxy`)

| Param | Type | Description |
|:--|:--|:--|
| `$AppID` | `string` | 郵件代理服務應用程式名稱 |
| `$CryptPassPhrase` | `string` | 郵件加密密碼片語 |
| `$AppPath` | `string` | 郵件代理服務的 API 網址 |
| `$AddQueue` | `bool` | 是否加入佇列 |



## 8.6 Deploy

```php
public function Deploy()
```

部署設定



## 8.7 Validate

```php
public function Validate()
```

驗證設定內容

**回傳**

`bool`



## 8.8 GetProxyURL

```php
public function GetProxyURL()
```

取得郵件服務的完整 API 網址

**回傳**

`string`



## 8.9 GetSMTPArray

```php
public function GetSMTPArray()
```

取得SMTP伺服器的設定關聯陣列，包含 Host, Username, Password, ServiceMail, Title 等鍵

**回傳**

`array`



# 9. ConfigTableName extends Config


## 9.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$TableJSONFile` | `string` | 資料表名稱快取JSON的路徑 |
| `$DatabaseConfig` | `ConfigDatabase` | **(protected)** 資料庫連線的設定物件 |


## 9.2 __construct

```php
public function __construct($TableJSONFile, $DatabaseConfig)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$TableJSONFile` | `string` | 資料表JSON檔案路徑 |
| `$Database` | `ConfigDatabase` | 資料庫連線設定 |



## 9.3 Deploy

```php
public function Deploy()
```

部署設定



# 10. ConfigTrade extends Config


## 10.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$TaxRate` | `float` | 營業稅率 |
| `$PricePrecision` | `int` | 價格的小數位數 |
| `$UnitPriceIncludesTax` | `bool` | 產品售價是否已含稅 |
| `$Currency` | `string` | 交易用貨幣 |
| `$CreateINVBeforeDelivery` | `bool` | 是否在出貨前建立發票；若此值為 `true`，則訂單在狀態事件 `OnWaitingDelivery` 會建立發票；反之則在狀態事件 `OnDelivery` 建立發票 |
| `$ActiveGoods` | `bool` | 是否在建立產品(PDTIFO)時同步建立物料(Goods)資料 |
| `$SALODRNoticeDocuments` | `array` | 訂單通知訊息範本文件的關聯陣列。<br>陣列的鍵是訂單狀態事件名稱：`OnWaitingDeal`, `OnDeal`, `OnWaitingPayment`, `OnPayment`, `OnWaitingDelivery`, `OnDelivery`, `OnWaitingReturn`, `OnReturn`, `OnWaitingRefund`, `OnRefund`, `OnWaitingClose`, `OnClose`<br>陣列中的每個值都是一個範本文件的資訊陣列，有以下兩個鍵：<br>`TPLDOCID`：範本文件的 REFODCID<br>`ReplaceArray`：範本文件的待替換關鍵字數值陣列 |
| `$Receipt` | `array` | 發票相關設定 |


## 10.2 __construct

```php
public function __construct($PricePrecision = 1, $TaxRate = 0.05, $UnitPriceIncludesTax = true, $Currency = 'NTD', $CreateINVBeforeDelivery = true, $ActiveGoods = true, $Receipt = array())
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$PricePrecision` | `int` | 價格的小數位數 |
| `$TaxRate` | `float` | 營業稅率 |
| `$UnitPriceIncludesTax` | `bool` | 產品售價是否已包含營業稅 |
| `$Currency` | `string` | 交易用貨幣 |
| `$CreateINVBeforeDelivery` | `bool` | 是否在出貨前建立發票 |
| `$ActiveGoods` | `bool` | 是否在建立產品(PDTIFO)時同步建立物料(Goods)資料 |
| `$Receipt` | `array` | 發票相關設定 |



## 10.3 FromENV(static)

```php
static public function FromENV()
```

從環境變數建構

**回傳**

ConfigTrade



## 10.4 Deploy

```php
public function Deploy()
```

部署設定



# 11. abstract DBSMOD


## 11.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | PDO 物件 |
| `$DBS` | `string` | 資料庫名稱 |
| `$Tables` | `array` | **(protected)** 本物件關聯的資料表資訊關聯陣列<br>陣列中各元素的鍵為資料表名稱，值為 DBSTableEntity 物件<br>本屬性在建構時自動寫入 |
| `$DefaultTable` | `string` | 預設資料表名稱<br>本物件的方法被呼叫時，若未帶入引數 $TableName, $TablePK<br>則使用此屬性作為資料表名稱 |
| `$Error` | `\Exception` | 錯誤訊息 |


## 11.2 __construct

```php
public function __construct($DBSLink, $DBS)
```

類別建構子

| Param | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | PDO 物件 |
| `$DBS` | `string` | 資料庫名稱 |



## 11.3 SetTables(protected)

```php
abstract protected function SetTables();
```

抽象方法:  
繼承 `DBSMOD` 的類別必須實作的抽象方法  
在建構實例時會呼叫以設定相關資料表的資訊  
回傳本物件關聯的資料表名稱的數值陣列  
第一個元素為預設的資料表名稱  
```php  
class DBSMOD_Example extends DBSMOD  
{  
  protected function SetTables()  
  {  
    $Tbs = ['PDTIFO', 'PDTStock', 'PDTIFOTYP', 'RT_PDTIFOTYP_PDTIFO'];  
    return array_map(function ($Tb) {  
      return $GLOBALS[$Tb . '_Tb'];  
    }, $Tbs);  
  }  
}  
```

**回傳**

`array`



## 11.4 DBSSelect(protected)

```php
protected function DBSSelect($ID, $Field_Array = array(), $TableName = "", $TablePK = "")
```

在指定資料表(預設為主要資料表)查詢指定 ID 的單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 查詢目標的主鍵 |
| `$Field_Array` | `array` | 資料表欄位名稱的陣列 |
| `$TableName` | `string` | 非必填: 資料表名稱，預設為物件的 $TableName |
| `$TablePK` | `string` | 非必填: 資料表主鍵欄位名稱，預設為物件的 $TablePK |

**回傳**

`array`|`false` 查詢成功時回傳以資料表欄位名稱為鍵的關聯式陣列



## 11.5 DBSInsert(protected)

```php
protected function DBSInsert($R_Data, $TableName = "", $TablePK = "")
```

在指定資料表(預設為主要資料表)新增單筆資料，被 `$TablePK` 指定的欄位會填入自動產生的 ID

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | 資料表欄位名稱與資料的映射 |
| `$TableName` | `string` | 非必填: 資料表名稱，預設為物件的 $TableName |
| `$TablePK` | `string` | 非必填: 資料表主鍵欄位名稱，預設為物件的 $TablePK |

**回傳**

`array`|`false` 新增成功時回傳包含主鍵及 `SERNO` 的關聯式陣列



## 11.6 DBSUpdate(protected)

```php
protected function DBSUpdate($ID, $R_Data, $TableName = "", $TablePK = "")
```

在指定資料表(預設為主要資料表)更新指定 ID 的單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 查詢目標的主鍵 |
| `$R_Data` | `array` | 資料表欄位名稱與資料的映射 |
| `$TableName` | `string` | 非必填: 資料表名稱，預設為物件的 $TableName |
| `$TablePK` | `string` | 非必填: 資料表主鍵欄位名稱，預設為物件的 $TablePK |

**回傳**

`array`|`false` 更新成功時回傳包含主鍵及 `SERNO` 的關聯式陣列



## 11.7 DBSDelete(protected)

```php
protected function DBSDelete($ID, $TableName = "", $TablePK = "", $ForceDelete = false)
```

在指定資料表(預設為主要資料表)刪除指定 ID 的單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 查詢目標的主鍵 |

**回傳**

`bool` 刪除成功時回傳 ``true``



## 11.8 DataExist(protected)

```php
protected function DataExist($ID, $TableName = "", $TablePK = "")
```

在指定資料表(預設為主要資料表)檢查指定 ID 的單筆資料是否存在

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 查詢目標的主鍵 |
| `$R_Data` | `array` | 資料表欄位名稱與資料的映射 |
| `$TableName` | `string` | 非必填: 資料表名稱，預設為物件的 $TableName |

**回傳**

`bool` 若指定 ID 資料已存在回傳 ``true``，反之回傳 ``false``



## 11.9 ReadFlag

```php
public function ReadFlag($Flag, $Index)
```

旗標字串讀取函式，以最右側的字元為 `0` 位

| Param | Type | Description |
|:--|:--|:--|
| `$Flag` | `string` | 待讀取的旗標 |
| `$Index` | `int` | 指定的索引，以字串中最右邊的字元為 `0` 位 |

**回傳**

`string`|`false` 回傳指定索引的旗標字元



## 11.10 WriteFlag

```php
public function WriteFlag($Flag, $Index, $NewChar = "")
```

旗標字串寫入函式，以最右側的字元為 `0` 位

| Param | Type | Description |
|:--|:--|:--|
| `$Flag` | `string` | 待寫入的旗標 |
| `$Index` | `int` | 指定的索引，以字串中最右邊的字元為 `0` 位 |
| `$NewChar` | `string` | 寫入旗標指定索引的字元 |

**回傳**

`string`|`false` 回傳修改後的旗標字串



## 11.11 GetTables

```php
public function GetTables()
```

取得物件的 Tables 屬性

**回傳**

`array`



# 12. DBSMOD_Assignment extends DBSMOD_DOC


## 12.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 12.2 SelectHandIn

```php
public function SelectHandIn($ID, $Field_Array = array())
```

取得作業繳交資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | AssignmentHandInID |
| `$Field_Array` | `array` | 欄位名稱陣列 |

**回傳**

`array`|`false`



## 12.3 CreateHandIn

```php
public function CreateHandIn($R_Data)
```

建立作業繳交資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | 作業繳交的資料 |

**回傳**

`array`|`false`



## 12.4 UpdateHandIn

```php
public function UpdateHandIn($ID, $R_Data)
```

更新作業繳交資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | AssignmentHandInID |
| `$R_Data` | `array` | 作業繳交的資料 |

**回傳**

`array`|`false`



## 12.5 DeleteHandIn

```php
public function DeleteHandIn($ID)
```

刪除作業繳交資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | AssignmentHandInID |

**回傳**

`bool`



## 12.6 AppendCourse

```php
public function AppendCourse($AssignmentDOCID, $CourseID)
```

新增作業文件與課程關聯

| Param | Type | Description |
|:--|:--|:--|
| `$AssignmentDOCID` | `string` | AssignmentDOCID |
| `$CourseID` | `string` | CourseID |

**回傳**

`bool`



## 12.7 RemoveCourse

```php
public function RemoveCourse($AssignmentDOCID, $CourseID)
```

移除作業文件與課程關聯

| Param | Type | Description |
|:--|:--|:--|
| `$AssignmentDOCID` | `string` | AssignmentDOCID |
| `$CourseID` | `string` | CourseID |

**回傳**

`bool`



## 12.8 Export

```php
public function Export($AssignmentDOCID)
```

TODO: 匯出作業文件、所屬課程、底下的作業繳交資料  
待完成 Archive, Spreadsheet 等模組後，再實作

| Param | Type | Description |
|:--|:--|:--|
| `$AssignmentDOCID` | `string` | AssignmentDOCID |

**回傳**

`array`|`bool`



# 13. DBSMOD_BulletinDOC extends DBSMOD_DOC


## 13.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 13.2 AppendCourse

```php
public function AppendCourse($BulletinDOCID, $CourseID)
```

新增公告文件與課程關聯

| Param | Type | Description |
|:--|:--|:--|
| `$BulletinDOCID` | `string` | BulletinDOCID |
| `$CourseID` | `string` | CourseID |

**回傳**

`bool`



## 13.3 RemoveCourse

```php
public function RemoveCourse($BulletinDOCID, $CourseID)
```

移除公告文件與課程關聯

| Param | Type | Description |
|:--|:--|:--|
| `$CourseID` | `string` | CourseID |
| `$BulletinDOCID` | `string` | BulletinDOCID |

**回傳**

`bool`



# 14. DBSMOD_Course extends DBSMOD


## 14.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$StatusFlagKeys` | `array` | `Course.StatusFlag` 課程每個旗標所象徵的狀態 |
| `$RequiredStatus` | `array` | `Course.StatusFlag` 初始即不為空值的旗標 |
| `$AutoCompleteStatus` | `array` | `Course.StatusFlag` 初始即為完成的旗標 |


## 14.2 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 14.3 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 14.4 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | Course資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 14.5 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseID |
| `$R_Data` | `array` | Course 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 14.6 Delete

```php
public function Delete($ID)
```

刪除課程資料；一併刪除教科書的關聯資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseID |

**回傳**

`bool`



## 14.7 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 CourseTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 14.8 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 CourseTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | CourseTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 14.9 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 CourseTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseTYPID |
| `$R_Data` | `array` | CourseTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 14.10 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 CourseTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseTYPID |

**回傳**

`bool`



## 14.11 SelectTOCItem

```php
public function SelectTOCItem($ID, $Field_Array = array())
```

取得課程目錄項目

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseTOCITMID |
| `$Field_Array` | `array` | 欄位名稱陣列 |

**回傳**

`array`|`false`



## 14.12 CreateTOCItem

```php
public function CreateTOCItem($R_Data, $PreviousItemID = null)
```

建立課程目錄項目，並更新同課程中其他章節的序號

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | 課程目錄項目的資料 |
| `$PreviousItemID` | `string` | 排序在前一個的課程目錄項目ID |

**回傳**

`array`|`false`



## 14.13 UpdateTOCItem

```php
public function UpdateTOCItem($ID, $R_Data)
```

更新課程目錄項目，並更新同課程中其他章節的序號

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseTOCITMID |
| `$R_Data` | `array` | 課程目錄項目的資料 |

**回傳**

`array`|`false`



## 14.14 DeleteTOCItem

```php
public function DeleteTOCItem($ID)
```

刪除課程目錄項目，並更新同課程中其他章節的序號

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseTOCITMID |

**回傳**

`bool`



## 14.15 AppendTextbook

```php
public function AppendTextbook($CourseID, $TextbookID)
```

新增教科書與課程關聯

| Param | Type | Description |
|:--|:--|:--|
| `$CourseID` | `string` | CourseID |
| `$TextbookID` | `string` | TextbookID |

**回傳**

`bool`



## 14.16 RemoveTextbook

```php
public function RemoveTextbook($CourseID, $TextbookID)
```

移除課程與教科書的關聯

| Param | Type | Description |
|:--|:--|:--|
| `$CourseID` | `string` | CourseID |
| `$TextbookID` | `string` | TextbookID |

**回傳**

`bool`



## 14.17 UpdateTYPIFOCNT(protected)

```php
protected function UpdateTYPIFOCNT($ID, $Count = 1)
```

更新資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CourseTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`bool`



## 14.18 GetInitStatusFlag(protected)

```php
protected function GetInitStatusFlag()
```

取得初始狀態旗標字串

**回傳**

`string`



# 15. DBSMOD_CUS extends DBSMOD


## 15.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 15.2 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CUSIFOID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 15.3 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | CUSIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 15.4 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CUSIFOID |
| `$R_Data` | `array` | CUSIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 15.5 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CUSIFOID |

**回傳**

`bool`



## 15.6 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 CUSIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CUSIFOTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 15.7 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 CUSIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | CUSIFOTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 15.8 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 CUSIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CUSIFOTYPID |
| `$R_Data` | `array` | CUSIFOTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 15.9 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 CUSIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CUSIFOTYPID |

**回傳**

`bool`



## 15.10 UpdateTYPIFOCNT(protected)

```php
protected function UpdateTYPIFOCNT($ID, $Count = 1)
```

更新資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | CUSIFOTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`bool`



# 16. DBSMOD_DOC extends DBSMOD


## 16.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$StatusFlagKeys` | `array` | `REFDOC.StatusFlag` 文件每個旗標所象徵的狀態 |
| `$RequiredStatus` | `array` | `REFDOC.StatusFlag` 初始即不為空值的旗標 |
| `$AutoCompleteStatus` | `array` | `REFDOC.StatusFlag` 初始即為完成的旗標 |
| `$DraftFields` | `array` | **(protected)** 文件在草稿時可寫入的 `REFDOC` 資料欄位名稱的數值陣列 |
| `$TYPTable` | `string` | **(protected)** 文件類別資料表名稱 |
| `$TYPTablePK` | `string` | **(protected)** 文件類別資料表主鍵欄位名稱 |


## 16.2 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)，並寫入 $this->TYPTable, $this->TYPTablePK

**回傳**

`array`



## 16.3 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | REFDOCID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 16.4 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | REFDOC資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 16.5 Update

```php
public function Update($ID, $R_Data, $AccumulateModifyCNT = false)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | REFDOCID |
| `$R_Data` | `array` | REFDOC 資料表欄位名稱與資料的映射 |
| `$AccumulateModifyCNT` | `bool` | 是否需要累計修改計數，若為 `true` 則累計 |

**回傳**

`array`|`false`



## 16.6 Approve

```php
public function Approve($DraftID)
```

核准文件

| Param | Type | Description |
|:--|:--|:--|
| `$DraftID` | `string` | 草稿的 REFDOCID |

**回傳**

`bool`



## 16.7 AccumulateCNT

```php
public function AccumulateCNT($ID, $Field, $Count = 1)
```

累計文件計數 ReadCNT|RSPCNT|TotalRSPCNT|LikeCNT|ShareCNT|CMTCNT|ModifyCNT

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | REFDOCID |
| `$Field` | `string` | 累計計數的欄位 |
| `$Count` | `int` | 累計的值 |

**回傳**

`bool`



## 16.8 Delete

```php
public function Delete($ID)
```

刪除文件資料；若刪除的文件為草稿，則一併變更原文件狀態旗標；若刪除的文件為發佈文件，則一併刪除草稿

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | REFDOCID |

**回傳**

`bool`



## 16.9 CreateDraftFromDOC

```php
public function CreateDraftFromDOC($ID, $R_Data)
```

建立既有文件的草稿，並將原文件標註狀態為編輯中

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 欲建立草稿的文件 REFDOCID |
| `$R_Data` | `array` | 草稿的文件內容 |

**回傳**

`array`|`false` 建立草稿成功時回傳包含主鍵及 `SERNO` 的關聯式陣列



## 16.10 CopyToTable

```php
public function CopyToTable($ID, $Table, $TablePK, $Field_Array = array())
```

複製文件資料到指定資料表

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 欲複製的文件 REFDOCID |
| `$Table` | `string` | 複製到的資料表名稱 |
| `$TablePK` | `string` | 複製到的資料表的主鍵名稱 |
| `$Field_Array` | `array` | 複製的欄位 |

**回傳**

`array`|`false` 複製成功時回傳主鍵的關聯式陣列



## 16.11 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 REFDOCTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | REFDOCTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 16.12 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 REFDOCTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | REFDOCTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 16.13 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 REFDOCTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | REFDOCTYPID |
| `$R_Data` | `array` | REFDOCTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 16.14 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 REFDOCTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | REFDOCTYPID |

**回傳**

`bool`



## 16.15 UpdateTYPIFOCNT(protected)

```php
protected function UpdateTYPIFOCNT($ID, $Count = 1)
```

更新資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | REFDOCTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`bool`



## 16.16 GetInitStatusFlag(protected)

```php
protected function GetInitStatusFlag()
```

取得初始狀態旗標字串

**回傳**

`string`



## 16.17 GetORIDOCField(protected)

```php
protected function GetORIDOCField() {
```

取得記錄原始文件ID的資料表欄位名稱，如 `ORIREFDOCID`

**回傳**

`string`



## 16.18 AppendMultilingualIndex

```php
public function AppendMultilingualIndex($ID, $Language, $ReferenceID = '', $ReferenceLanguage = '')
```

附加語系關聯

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 欲附加語系關聯的文件 UID |
| `$Language` | `string` | 欲附加的語系代碼，如 `zh-TW` |
| `$ReferenceID` | `string` | (選擇性) 文件資料對應的其他語系的文件 UID |
| `$ReferenceLanguage` | `string` | (選擇性) 其他語系文件的語系代碼，如 `en-US` |

**回傳**

`bool`



## 16.19 RemoveMultilingualIndex

```php
public function RemoveMultilingualIndex($ID, $Language)
```

移除語系關聯

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 欲移除語系關聯的文件 UID |
| `$Language` | `string` | 欲移除的語系代碼，如 `zh-TW` |

**回傳**

`bool`



# 17. DBSMOD_DOC_enUS extends DBSMOD_DOC


## 17.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)，並寫入 $this->TYPTable, $this->TYPTablePK

**回傳**

`array`



# 18. DBSMOD_DSCDOC extends DBSMOD_DOC


## 18.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 18.2 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | DSSCDOC資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 18.3 SelectTopic

```php
public function SelectTopic($ID, $Field_Array = array())
```

取得討論主題

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | DSCTopicID |
| `$Field_Array` | `array` | 欄位名稱陣列 |

**回傳**

`array`|`false`



## 18.4 CreateTopic

```php
public function CreateTopic($R_Data)
```

建立討論主題資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | 討論主題的資料 |

**回傳**

`array`|`false`



## 18.5 UpdateTopic

```php
public function UpdateTopic($ID, $R_Data)
```

更新討論主題資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | DSCTopicID |
| `$R_Data` | `array` | 討論主題的資料 |

**回傳**

`array`|`false`



## 18.6 DeleteTopic

```php
public function DeleteTopic($ID)
```

刪除討論主題資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | DSCTopicID |

**回傳**

`bool`



## 18.7 SelectReply

```php
public function SelectReply($ID, $Field_Array = array())
```

取得討論回覆

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | DSCReplyID |
| `$Field_Array` | `array` | 欄位名稱陣列 |

**回傳**

`array`|`false`



## 18.8 CreateReply

```php
public function CreateReply($R_Data)
```

建立討論回覆資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | 討論回覆的資料 |

**回傳**

`array`|`false`



## 18.9 UpdateReply

```php
public function UpdateReply($ID, $R_Data)
```

更新討論回覆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | DSCReplyID |
| `$R_Data` | `array` | 討論回覆的資料 |

**回傳**

`array`|`false`



## 18.10 DeleteReply

```php
public function DeleteReply($ID)
```

刪除討論回覆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | DSCTopicID |

**回傳**

`bool`



## 18.11 AppendCourse

```php
public function AppendCourse($DSCDOCID, $CourseID)
```

新增課程與討論文件、討論主題關聯

| Param | Type | Description |
|:--|:--|:--|
| `$DSCDOCID` | `string` | DSCDOCID |
| `$CourseID` | `string` | CourseID |

**回傳**

`bool`



## 18.12 RemoveCourse

```php
public function RemoveCourse($DSCDOCID, $CourseID)
```

移除課程與討論文件、討論主題關聯

| Param | Type | Description |
|:--|:--|:--|
| `$DSCDOCID` | `string` | DSCDOCID |
| `$CourseID` | `string` | CourseID |

**回傳**

`bool`



# 19. DBSMOD_File extends DBSMOD


## 19.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$UserPermissionFields` | `array` | **(protected)** 權限相關資料表欄位與權限常數的映射 |


## 19.2 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 19.3 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 19.4 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | File資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 19.5 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$R_Data` | `array` | File資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 19.6 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |

**回傳**

`bool`



## 19.7 SetPermission(protected)

```php
protected function SetPermission($Fields, $ID, $AgentID, $Scope = FILE_PERMISSION_ALL)
```

設定用戶或用戶群組對檔案的權限  
`Scope` 參數建議使用 `FILE_PERMISSION_*` 常數:  
FILE_PERMISSION_DELETE => 1  
FILE_PERMISSION_WRITE => 2  
FILE_PERMISSION_READ => 4  
FILE_PERMISSION_WRITE_DELETE => 3  
FILE_PERMISSION_DELETE_WRITE => 3  
FILE_PERMISSION_READ_DELETE => 5  
FILE_PERMISSION_DELETE_READ => 5  
FILE_PERMISSION_READ_WRITE => 6  
FILE_PERMISSION_WRITE_READ => 6  
FILE_PERMISSION_ALL => 7

| Param | Type | Description |
|:--|:--|:--|
| `$Fields` | `array` | File 資料表權限相關欄位名稱與資料的映射 |
| `$ID` | `string` | FileID |
| `$AgentID` | `string` | UserID 或 UserGroupID |
| `$Scope` | `int` | 權限範圍，建議使用 FILE_PERMISSION_* 常數 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.8 SetUserPermission

```php
public function SetUserPermission($ID, $UserID, $Scope = FILE_PERMISSION_ALL)
```

設定用戶對檔案的權限  
`Scope` 參數建議使用 `FILE_PERMISSION_*` 常數:  
FILE_PERMISSION_DELETE => 1  
FILE_PERMISSION_WRITE => 2  
FILE_PERMISSION_READ => 4  
FILE_PERMISSION_WRITE_DELETE => 3  
FILE_PERMISSION_DELETE_WRITE => 3  
FILE_PERMISSION_READ_DELETE => 5  
FILE_PERMISSION_DELETE_READ => 5  
FILE_PERMISSION_READ_WRITE => 6  
FILE_PERMISSION_WRITE_READ => 6  
FILE_PERMISSION_ALL => 7

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$UserID` | `string` | UserID |
| `$Scope` | `int` | 權限範圍，建議使用 FILE_PERMISSION_* 常數 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.9 SetGroupPermission

```php
public function SetGroupPermission($ID, $UserGRPID, $Scope = FILE_PERMISSION_ALL)
```

設定用戶群組對檔案的權限  
`Scope` 參數建議使用 `FILE_PERMISSION_*` 常數:  
FILE_PERMISSION_DELETE => 1  
FILE_PERMISSION_WRITE => 2  
FILE_PERMISSION_READ => 4  
FILE_PERMISSION_WRITE_DELETE => 3  
FILE_PERMISSION_DELETE_WRITE => 3  
FILE_PERMISSION_READ_DELETE => 5  
FILE_PERMISSION_DELETE_READ => 5  
FILE_PERMISSION_READ_WRITE => 6  
FILE_PERMISSION_WRITE_READ => 6  
FILE_PERMISSION_ALL => 7

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$UserGRPID` | `string` | UserGRPID |
| `$Scope` | `int` | 權限範圍，建議使用 FILE_PERMISSION_* 常數 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.10 AlterSinglePermission(protected)

```php
protected function AlterSinglePermission($Field, $ID, $AgentID, $Allow)
```

設定用戶或用戶群組對檔案的單一權限

| Param | Type | Description |
|:--|:--|:--|
| `$Field` | `string` | 權限欄位名稱 |
| `$ID` | `string` | FileID |
| `$AgentID` | `string` | UserID 或 UserGroupID |
| `$Allow` | `bool` | true: 允許，false: 禁止 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.11 AlterUserReadPermission

```php
public function AlterUserReadPermission($ID, $UserID, $Allow)
```

設定用戶對檔案的讀取權限，不影響其他權限

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$UserID` | `string` | UserID |
| `$Allow` | `bool` | true: 允許讀取，false: 禁止讀取 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.12 AlterGroupReadPermission

```php
public function AlterGroupReadPermission($ID, $UserGRPID, $Allow)
```

設定用戶群組對檔案的讀取權限，不影響其他權限

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$UserGRPID` | `string` | UserGRPID |
| `$Allow` | `bool` | true: 允許讀取，false: 禁止讀取 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.13 AlterUserWritePermission

```php
public function AlterUserWritePermission($ID, $UserID, $Allow)
```

設定用戶對檔案的寫入權限，不影響其他權限

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$UserID` | `string` | UserID |
| `$Allow` | `bool` | true: 允許寫入，false: 禁止寫入 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.14 AlterGroupWritePermission

```php
public function AlterGroupWritePermission($ID, $UserGRPID, $Allow)
```

設定用戶對檔案的寫入權限，不影響其他權限

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$UserGRPID` | `string` | UserGRPID |
| `$Allow` | `bool` | true: 允許寫入，false: 禁止寫入 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.15 AlterUserDeletePermission

```php
public function AlterUserDeletePermission($ID, $UserID, $Allow)
```

設定用戶對檔案的刪除權限，不影響其他權限

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$UserID` | `string` | UserID |
| `$Allow` | `bool` | true: 允許刪除，false: 禁止刪除 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



## 19.16 AlterGroupDeletePermission

```php
public function AlterGroupDeletePermission($ID, $UserGRPID, $Allow)
```

設定用戶對檔案的刪除權限，不影響其他權限

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | FileID |
| `$UserGRPID` | `string` | UserGRPID |
| `$Allow` | `bool` | true: 允許刪除，false: 禁止刪除 |

**回傳**

`bool` `true`: 成功，`false`: 失敗



# 20. DBSMOD_Goods extends DBSMOD


## 20.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 20.2 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆物料資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 20.3 Create

```php
public function Create($R_Data)
```

新增物料資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | Goods 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 20.4 Update

```php
public function Update($ID, $R_Data)
```

更新物料資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsID |
| `$R_Data` | `array` | Goods 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 20.5 Delete

```php
public function Delete($ID)
```

刪除物料、物料庫存等資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsID |

**回傳**

`bool`



## 20.6 CreateStock

```php
public function CreateStock($R_Data)
```

新增物料資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | GoodsStock 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 20.7 SelectStockByGoodsID

```php
public function SelectStockByGoodsID($ID, $Field_Array = array())
```

查詢單筆物料庫存資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsID |
| `$Field_Array` | `array` | 查詢的 GoodsStock 資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 20.8 UpdateStockByGoodsID

```php
public function UpdateStockByGoodsID($ID, $R_Data)
```

更新物料庫存資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsID |
| `$R_Data` | `array` | GoodsStock 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 20.9 UpdateStockNewQTY

```php
public function UpdateStockNewQTY($GoodsID, $QTY, $Flag = STOCK_OVERWRITE)
```

修改庫存的新品數量 (以 GoodsID 為索引)

| Param | Type | Description |
|:--|:--|:--|
| `$GoodsID` | `string` | GoodsID |
| `$QTY` | `int` | 修改數量 |
| `$Flag` | `int` | `STOCK_OVERWRITE`: 以 $QTY 覆寫庫存新品數量；`STOCK_PLUS`: 既有的庫存數量與 $QTY 相加 |

**回傳**

`bool` 修改成功回傳 ``true``，反之回傳 ``false``



## 20.10 UpdateStockNewQTYByProductID

```php
public function UpdateStockNewQTYByProductID($PDTIFOID, $QTY, $Flag = STOCK_OVERWRITE)
```

修改庫存的新品數量 (以 PDTIFOID 為索引)

| Param | Type | Description |
|:--|:--|:--|
| `$PDTIFOID` | `string` | PDTIFOID |
| `$QTY` | `int` | 修改數量 |
| `$Flag` | `int` | `STOCK_OVERWRITE`: 以 $QTY 覆寫庫存新品數量；`STOCK_PLUS`: 既有的庫存數量與 $QTY 相加 |

**回傳**

`bool` 修改成功回傳 ``true``，反之回傳 ``false``



## 20.11 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 GoodsTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 20.12 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 GoodsTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | GoodsTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 20.13 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 GoodsTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsTYPID |
| `$R_Data` | `array` | GoodsTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 20.14 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 GoodsTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsTYPID |

**回傳**

`bool`



## 20.15 UpdateTYPIFOCNT(protected)

```php
protected function UpdateTYPIFOCNT($ID, $Count = 1)
```

更新物料類別資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | GoodsTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`false`



## 20.16 AppendRLVProduct

```php
public function AppendRLVProduct($GoodsID, $PDTIFOID, $OptionSet)
```

新增產品與物料的關聯

| Param | Type | Description |
|:--|:--|:--|
| `$GoodsID` | `string` | GoodsID |
| `$PDTIFOID` | `string` | PDTIFOID |
| `$OptionSet` | `string` | 規格關聯陣列的JSON字串，寫入 `RT_PDTIFO_Goods_Tb.AvailableOptionSet` 欄位 |

**回傳**

`bool`



## 20.17 RemoveRLVProduct

```php
public function RemoveRLVProduct($GoodsID, $PDTIFOID)
```

移除產品與物料的關聯

| Param | Type | Description |
|:--|:--|:--|
| `$GoodsID` | `string` | GoodsID |
| `$PDTIFOID` | `string` | PDTIFOID |

**回傳**

`bool`



# 21. DBSMOD_INV extends DBSMOD


## 21.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$StatusFlagKeys` | `array` | `INVIFO.StatusFlag` 訂單每個旗標所象徵的狀態 |
| `$RequiredStatus` | `array` | `INVIFO.StatusFlag` 初始即不為空值的旗標 |
| `$AutoCompleteStatus` | `array` | `INVIFO.StatusFlag` 初始即為完成的旗標 |
| `$DateTimeFieldMapping` | `array` | **(protected)** `INVIFO.StatusFlag` 旗標對應的時間 |
| `$INVEventFlagKeys` | `array` | `INVIFO.EventFlag` 每個旗標所象徵的狀態 |
| `$TradeSettings` | `ConfigTrade` | 交易稅率、價格小數位數等的設定物件 |


## 21.2 __construct

```php
public function __construct($DBSLink, $DBS, $TradeSettings = null)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | PDO 物件 |
| `$DBS` | `string` | 資料庫名稱 |
| `$TradeSettings` | `ConfigTrade` | 交易稅率、價格小數位數等的設定物件 |



## 21.3 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 21.4 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALINVID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 21.5 Create

```php
public function Create($R_Data, $ItemArray = array())
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | INVIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 21.6 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALINVID |
| `$R_Data` | `array` | INVIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 21.7 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALINVID |

**回傳**

`bool`



## 21.8 UpdateItem

```php
public function UpdateItem($SALODRITMID, $R_Data)
```

更新訂購項目

| Param | Type | Description |
|:--|:--|:--|
| `$SALODRITMID` | `string` |  |
| `$R_Data` | `array` |  |

**回傳**

`array`|`false`



## 21.9 CreateItem(protected)

```php
protected function CreateItem($R_Data)
```

建立訂購項目

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` |  |

**回傳**

`array`|`false`



## 21.10 GetInitStatusFlag(protected)

```php
protected function GetInitStatusFlag()
```

取得初始狀態旗標字串

**回傳**

`string`



## 21.11 GetInvoiceForReceipt(protected)

```php
protected function GetInvoiceForReceipt($R_Data)
```

易發票開立

**回傳**

`string`



# 22. DBSMOD_Link extends DBSMOD


## 22.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 22.2 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | LinkIFOID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 22.3 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | LinkIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 22.4 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | LinkIFOID |
| `$R_Data` | `array` | LinkIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 22.5 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | LinkIFOID |

**回傳**

`bool`



# 23. DBSMOD_Link_enUS extends DBSMOD_Link


## 23.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



# 24. DBSMOD_Monitor extends DBSMOD


## 24.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$MonitorLogItemCacheValidDuration` | `int` | 監測記錄快取的效期 (秒) |


## 24.2 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 24.3 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorIFOID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 24.4 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | MonitorIFO 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.5 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorIFOID |
| `$R_Data` | `array` | MonitorIFO 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.6 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorIFOID |

**回傳**

`bool`



## 24.7 SelectLog

```php
public function SelectLog($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorLogID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 24.8 CreateLog

```php
public function CreateLog($R_Data, $MonitorIFOID)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | MonitorLog 資料表欄位名稱與資料的映射 |
| `$MonitorIFOID` | `string` | MonitorIFOID |

**回傳**

`array`|`false`



## 24.9 UpdateLog

```php
public function UpdateLog($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorLogID |
| `$R_Data` | `array` | MonitorLog 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.10 DeleteLog

```php
public function DeleteLog($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorLogID |

**回傳**

`bool`



## 24.11 SelectITM

```php
public function SelectITM($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorITMID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 24.12 CreateITM

```php
public function CreateITM($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | MonitorITM 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.13 UpdateITM

```php
public function UpdateITM($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorITMID |
| `$R_Data` | `array` | MonitorITM 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.14 DeleteITM

```php
public function DeleteITM($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorITMID |

**回傳**

`bool`



## 24.15 SelectDEV

```php
public function SelectDEV($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorDEVID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 24.16 CreateDEV

```php
public function CreateDEV($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | MonitorDEV 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.17 UpdateDEV

```php
public function UpdateDEV($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorDEVID |
| `$R_Data` | `array` | MonitorDEV 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.18 DeleteDEV

```php
public function DeleteDEV($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorDEVID |

**回傳**

`bool`



## 24.19 SelectDEVTYP

```php
public function SelectDEVTYP($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorDEVTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 24.20 CreateDEVTYP

```php
public function CreateDEVTYP($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | MonitorDEVTYP 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.21 UpdateDEVTYP

```php
public function UpdateDEVTYP($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorDEVTYPID |
| `$R_Data` | `array` | MonitorDEVTYP 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 24.22 DeleteDEVTYP

```php
public function DeleteDEVTYP($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorDEVTYPID |

**回傳**

`bool`



## 24.23 UpdateDEVTYPIFOCNT(protected)

```php
protected function UpdateDEVTYPIFOCNT($ID, $Count = 1)
```

更新資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | MonitorDEVTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`bool`



## 24.24 CreateLogItem

```php
public function CreateLogItem($R_Data, $MonitorLogID)
```

新增監測紀錄

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | MonitorLog 資料表欄位名稱與資料的映射，必須包含 MonitorLogID |

**回傳**

`array`|`false`



## 24.25 ClearExpiredLogItemCache

```php
public function ClearExpiredLogItemCache($CacheTableName)
```

清理過期的監測紀錄快取

| Param | Type | Description |
|:--|:--|:--|
| `$CacheTableName` | `string` | 快取資料表名稱 |

**回傳**

`true`



# 25. DBSMOD_OAuthToken extends DBSMOD


## 25.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$ExpireTime` | `int` | 令牌有效期 (秒)，預設為 3600 秒 (1 小時) |


## 25.2 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 25.3 CreateToken

```php
public function CreateToken($UserID, $PrivateKeyUri, $ClientID = '', $Scopes = array())
```

產生令牌並儲存於 OAuthACSToken，回傳令牌物件

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | 使用者 ID |
| `$PrivateKeyUri` | `string` | 私鑰位置 |
| `$ClientID` | `string` | 客戶端 ID |
| `$Scopes` | `array` | 權限範圍 |

**回傳**

JWTEntity



## 25.4 CheckToken

```php
public function CheckToken($JWTString, $PublicKeyUri)
```

檢查令牌是否有效 (UserToken)

| Param | Type | Description |
|:--|:--|:--|
| `$JWTString` | `string` | 待驗證的令牌 |
| `$PublicKeyUri` | `string` | 公鑰位置 |

**回傳**

JWTEntity|`false` 回傳 ACSToken 物件，若失敗則回傳 `false`



## 25.5 DeleteToken

```php
public function DeleteToken($JWTString, $PublicKeyUri)
```

刪除指定令牌

| Param | Type | Description |
|:--|:--|:--|
| `$JWTString` | `string` | 待刪除的令牌 |
| `$PublicKeyUri` | `string` | 公鑰位置 |

**回傳**

`true`



## 25.6 GenerateID(protected)

```php
protected function GenerateID($Length = 40)
```

產生隨機 ID (16 進位)

| Param | Type | Description |
|:--|:--|:--|
| `$Length` | `int` | ID 長度 |

**回傳**

`string`



## 25.7 IsRevoked(protected)

```php
protected function IsRevoked($JTI)
```

檢查令牌是否已被刪除

| Param | Type | Description |
|:--|:--|:--|
| `$JTI` | `string` | 令牌 ID |

**回傳**

`bool`ean 回傳 `true` 表示已被刪除



# 26. DBSMOD_PDT extends DBSMOD


## 26.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$TradeSettings` | `ConfigTrade` | 控制自動建立物料資料的參數設定物件 |


## 26.2 __construct

```php
public function __construct($DBSLink, $DBS, $TradeSettings = null)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | PDO 物件 |
| `$DBS` | `string` | 資料庫名稱 |
| `$TradeSettings` | `ConfigTrade` | 交易稅率、價格小數位數等的設定物件 |



## 26.3 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 26.4 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆產品資料  
若引數 `$Field_Array` 包括 `PDTIFOTYPID` 則同時查詢相關聯的產品類別，並回傳所有產品類別的 `PDTIFOTYPID` 的數值陣列

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 26.5 Create

```php
public function Create($R_Data)
```

新增產品、產品庫存(庫存0)、產品類別關聯等資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | PDTIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 26.6 Update

```php
public function Update($ID, $R_Data)
```

更新產品資料  
若引數 `$R_Data` 包含 `PDTIFOTYPID`，則更新產品類別關聯

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOID |
| `$R_Data` | `array` | PDTIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 26.7 Delete

```php
public function Delete($ID)
```

刪除產品、產品庫存、產品類別關聯等資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOID |

**回傳**

`bool`



## 26.8 AppendRLVTYP

```php
public function AppendRLVTYP($ID, $TYPID)
```

新增產品與產品類別的關聯

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOID |
| `$TYPID` | `string` | PDTIFOTYPID |

**回傳**

`bool`



## 26.9 RemoveRLVTYP

```php
public function RemoveRLVTYP($ID, $TYPID)
```

移除產品與產品類別的關聯

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOID |
| `$TYPID` | `string` | PDTIFOTYPID |

**回傳**

`bool`



## 26.10 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 PDTIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 26.11 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 PDTIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | PDTIFOTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 26.12 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 PDTIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOTYPID |
| `$R_Data` | `array` | PDTIFOTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 26.13 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 PDTIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOTYPID |

**回傳**

`bool`



## 26.14 UpdateTYPIFOCNT(protected)

```php
protected function UpdateTYPIFOCNT($ID, $Count = 1)
```

更新產品類別資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`false`



## 26.15 AppendRLVCNR

```php
public function AppendRLVCNR($ID, $CNRID, $R_Data = array())
```

新增產品與專櫃的關聯

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOID |
| `$CNRID` | `string` | CNRIFOID |
| `$R_Data` | `array` | 新增到 'RT_CNRPDT` 的資料 |

**回傳**

`bool`



## 26.16 RemoveRLVCNR

```php
public function RemoveRLVCNR($ID, $CNRID)
```

移除產品與專櫃的關聯

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PDTIFOID |
| `$CNRID` | `string` | CNRIFOID |

**回傳**

`bool`



## 26.17 SelectCNR

```php
public function SelectCNR($CNRID, $Field_Array = array())
```

查詢單筆專櫃資料

| Param | Type | Description |
|:--|:--|:--|
| `$CNRID` | `string` | CNRIFOID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 26.18 CreateCNR

```php
public function CreateCNR($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | CNRIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 26.19 UpdateCNR

```php
public function UpdateCNR($CNRID, $R_Data)
```

更新專櫃資料

| Param | Type | Description |
|:--|:--|:--|
| `$CNRID` | `string` | CNRIFOID |
| `$R_Data` | `array` | CNRIFO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 26.20 DeleteCNR

```php
public function DeleteCNR($CNRID)
```

刪除專櫃資料

| Param | Type | Description |
|:--|:--|:--|
| `$CNRID` | `string` | CNRIFOID |

**回傳**

`bool`



## 26.21 SelectCNRTYP

```php
public function SelectCNRTYP($CNRID, $Field_Array = array())
```

查詢單筆 CNRIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$CNRID` | `string` | CNRIFOTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 26.22 CreateCNRTYP

```php
public function CreateCNRTYP($R_Data)
```

新增資料 CNRIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | CNRIFOTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 26.23 UpdateCNRTYP

```php
public function UpdateCNRTYP($CNRID, $R_Data)
```

更新資料 CNRIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$CNRID` | `string` | CNRIFOTYPID |
| `$R_Data` | `array` | CNRIFOTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 26.24 DeleteCNRTYP

```php
public function DeleteCNRTYP($CNRID)
```

刪除資料 CNRIFOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$CNRID` | `string` | CNRIFOTYPID |

**回傳**

`bool`



## 26.25 UpdateCNRTYPIFOCNT(protected)

```php
protected function UpdateCNRTYPIFOCNT($CNRID, $Count = 1)
```

更新 CNRIFOTYP 資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$CNRID` | `string` | CNRIFOTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`bool`



# 27. DBSMOD_PHSSAL extends DBSMOD


## 27.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$StatusFlagKeys` | `array` | `PHSSAL.StatusFlag` 訂單每個旗標所象徵的狀態 |
| `$RequiredStatus` | `array` | `PHSSAL.StatusFlag` 初始即不為空值的旗標 |
| `$AutoCompleteStatus` | `array` | `PHSSAL.StatusFlag` 初始即為完成的旗標 |
| `$TradeSettings` | `ConfigTrade` | 交易稅率、價格小數位數等的設定物件 |


## 27.2 __construct

```php
public function __construct($DBSLink, $DBS, $TradeSettings = null)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | PDO 物件 |
| `$DBS` | `string` | 資料庫名稱 |
| `$TradeSettings` | `ConfigTrade` | 交易稅率、價格小數位數等的設定物件 |



## 27.3 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 27.4 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PHSSALID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 27.5 Create

```php
public function Create($R_Data, $ItemArray = array())
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | PHSSAL資料表欄位名稱與資料的映射 |
| `$ItemArray` | `array` | 訂購項目的數值陣列，每個元素為包含 `UnitPrice`、`QTY` 等鍵的關聯陣列 |

**回傳**

`array`|`false`



## 27.6 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PHSSALID |
| `$R_Data` | `array` | PHSSAL資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 27.7 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PHSSALID |

**回傳**

`bool`



## 27.8 UpdateItem

```php
public function UpdateItem($PHSSALITMID, $R_Data)
```

更新訂購項目

| Param | Type | Description |
|:--|:--|:--|
| `$PHSSALITMID` | `string` |  |
| `$R_Data` | `array` |  |

**回傳**

`array`|`false`



## 27.9 CreateItem(protected)

```php
protected function CreateItem($R_Data)
```

建立訂購項目

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` |  |

**回傳**

`array`|`false`



## 27.10 GetInitStatusFlag(protected)

```php
protected function GetInitStatusFlag()
```

取得初始狀態旗標字串

**回傳**

`string`



# 28. DBSMOD_PMO extends DBSMOD


## 28.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 28.2 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆促銷資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMOID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 28.3 Create

```php
public function Create($R_Data)
```

新增促銷

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | PMO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 28.4 Update

```php
public function Update($ID, $R_Data)
```

更新促銷

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMOID |
| `$R_Data` | `array` | PMO資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 28.5 Delete

```php
public function Delete($ID)
```

刪除促銷資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMOID |

**回傳**

`bool`



## 28.6 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 PMOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMOTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 28.7 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 PMOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | PMOTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 28.8 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 PMOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMOTYPID |
| `$R_Data` | `array` | PMOTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 28.9 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 PMOTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMOTYPID |

**回傳**

`bool`



## 28.10 SelectPMOPDTDCN

```php
public function SelectPMOPDTDCN($ID, $Field_Array = array())
```

查詢單筆 促銷產品折扣

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMOPDTDCNID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 28.11 CreatePMOPDTDCN

```php
public function CreatePMOPDTDCN($R_Data)
```

新增資料 促銷產品折扣

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | PMOPDTDCN資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 28.12 UpdatePMOPDTDCN

```php
public function UpdatePMOPDTDCN($PMOPDTDCNID, $R_Data)
```

更新 促銷產品折扣

| Param | Type | Description |
|:--|:--|:--|
| `$PMOPDTDCNID` | `string` | PMOPDTDCNID |
| `$R_Data` | `array` | PMOPDTDCN資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 28.13 DeletePMOPDTDCN

```php
public function DeletePMOPDTDCN($PMOPDTDCNID)
```

刪除 促銷產品折扣

| Param | Type | Description |
|:--|:--|:--|
| `$PMOPDTDCNID` | `string` | PMOPDTDCNID |

**回傳**

`bool`



# 29. DBSMOD_PMSGRP extends DBSMOD


## 29.2 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆權限群組

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMSGRPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 29.3 Create

```php
public function Create($R_Data)
```

新增權限群組

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | PMSGRP 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 29.4 Update

```php
public function Update($ID, $R_Data)
```

更新權限群組

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMSGRPID |
| `$R_Data` | `array` | PMSGRP 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 29.5 Delete

```php
public function Delete($ID)
```

刪除權限群組

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMSGRPID |

**回傳**

`bool`



## 29.6 SelectPMSScope

```php
public function SelectPMSScope($ID, $Field_Array = array())
```

查詢單筆權限範圍

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMSGRPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 29.7 CreatePMSScope

```php
public function CreatePMSScope($R_Data)
```

新增權限範圍

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | PMSScope 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 29.8 UpdatePMSScope

```php
public function UpdatePMSScope($ID, $R_Data)
```

更新權限範圍

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMSScopeID |
| `$R_Data` | `array` | PMSScope 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 29.9 DeletePMSScope

```php
public function DeletePMSScope($ID)
```

刪除權限範圍

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | PMSScopeID |

**回傳**

`bool`



## 29.10 AppendPMSScope

```php
public function AppendPMSScope($PMSGRPID, $PMSScopeID)
```

新增權限群組與權限範圍關聯

| Param | Type | Description |
|:--|:--|:--|
| `$PMSGRPID` | `string` | PMSGRPID |
| `$PMSScopeID` | `string` | PMSScopeID |

**回傳**

`bool`



## 29.11 RemovePMSScope

```php
public function RemovePMSScope($PMSGRPID, $PMSScopeID)
```

移除權限群組與權限範圍關聯

| Param | Type | Description |
|:--|:--|:--|
| `$PMSGRPID` | `string` | PMSGRPID |
| `$PMSScopeID` | `string` | PMSScopeID |

**回傳**

`bool`



## 29.12 AppendPMSScopeByDCP

```php
public function AppendPMSScopeByDCP($PMSGRPID, $ScopeDCP)
```

新增權限群組與權限範圍關聯，以權限範圍的描述為索引

| Param | Type | Description |
|:--|:--|:--|
| `$PMSGRPID` | `string` | PMSGRPID |
| `$ScopeDCP` | `string` | 權限範圍描述 (PMSScope.DCP) |

**回傳**

`bool`



## 29.13 RemovePMSScopeByDCP

```php
public function RemovePMSScopeByDCP($PMSGRPID, $ScopeDCP)
```

移除權限群組與權限範圍關聯，以權限範圍的描述為索引

| Param | Type | Description |
|:--|:--|:--|
| `$PMSGRPID` | `string` | PMSGRPID |
| `$ScopeDCP` | `string` | 權限範圍描述 (PMSScope.DCP) |

**回傳**

`bool`



## 29.14 CheckUser

```php
public function CheckUser($UserID, $Scope)
```

檢查使用者對指定權限範圍是否有權限

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | UserID |
| `$Scope` | `string` | 權限範圍的定義 (PMSScope.Scope) |

**回傳**

`bool`



# 30. DBSMOD_RSCDOC extends DBSMOD_DOC


## 30.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 30.2 AppendCourseTOCItem

```php
public function AppendCourseTOCItem($RSCDOCID, $CourseTOCITMID)
```

新增資源文件與課程目錄項目關聯

| Param | Type | Description |
|:--|:--|:--|
| `$RSCDOCID` | `string` | RSCDOCID |
| `$CourseTOCITMID` | `string` | CourseTOCITMID |

**回傳**

`bool`



## 30.3 RemoveCourseTOCItem

```php
public function RemoveCourseTOCItem($RSCDOCID, $CourseTOCITMID)
```

移除資源文件與課程目錄項目關聯

| Param | Type | Description |
|:--|:--|:--|
| `$RSCDOCID` | `string` | RSCDOCID |
| `$CourseTOCITMID` | `string` | CourseTOCITMID |

**回傳**

`bool`



## 30.4 AppendTextbookTOCItem

```php
public function AppendTextbookTOCItem($RSCDOCID, $TextbookTOCITMID)
```

新增資源文件與課程目錄項目關聯

| Param | Type | Description |
|:--|:--|:--|
| `$RSCDOCID` | `string` | RSCDOCID |
| `$TextbookTOCITMID` | `string` | TextbookTOCITMID |

**回傳**

`bool`



## 30.5 RemoveTextbookTOCItem

```php
public function RemoveTextbookTOCItem($RSCDOCID, $TextbookTOCITMID)
```

移除資源文件與課程目錄項目關聯

| Param | Type | Description |
|:--|:--|:--|
| `$RSCDOCID` | `string` | RSCDOCID |
| `$TextbookTOCITMID` | `string` | TextbookTOCITMID |

**回傳**

`bool`



# 31. DBSMOD_SALODR extends DBSMOD


## 31.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$StatusFlagKeys` | `array` | `SALODR.StatusFlag` 訂單每個旗標所象徵的狀態 |
| `$RequiredStatus` | `array` | `SALODR.StatusFlag` 初始即不為空值的旗標 |
| `$AutoCompleteStatus` | `array` | `SALODR.StatusFlag` 初始即為完成的旗標 |
| `$DateTimeFieldMapping` | `array` | **(protected)** `SALODR.StatusFlag` 旗標對應的時間 |
| `$TradeSettings` | `ConfigTrade` | 交易稅率、價格小數位數等的交易參數設定物件 |


## 31.2 __construct

```php
public function __construct($DBSLink, $DBS, $TradeSettings = null)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | PDO 物件 |
| `$DBS` | `string` | 資料庫名稱 |
| `$TradeSettings` | `ConfigTrade` | 交易稅率、價格小數位數等的設定物件 |



## 31.3 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 31.4 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 31.5 Create

```php
public function Create($R_Data, $ItemArray = [])
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | SALODR資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 31.6 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$R_Data` | `array` | SALODR資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 31.7 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |

**回傳**

`bool`



## 31.8 SelectItems

```php
public function SelectItems($ID, $Field_Array = ['SALODRITMID'])
```

SelectItems

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$Field_Array` | `array` | 欄位名稱陣列 |

**回傳**

`array`|`false`



## 31.9 UpdateItem

```php
public function UpdateItem($ID, $SALODRITMID, $R_Data, $ReCalculate = true)
```

更新訂購項目，但若訂單符合以下任一狀態，則不執行: 待出貨、已出貨、待退貨、已退貨、待退款、已退款、待結案、已結案  
若要刪除訂購項目，請將 `$R_Data['QTY]` 設為 `0`。

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODRITMID` | `string` | SALODRITMID |
| `$R_Data` | `array` | 訂購項目的資料 |
| `$ReCalculate` | `bool` | 是否重新計算訂單資料內的總價 |

**回傳**

`array`|`false`



## 31.10 CreateItem

```php
public function CreateItem($ID, $R_Data)
```

建立訂購項目

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$R_Data` | `array` | 訂購項目的資料 |

**回傳**

`array`|`false`



## 31.11 ProcessAmount(protected)

```php
protected function ProcessAmount($ItemArray, $DELPrice = 0)
```

加總訂單項目的總價，得到訂單的 `TotalPrice`、`SALPrice`、`SALTax` 等資料  
```php  
$ItemArray = [  
   [ 'UnitPrice' => 100, 'QTY' => 2],  
   [ 'UnitPrice' => 80, 'QTY' => 3 ]  
];  
$Mod = new DBSMOD_SALODR($Link, $DB_TABLE);  
$Sum = $Mod->ProcessAmount($ItemArray, 100); //第二個參數為訂單的 `DELPrice`  
echo $Sum['TotalPrice']; //540  
echo $Sum['SALPrice']; //418  
echo $Sum['SALTax']; //22  
```

| Param | Type | Description |
|:--|:--|:--|
| `$ItemArray` | `array` |  |
| `$DELPrice` | `int` |  |



## 31.12 GetInitStatusFlag(protected)

```php
protected function GetInitStatusFlag()
```

取得初始狀態旗標字串

**回傳**

`string`



## 31.13 FireStatusEvent(protected)

```php
protected function FireStatusEvent($ID, $NewStatusFlag, $ORIStatusFlag, $SALODR_Data = array())
```

觸發訂單狀態變更的事件

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$NewStatusFlag` | `string` | 新狀態旗標字串 |
| `$ORIStatusFlag` | `string` | 原狀態旗標字串 |
| `$SALODR_Data` | `array` | SALODR資料 |



## 31.14 SendStatusNotice(protected)

```php
protected function SendStatusNotice($ID, $EventName, $SALODR_Data = array())
```

發送狀態變更通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$EventName` | `string` | 事件名稱 |
| `$SALODR_Data` | `array` | SALODR 資料 |



## 31.15 CreateReturnFromSALODR

```php
public function CreateReturnFromSALODR($ID, $ItemArray = array())
```

從 SALODR 複製資料以建立新的一筆 SALReturnODR  
(只支援一筆訂單一筆退貨)

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$ItemArray` | `array` |  |



## 31.16 CreatePHSSALFromSALODR(protected)

```php
protected function CreatePHSSALFromSALODR($ID, $PHSSALTYPID = PHSSALTYPID_SALES)
```

從 SALODR|SALReturnODR 複製資料以建立新的一筆 PHSSAL

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$PHSSALTYPID` | `string` | 銷貨單類別 ID，可能的值為正常銷貨 `PHSSALTYPID_SALES` 及銷貨退回 `PHSSALTYPID_SALES_RETURN` |

**回傳**

`array`|`false` 回傳包含新建立銷貨單的 PHSSALID 及 SERNO 的關聯陣列



## 31.17 CreateINVFromSALODR(protected)

```php
protected function CreateINVFromSALODR($ID)
```

從 SALODR 複製資料以建立新的一筆 INVIFO

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |

**回傳**

`array`|`false` 回傳包含新建立發票的 INVIFOID 及 SERNO 的關聯陣列



## 31.18 OnWaitingDeal(protected)

```php
protected function OnWaitingDeal($ID, $SALODR_Data = array())
```

訂單狀態事件-等待交易成立：發送訂單待審核通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.19 OnDeal(protected)

```php
protected function OnDeal($ID, $SALODR_Data = array())
```

訂單狀態事件-交易成立：新建關聯資料表

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.20 OnWaitingPayment(protected)

```php
protected function OnWaitingPayment($ID, $SALODR_Data = array())
```

訂單狀態事件-待付款：發送待付款通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.21 OnPayment(protected)

```php
protected function OnPayment($ID, $SALODR_Data = array())
```

訂單狀態事件-完成付款：發送已付款通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.22 OnWaitingDelivery(protected)

```php
protected function OnWaitingDelivery($ID, $SALODR_Data = array())
```

訂單狀態事件-完成出貨：發送已出貨通知/扣除庫存/新建出貨單/更新關聯表

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.23 OnDelivery(protected)

```php
protected function OnDelivery($ID, $SALODR_Data = array())
```

訂單狀態事件-完成出貨：新建銷貨單/新建發票/發送已出貨通知/更新關聯表

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.24 OnWaitingReturn(protected)

```php
protected function OnWaitingReturn($ID, $SALODR_Data = array())
```

訂單狀態事件-待退貨：新建退回單/發送待退貨通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.25 OnReturn(protected)

```php
protected function OnReturn($ID, $SALODR_Data = array())
```

訂單狀態事件-已退貨：新建銷貨退回單/更新發票/更新庫存/更新關聯資料表

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.26 OnWaitingRefund(protected)

```php
protected function OnWaitingRefund($ID, $SALODR_Data = array())
```

(暫不實作) 訂單狀態事件-等待退款：發送等待退款通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.27 OnRefund(protected)

```php
protected function OnRefund($ID, $SALODR_Data = array())
```

(暫不實作) 訂單狀態事件-已退款：更新退回訂單/更新退回訂單/更新銷貨退回單/發送已退款通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.28 OnWaitingClose(protected)

```php
protected function OnWaitingClose($ID, $SALODR_Data = array())
```

訂單狀態事件-待結案：發送待結案通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



## 31.29 OnClose(protected)

```php
protected function OnClose($ID, $SALODR_Data = array())
```

(暫不實作) 訂單狀態事件-已結案：發送已結案通知

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | SALODRID |
| `$SALODR_Data` | `array` | SALODR資料 |

**回傳**

`bool`



# 32. DBSMOD_Textbook extends DBSMOD


## 32.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 32.2 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆教科書資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 32.3 Create

```php
public function Create($R_Data)
```

新增教科書資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | Textbook 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 32.4 Update

```php
public function Update($ID, $R_Data)
```

更新教科書資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookID |
| `$R_Data` | `array` | Textbook 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 32.5 Delete

```php
public function Delete($ID)
```

刪除教科書資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookID |

**回傳**

`bool`



## 32.6 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 TextbookTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 32.7 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 TextbookTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | TextbookTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 32.8 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 TextbookTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookTYPID |
| `$R_Data` | `array` | TextbookTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 32.9 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 TextbookTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookTYPID |

**回傳**

`bool`



## 32.10 UpdateTYPIFOCNT(protected)

```php
protected function UpdateTYPIFOCNT($ID, $Count = 1)
```

更新教科書類別資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`false`



## 32.11 SelectTOCItem

```php
public function SelectTOCItem($ID, $Field_Array = array())
```

取得教科書目錄項目

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookTOCITMID |
| `$Field_Array` | `array` | 欄位名稱陣列 |

**回傳**

`array`|`false`



## 32.12 CreateTOCItem

```php
public function CreateTOCItem($R_Data, $PreviousItemID = null)
```

建立教科書目錄項目，並更新同書本中其他章節的序號

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | 教科書目錄項目的資料 |
| `$PreviousItemID` | `string` | 排序在前一個的教科書目錄項目ID |

**回傳**

`array`|`false`



## 32.13 UpdateTOCItem

```php
public function UpdateTOCItem($ID, $R_Data)
```

更新教科書目錄項目，若更新的資料包含序號，同時更新同書本中其他章節的序號

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookTOCITMID |
| `$R_Data` | `array` | 教科書目錄項目的資料 |

**回傳**

`array`|`false`



## 32.14 DeleteTOCItem

```php
public function DeleteTOCItem($ID)
```

刪除教科書目錄項目，並更新同書本中其他章節的序號

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | TextbookTOCITMID |

**回傳**

`bool`



# 33. DBSMOD_User extends DBSMOD


## 33.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$VRFFlagKeys` | `array` | `User.VRFFlag` 旗標各字元對應的鍵，映射到 `UserAUT.AUTVRFSet` 的鍵。<br>陣列中第 `0` 位對應到旗標字串的最右側字元。 |
| `$RequiredVRF` | `array` | 用戶登入前必須通過的驗證 |
| `$MODSalt` | `string` | 模組內加密使用的鹽 |


## 33.2 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 33.3 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 33.4 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | User資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 33.5 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserID |
| `$R_Data` | `array` | User資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 33.6 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserID |

**回傳**

`bool` 刪除資料成功則回傳 ``true``



## 33.7 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 UserTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 33.8 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 UserTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | UserTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 33.9 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 UserTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserTYPID |
| `$R_Data` | `array` | UserTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 33.10 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 UserTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserTYPID |

**回傳**

`bool`



## 33.11 SelectAUT

```php
public function SelectAUT($ID, $Field_Array = array())
```

查詢單筆用戶驗證資料 (以 UserID 為索引)

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 33.12 SelectCUS

```php
public function SelectCUS($UserID, $Field_Array = array())
```

查詢單筆用戶所屬廠商的關聯及廠商資料 (以 UserID 為索引)；每個用戶只能隸屬於一個廠商

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | UserID |
| `$Field_Array` | `array` | 查詢的 RT_CUS_User 及 CUSIFO 資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 33.13 UpdateCUS

```php
public function UpdateCUS($UserID, $R_Data)
```

更新或新建用戶所屬廠商的關聯 (以 UserID 為索引)；每個用戶只能隸屬於一個廠商

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserID |
| `$R_Data` | `array` | RT_CUS_User 資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 33.14 ProcessPIN(protected)

```php
protected function ProcessPIN($PIN)
```

雜湊處理密碼及登入帳號

| Param | Type | Description |
|:--|:--|:--|
| `$PIN` | `string` | 待雜湊處理的字串 |

**回傳**

`string` 回傳雜湊後的字串



## 33.15 ProcessAUTVRF(protected)

```php
protected function ProcessAUTVRF($VRFFlag, $ORISet = null)
```

從 `User.VRFFlag` 旗標字串產生 `UserAUT.AUTVRFSet` 格式的陣列

| Param | Type | Description |
|:--|:--|:--|
| `$VRFFlag` | `string` | `User.VRFFlag` 的值 |
| `$ORISet` | `array` | 修改前的 `UserAUT.AUTVRFSet` 解析成的關聯陣列 |

**回傳**

`array` 回傳 `UserAUT.AUTVRFSet` 格式的關聯陣列



## 33.16 Login

```php
public function Login($LoginName, $PIN1, $Field_Array = ['UserID', 'SERNO'], $UserTYP = null)
```

用戶以帳號密碼登入

| Param | Type | Description |
|:--|:--|:--|
| `$LoginName` | `string` | 用戶帳號 |
| `$PIN1` | `string` | 用戶密碼 |
| `$Field_Array` | `array` | 回傳時的用戶資料欄位，預設只包含 `UserID`, `SERNO` |
| `$UserTYP` | `string` | 指定的用戶類別，如 `MBR`, `EPY` |

**回傳**

`array`|`false` 登入成功時回傳包含令牌 `ACSToken` 的用戶資料，登入失敗時回傳 ``false``



## 33.17 SendNotice

```php
public function SendNotice($ID, $TPLDOCID, $ReplaceArray = array(), $SendMethod = NOTICE_EMAIL)
```

發送通知給用戶

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 用戶的 `UserID` |
| `$TPLDOCID` | `string` | 通知的範本文件 `REFDOCID` |
| `$ReplaceArray` | `array` | 待替換字串的關聯陣列 |
| `$SendMethod` | `int` | 發送途徑 |

**回傳**

`bool` 若成功發送即回傳 ``true``，反之則回傳 ``false``



## 33.18 ActivateEMLVRF

```php
public function ActivateEMLVRF($ID, $TPLDOCID)
```

發送電子信箱驗證信。  
信件中的驗證連結會包含兩組加密金鑰。

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 收信用戶的 UserID |
| `$TPLDOCID` | `string` | 電子信箱驗證信的文件範本 REFDOCID |

**回傳**

`bool` 發送成功即回傳 ``true``



## 33.19 ChangeAUTVRF(protected)

```php
protected function ChangeAUTVRF($UserID, $AUTKey, $State)
```

改變用戶驗證狀態

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | 待修改的用戶 UserID |
| `$AUTKey` | `string` | 待修改的驗證項目，必須是本物件屬性 `$VRFFlagKeys` 中的其中一個元素 |
| `$State` | `string` | 驗證狀態的新旗標字元:<br>- `-`: Null<br>- `F`: Failed<br>- `I`: InProcessing<br>- `S`: Success |

**回傳**

`bool` 若成功改變用戶驗證狀態則回傳 ``true``



## 33.20 ProcessEMLVRF

```php
public function ProcessEMLVRF($Key1, $Key2)
```

透過解密兩組金鑰驗證用戶的電子信箱

| Param | Type | Description |
|:--|:--|:--|
| `$Key1` | `string` | 第一組加密字串，對應到連結參數 `str1` |
| `$Key2` | `string` | 第二組加密字串，對應到連結參數 `str2` |

**回傳**

`bool` 通過驗證即回傳 ``true``



## 33.21 ProcessEMLVRFByUserID

```php
public function ProcessEMLVRFByUserID($UserID)
```

直接通過用戶的電子信箱驗證

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | 待通過電子信箱驗證的用戶 UserID |

**回傳**

`bool` 通過驗證即回傳 ``true``



## 33.22 ResetPIN

```php
public function ResetPIN($Recipient, $TPLDOCID, $SendMethod = NOTICE_EMAIL)
```

重置指定用戶的密碼為長度 8 位的字串，格式如 `/^[A-Z][a-z][0-9]{6}$/`，並發送通知給用戶

| Param | Type | Description |
|:--|:--|:--|
| `$Recipient` | `string` | 用戶的以下資訊中的任一個: `User.LoginName`, `User.EML1`, `User.MobileTEL1` |
| `$TPLDOCID` | `string` | 重置密碼通知的文件範本 REFDOCID |
| `$SendMethod` | `int` | 通知發送途徑 |

**回傳**

`bool` 發送成功即回傳 ``true``



## 33.23 ActivateOTP

```php
public function ActivateOTP($UserID, $TPLDOCID, $SendMethod = NOTICE_EMAIL, $Scope = array())
```

產生用戶 OTP，並發送給用戶

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | 用戶 UserID |
| `$TPLDOCID` | `string` | OTP 通知的文件範本 REFDOCID |
| `$SendMethod` | `int` | 通知發送途徑 |
| `$Scope` | `array` | OTP 作用範圍陣列，陣列中字串格式為 `{method}:{api}` eg. `array("get:user-info", "put:user-info")` |

**回傳**

`bool` 發送成功即回傳 ``true``



## 33.24 ProcessOTP

```php
public function ProcessOTP($Token, $WriteOffFlag = true)
```

驗證 OTP 是否正確  
```  
$Token = $_POST['token'];  
$Mod = new DBSMOD_User($this->DBSLink, $this->DBS);  
$Result = $Mod->ProcessOTP($Token);  
echo $Result['UserIFOID];        //0r47ckwc6jy60rf1  
echo $Result['UserID];           //0r47ckwc6jy60rf1  
echo $Result['UserAliasName];    //John Doe  
echo $Result['UserTYP];          //EPY  
echo $Result['SessionID];        //  
echo $Result['Scope];            //["get:user-info", "put:user-info"]  
echo $Result['ExpireDateTime];   //2022-01-01 00:00:00  
echo $Result['ACSToken];         //M7YdNTZhxPtQ8K4woqI9L0d...  
```

| Param | Type | Description |
|:--|:--|:--|
| `$Token` | `string` | OTP Token |
| `$WriteOffFlag` | `bool` | 是否註銷 OTP，預設為 `true` |

**回傳**

`array`|`false` 通過驗證時回傳包含令牌 `ACSToken` 的用戶資料，失敗時回傳 ``false``



## 33.25 UpdateTYPIFOCNT(protected)

```php
protected function UpdateTYPIFOCNT($ID, $Count = 1)
```

更新資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`bool`



# 34. DBSMOD_UserGRP extends DBSMOD


## 34.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 34.2 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserGRPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 34.3 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | UserGRP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 34.4 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserGRPID |
| `$R_Data` | `array` | UserGRP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 34.5 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | UserGRPID |

**回傳**

`bool` 刪除資料成功則回傳 ``true``



## 34.6 SelectRole

```php
public function SelectRole($ID, $Field_Array = array())
```

取得角色

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | RoleID |
| `$Field_Array` | `array` | 欄位名稱陣列 |

**回傳**

`array`|`false`



## 34.7 CreateRole

```php
public function CreateRole($R_Data)
```

建立角色

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | 角色的資料 |

**回傳**

`array`|`false`



## 34.8 UpdateRole

```php
public function UpdateRole($ID, $R_Data)
```

更新角色

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | RoleID |
| `$R_Data` | `array` | 角色的資料 |

**回傳**

`array`|`false`



## 34.9 DeleteRole

```php
public function DeleteRole($ID)
```

刪除角色

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | RoleID |

**回傳**

`bool`



## 34.10 AppendUser

```php
public function AppendUser($UserGRPID, $UserID, $RoleID = '', $GNLNote = '')
```

新增用戶群組與用戶關聯

| Param | Type | Description |
|:--|:--|:--|
| `$UserGRPID` | `string` | UserGRPID |
| `$UserID` | `string` | UserID |
| `$RoleID` | `string` | RoleID |
| `$GNLNote` | `string` | GNLNote |

**回傳**

`bool`



## 34.11 RemoveUser

```php
public function RemoveUser($UserGRPID, $UserID)
```

移除用戶群組與用戶關聯

| Param | Type | Description |
|:--|:--|:--|
| `$UserGRPID` | `string` | UserGRPID |
| `$UserID` | `string` | UserID |

**回傳**

`bool`



# 35. DBSMOD_UserToken extends DBSMOD


## 35.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$ExpireTime` | `int` | 一般令牌的效期 (秒) |
| `$TMPExpireTime` | `int` | 暫時令牌的效期 (秒) |


## 35.2 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 35.3 ClearExpiredTokenOnTable(protected)

```php
protected function ClearExpiredTokenOnTable($DBSTable)
```

清除過期的令牌

| Param | Type | Description |
|:--|:--|:--|
| `$DBSTable` | `string` | 清除的資料表名稱 |



## 35.4 DeleteByTokenOnTable(protected)

```php
protected function DeleteByTokenOnTable($DBSTable, $ACSToken)
```

刪除指定令牌

| Param | Type | Description |
|:--|:--|:--|
| `$DBSTable` | `string` | 令牌儲存的資料表名稱 |
| `$ACSToken` | `string` | 令牌 |

**回傳**

`true`



## 35.5 DeleteByUserOnTable(protected)

```php
protected function DeleteByUserOnTable($DBSTable, $UserID, $Condition = '')
```

刪除指定用戶的令牌，可透過 $Condition 參數指定刪除條件

| Param | Type | Description |
|:--|:--|:--|
| `$DBSTable` | `string` | 令牌儲存的資料表名稱 |
| `$UserID` | `string` | 用戶 UID |
| `$Condition` | `string` | 刪除條件：若為 Apple|Android|PC 則刪除指定裝置的令牌；若為日期格式，則刪除指定日期前產生的令牌；若為空值，則刪除所有令牌 |

**回傳**

`true`



## 35.6 CreateTokenOnTable(protected)

```php
protected function CreateTokenOnTable($DBSTable, $UserID, $UserTYP, $Scopes)
```

產生令牌，並儲存到指定的資料表，回傳令牌物件  
此方法不開放外部呼叫，請使用 DBSMOD_UserToken::CreateToken() 或 DBSMOD_UserToken::CreateTMPToken() 來產生令牌

| Param | Type | Description |
|:--|:--|:--|
| `$DBSTable` | `string` | 儲存令牌的資料表名稱 |
| `$UserID` | `string` | 用戶UID |
| `$UserTYP` | `string` | 用戶類型，可能的值為 MBR|EPY|CUS 及空字串，若為空字串，自動查詢 UserAUT.UserTYP 取得 |
| `$Scopes` | `array` | 列舉權限範圍的數值陣列 |

**回傳**

ACSTokenEntity|`false` 回傳 ACSToken 物件，若失敗則回傳 `false`



## 35.7 CheckTokenOnTable(protected)

```php
protected function CheckTokenOnTable($DBSTable, $ACSToken, $UserTYP = '', $CheckSource = false)
```

檢查令牌是否有效  
此方法不開放外部呼叫，請使用 DBSMOD_UserToken::CheckToken() 或 DBSMOD_UserToken::CheckTMPToken() 來檢查令牌

| Param | Type | Description |
|:--|:--|:--|
| `$DBSTable` | `string` | 儲存令牌的資料表名稱 |
| `$ACSToken` | `string` | 待驗證的令牌 |
| `$UserTYP` | `string` | 用戶類型，可能的值為 MBR|EPY|CUS，預設為空字串，表示不限制 |
| `$CheckSource` | `bool` | 是否檢查來源，預設為 false |

**回傳**

ACSTokenEntity|`false` 回傳 ACSToken 物件，若失敗則回傳 `false`



## 35.8 CreateToken

```php
public function CreateToken($UserID, $UserTYP = '', $Scopes = array())
```

產生令牌並儲存於 UserToken，回傳令牌物件

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | 用戶UID |
| `$UserTYP` | `string` | 用戶類型，可能的值為 MBR|EPY|CUS 及空字串，預設為空字串，自動查詢 UserAUT.UserTYP 取得 |
| `$Scopes` | `array` | 列舉權限範圍的數值陣列，預設為空陣列，表示不限制 |

**回傳**

ACSTokenEntity|`false` 回傳 ACSToken 物件，若失敗則回傳 `false`



## 35.9 CreateTMPToken

```php
public function CreateTMPToken($UserID, $UserTYP = '', $Scopes = array())
```

產生令牌並儲存於 TMPToken，回傳令牌物件

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | 用戶UID |
| `$UserTYP` | `string` | 用戶類型，可能的值為 MBR|EPY|CUS 及空字串，預設為空字串，自動查詢 UserAUT.UserTYP 取得 |
| `$Scopes` | `array` | 列舉權限範圍的數值陣列，預設為空陣列，表示不限制 |



## 35.10 DeleteToken

```php
public function DeleteToken($ACSToken)
```

刪除指定令牌 (UserToken)

| Param | Type | Description |
|:--|:--|:--|
| `$ACSToken` | `string` | 令牌 |

**回傳**

`true`



## 35.11 DeleteTMPToken

```php
public function DeleteTMPToken($ACSToken)
```

刪除指定令牌 (TMPToken)

| Param | Type | Description |
|:--|:--|:--|
| `$ACSToken` | `string` | 令牌 |

**回傳**

`true`



## 35.12 DeleteTokenByUser

```php
public function DeleteTokenByUser($UserID, $Condition = '')
```

刪除指定用戶的令牌，可透過 $Condition 參數指定刪除條件 (UserToken)

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | 用戶 UID |
| `$Condition` | `string` | 刪除條件：若為 Apple|Android|PC 則刪除指定裝置的令牌；若為日期格式，則刪除指定日期前產生的令牌；若為空值，則刪除所有令牌 |

**回傳**

`true`



## 35.13 DeleteTMPTokenByUser

```php
public function DeleteTMPTokenByUser($UserID, $Condition = '')
```

刪除指定用戶的令牌，可透過 $Condition 參數指定刪除條件 (TMPToken)

| Param | Type | Description |
|:--|:--|:--|
| `$UserID` | `string` | 用戶 UID |
| `$Condition` | `string` | 刪除條件：若為 Apple|Android|PC 則刪除指定裝置的令牌；若為日期格式，則刪除指定日期前產生的令牌；若為空值，則刪除所有令牌 |

**回傳**

`true`



## 35.14 CheckToken

```php
public function CheckToken($ACSToken, $UserTYP = '', $CheckSource = false)
```

檢查令牌是否有效 (UserToken)

| Param | Type | Description |
|:--|:--|:--|
| `$ACSToken` | `string` | 待驗證的令牌 |
| `$UserTYP` | `string` | 用戶類型，可能的值為 MBR|EPY|CUS，預設為空字串，表示不限制 |
| `$CheckSource` | `bool` | 是否檢查來源，預設為 false |

**回傳**

ACSTokenEntity|`false` 回傳 ACSToken 物件，若失敗則回傳 `false`



## 35.15 CheckTMPToken

```php
public function CheckTMPToken($ACSToken, $UserTYP = '', $CheckSource = false)
```

檢查令牌是否有效 (TMPToken)

| Param | Type | Description |
|:--|:--|:--|
| `$ACSToken` | `string` | 待驗證的令牌 |
| `$UserTYP` | `string` | 用戶類型，可能的值為 MBR|EPY|CUS，預設為空字串，表示不限制 |
| `$CheckSource` | `bool` | 是否檢查來源，預設為 false |

**回傳**

ACSTokenEntity|`false` 回傳 ACSToken 物件，若失敗則回傳 `false`



## 35.16 Hash(protected)

```php
protected function Hash($String)
```

雜湊字串

| Param | Type | Description |
|:--|:--|:--|
| `$String` | `string` | 待雜湊的字串 |

**回傳**

`string` 回傳雜湊後的字串



## 35.17 GetRandomToken(protected)

```php
protected function GetRandomToken()
```

產生 190~255 位的 62 進位亂數

**回傳**

`string` 回傳亂數



## 35.18 GetUserSource

```php
public function GetUserSource()
```

取得使用者來源資訊  
```php  
$Mod = new DBSMOD_UserToken($this->DBSLink, $this->DBS);  
$UserSource = $Mod->GetUserSource();  
print_r($UserSource);  
//Array(  
//    [user_ip] => '111.11.111.11'  
//    [user_agent] => 'PC'  
//)  
```

**回傳**

`array` 使用者來源資訊



# 36. DBSMOD_ViewSchema extends DBSMOD


## 36.1 SetTables(protected)

```php
protected function SetTables()
```

設定預設資料表參數 (實作抽象方法)

**回傳**

`array`



## 36.2 Select

```php
public function Select($ID, $Field_Array = array())
```

查詢單筆資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | ViewSchemaID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 36.3 Create

```php
public function Create($R_Data)
```

新增資料

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | ViewSchema資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 36.4 Update

```php
public function Update($ID, $R_Data)
```

更新資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | ViewSchemaID |
| `$R_Data` | `array` | ViewSchema資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 36.5 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | ViewSchemaID |

**回傳**

`bool`



## 36.6 SelectTYP

```php
public function SelectTYP($ID, $Field_Array = array())
```

查詢單筆 ViewSchemaTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | ViewSchemaTYPID |
| `$Field_Array` | `array` | 查詢的資料表欄位名稱陣列 |

**回傳**

`array`|`false`



## 36.7 CreateTYP

```php
public function CreateTYP($R_Data)
```

新增資料 ViewSchemaTYP

| Param | Type | Description |
|:--|:--|:--|
| `$R_Data` | `array` | ViewSchemaTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 36.8 UpdateTYP

```php
public function UpdateTYP($ID, $R_Data)
```

更新資料 ViewSchemaTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | ViewSchemaTYPID |
| `$R_Data` | `array` | ViewSchemaTYP資料表欄位名稱與資料的映射 |

**回傳**

`array`|`false`



## 36.9 DeleteTYP

```php
public function DeleteTYP($ID)
```

刪除資料 ViewSchemaTYP

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | ViewSchemaTYPID |

**回傳**

`bool`



## 36.10 UpdateTYPIFOCNT(protected)

```php
protected function UpdateTYPIFOCNT($ID, $Count = 1)
```

更新資料計數

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | ViewSchemaTYPID |
| `$Count` | `integer` | 計數待相加的數字 |

**回傳**

`int`|`bool`



## 36.11 MergeCommonSchema

```php
public function MergeCommonSchema($Content)
```

合併頁面內容的 FUI Schema 與包含頁首/頁尾的共通 FUI Schema，回傳完整頁面的 FUI Schema

| Param | Type | Description |
|:--|:--|:--|
| `$Content` | `array|string` | 網頁頁面內容的 FUI Schema，可以是關聯陣列或是 JSON 格式的字串 |

**回傳**

`array`|`false`



# 37. ACSTokenEntity


## 37.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Token` | `string` | 令牌 |
| `$UserTYP` | `string` | 用戶類型，如：MBR、EPY |
| `$UserID` | `string` | 用戶 UID，對應 User.UserID |
| `$UserIFOID` | `string` | 同 ACSToken::UserID，用戶 UID，對應 User.UserID |
| `$UserCode` | `string` | 用戶 UID 代碼雜湊 |
| `$UserAliasName` | `string` | 用戶名稱，對應 User.FullName |
| `$FullName` | `string` | 同 ACSToken::UserAliasName，用戶名稱，對應 User.FullName |
| `$ExpireDateTime` | `string` | 令牌到期時間 (YYYY-MM-DD HH:II:SS) |
| `$ExpireTimestamp` | `int` | 令牌到期時間戳記 |
| `$SessionID` | `string` | 用戶 SessionID |
| `$Scope` | `string` | 令牌權限範圍的 JSON 字串，如 '["get:member-real-name","put:member-real-name"]' |


## 37.2 __construct

```php
public function __construct($ACSToken, $UserTYP, $UserID, $UserCode, $UserAliasName, $ExpireTimestamp, $SessionID, $Scope)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$ACSToken` | `string` | 令牌 |
| `$UserTYP` | `string` | 用戶類型，如：MBR、EPY |
| `$UserID` | `string` | 用戶 UID，對應 User.UserID |
| `$UserCode` | `string` | 用戶 UID 代碼雜湊 |
| `$UserAliasName` | `string` | 用戶名稱，對應 User.FullName |
| `$ExpireTimestamp` | `int` | 令牌到期時間戳記 |
| `$SessionID` | `string` | 用戶 SessionID |
| `$Scope` | `string` | 令牌權限範圍的 JSON 字串，如 '["get:member-real-name","put:member-real-name"]' |



## 37.3 FromArray(static)

```php
static public function FromArray($Array)
```

從關聯陣列建構 ACSToken 物件的靜態方法

| Param | Type | Description |
|:--|:--|:--|
| `$Array` | `array` | 關聯陣列，鍵包括：ACSToken、UserTYP、UserID、UserCode、UserAliasName、ExpireTimestamp、SessionID、Scope |

**回傳**

ACSTokenEntity



## 37.4 ToArray

```php
public function ToArray()
```

輸出物件屬性為關聯陣列

**回傳**

`array`



# 38. Archive


## 38.1 __construct

```php
public function __construct($Path)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Path` | `string` | 壓縮檔案絕對路徑 |



## 38.2 GetFileInfo

```php
public function GetFileInfo($CreatorID, $CreatorName)
```

回傳以 File 資料表欄位名稱為鍵的關聯陣列，包括 Title, FileName, StoreDIRPath, FileSize, ContentTYP, CreatorID, CreatorName 等  
其中，Title 與 FileName 內容相同，為檔案名稱(含副檔名)

| Param | Type | Description |
|:--|:--|:--|
| `$CreatorID` | `string` |  |
| `$CreatorName` | `string` |  |

**回傳**

`array` 以 File 資料表欄位名稱為鍵的關聯陣列，包括 Title, FileName, StoreDIRPath, FileSize, ContentTYP, CreatorID, CreatorName 等



# 39. DBSTableEntity


## 39.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | PDO 物件 |
| `$DBS` | `string` | 資料庫名稱 |
| `$Name` | `string` | 資料表名稱 |
| `$PK` | `string` | 資料表主鍵的欄位名稱 |
| `$Fields` | `array` | **(protected)** 資料表欄位名稱的數值陣列 |
| `$JSONPath` | `string` | 存放資料表結構快取JSON的資料夾路徑 |


## 39.2 __construct

```php
public function __construct($Name, $DBSLink, $DBS)
```

類別建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Name` | `string` | 資料表名稱 |
| `$DBSLink` | `\PDO` | PDO 物件 |
| `$DBS` | `string` | 資料庫名稱 |



## 39.3 SetFields

```php
public function SetFields()
```

寫入屬性 Fields (資料表欄位名稱的數值陣列)



## 39.4 GetFields

```php
public function GetFields()
```

讀取屬性 Fields (資料表欄位名稱的數值陣列)

**回傳**

`array`



## 39.5 ValidateFields

```php
public function ValidateFields(array $Fields)
```

驗證欄位名稱是否被包含於物件中的屬性 Fields

| Param | Type | Description |
|:--|:--|:--|
| `$Fields` | `array` |  |

**回傳**

`bool`



# 40. JWTEntity


## 40.1 ToString

```php
public function ToString($PrivateKeyUri)
```

將 JWTEntity 物件轉換為 JWT 字串

| Param | Type | Description |
|:--|:--|:--|
| `$PrivateKeyUri` | `string` | 私鑰檔案路徑 |

**回傳**

`string` JWT 字串



## 40.2 GetJTI

```php
public function GetJTI()
```

Get the value of JTI



## 40.3 SetJTI

```php
public function SetJTI($JTI)
```

Set the value of JTI

**回傳**

self



## 40.4 GetSUB

```php
public function GetSUB()
```

Get the value of SUB



## 40.5 SetSUB

```php
public function SetSUB($SUB)
```

Set the value of SUB

**回傳**

self



## 40.6 GetISS

```php
public function GetISS()
```

Get the value of ISS



## 40.7 SetISS

```php
public function SetISS($ISS)
```

Set the value of ISS

**回傳**

self



## 40.8 GetAUD

```php
public function GetAUD()
```

Get the value of AUD



## 40.9 SetAUD

```php
public function SetAUD($AUD)
```

Set the value of AUD

**回傳**

self



## 40.10 GetEXP

```php
public function GetEXP()
```

Get the value of EXP



## 40.11 SetEXP

```php
public function SetEXP($EXP)
```

Set the value of EXP

**回傳**

self



## 40.12 GetIAT

```php
public function GetIAT()
```

Get the value of IAT



## 40.13 SetIAT

```php
public function SetIAT($IAT)
```

Set the value of IAT

**回傳**

self



## 40.14 GetNBF

```php
public function GetNBF()
```

Get the value of NBF



## 40.15 SetNBF

```php
public function SetNBF($NBF)
```

Set the value of NBF

**回傳**

self



## 40.16 GetScopes

```php
public function GetScopes()
```

Get the value of Scopes



## 40.17 SetScopes

```php
public function SetScopes($Scopes)
```

Set the value of Scopes

**回傳**

self



# 41. MailEntity


## 41.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$From` | `string` | 寄件者 |
| `$FromName` | `string` | 寄件者名稱 |
| `$To` | `array` | 收件者郵件位址的數值陣列 |
| `$ToName` | `array` | 收件者名稱的數值陣列 |
| `$Bcc` | `string` | 密件副本 |
| `$BccName` | `string` | 密件副本名稱 |
| `$Subject` | `string` | 主旨 |
| `$Detail` | `string` | 內容 |
| `$FileDIR` | `string` | 附件 |


## 41.2 __construct

```php
public function __construct($From, $FromName, $To, $ToName, $Bcc, $BccName, $Subject, $Detail, $FileDIR)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$From` | `string` | 寄件者 |
| `$FromName` | `string` | 寄件者名稱 |
| `$To` | `string` | 收件者 |
| `$ToName` | `string` | 收件者名稱 |
| `$Bcc` | `string` | 密件副本 |
| `$BccName` | `string` | 密件副本名稱 |
| `$Subject` | `string` | 主旨 |
| `$Detail` | `string` | 內容 |



## 41.3 FromArray(static)

```php
static public function FromArray($Array)
```

從陣列建立實體

**回傳**

MailEntity



## 41.4 ToArray

```php
public function ToArray()
```

輸出為陣列

**回傳**

`array`



# 42. SiteSettingsEntity


## 42.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$SiteName` | `string` | 網站名稱 |
| `$LogoImageUrl` | `string[]` | 網站 Logo 圖片網址 |
| `$ServiceTel1` | `string` | 服務電話 1 |
| `$ServiceTel2` | `string` | 服務電話 2 |
| `$ServiceFax1` | `string` | 服務傳真 1 |
| `$ServiceAddress` | `string` | 服務地址 |
| `$ServiceEmail` | `string` | 服務電子郵件 |
| `$ServiceHours` | `string` | 服務時間說明 |
| `$OwnerName` | `string` | 網站擁有者名稱，將顯示於頁尾的版權聲明 |
| `$LinkLine` | `string` | LINE 官方帳號連結 |
| `$LinkFacebook` | `string` | Facebook 粉絲專頁連結 |
| `$LinkYouTube` | `string` | YouTube 頻道連結 |
| `$LinkLinkedIn` | `string` | LinkedIn 個人頁面連結 |
| `$LinkInstagram` | `string` | Instagram 個人頁面連結 |
| `$LinkTwitter` | `string` | Twitter 個人頁面連結 |


## 42.2 __construct

```php
public function __construct($SiteName = '', $LogoImageUrl = [], $ServiceTel1 = '', $ServiceTel2 = '', $ServiceFax1 = '', $ServiceAddress = '', $ServiceEmail = '', $ServiceHours = '', $OwnerName = '', $LinkLine = '', $LinkFacebook = '', $LinkYouTube = '', $LinkLinkedIn = '', $LinkInstagram = '', $LinkTwitter = '')
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$SiteName` | `string` | 網站名稱 |
| `$LogoImageUrl` | `string[]` | 網站 Logo 圖片網址 |
| `$ServiceTel1` | `string` | 服務電話 1 |
| `$ServiceTel2` | `string` | 服務電話 2 |
| `$ServiceFax1` | `string` | 服務傳真 1 |
| `$ServiceAddress` | `string` | 服務地址 |
| `$ServiceEmail` | `string` | 服務電子郵件 |
| `$ServiceHours` | `string` | 服務時間說明 |
| `$OwnerName` | `string` | 網站擁有者名稱，將顯示於頁尾的版權聲明 |
| `$LinkLine` | `string` | LINE 官方帳號連結 |
| `$LinkFacebook` | `string` | Facebook 粉絲專頁連結 |
| `$LinkYouTube` | `string` | YouTube 頻道連結 |
| `$LinkLinkedIn` | `string` | LinkedIn 個人頁面連結 |
| `$LinkInstagram` | `string` | Instagram 個人頁面連結 |
| `$LinkTwitter` | `string` | Twitter 個人頁面連結 |



## 42.3 FromArray(static)

```php
static public function FromArray($Array)
```

從關聯陣列建立 SiteSettingsEntity，可用的鍵如下 (首字母大小寫皆相容): `SiteName`, `LogoImageUrl`, `ServiceTel1`, `ServiceTel2`, `ServiceFax1`, `ServiceAddress`, `ServiceEmail`, `ServiceHours`, `OwnerName`, `LinkLine`, `LinkFacebook`, `LinkYouTube`, `LinkLinkedIn`, `LinkInstagram`, `LinkTwitter`

| Param | Type | Description |
|:--|:--|:--|
| `$Array` | `array` | 關聯陣列 |

**回傳**

SiteSettingsEntity



## 42.4 ToArray

```php
public function ToArray($Capitalize = false)
```

將 SiteSettingsEntity 轉換為關聯陣列

| Param | Type | Description |
|:--|:--|:--|
| `$Capitalize` | `bool` | 是否將鍵名首字母大寫 |

**回傳**

`array`



# 43. SMSEntity


## 43.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$To` | `string` | 收件者手機號碼的數值陣列 |
| `$Detail` | `string` | 簡訊內容 |


## 43.2 __construct

```php
public function __construct($To, $Detail = '') {
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$To` | `string` |  |
| `$Detail` | `string` |  |



## 43.3 FromArray(static)

```php
static public function FromArray($Array) {
```

從數值陣列建立 SMSEntity 實例

| Param | Type | Description |
|:--|:--|:--|
| `$Array` | `array` |  |

**回傳**

SMSEntity



## 43.4 ToArray

```php
public function ToArray() {
```

輸出為關聯陣列

**回傳**

`array`



# 44. Spreadsheet


## 44.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Path` | `string` | 檔案絕對路徑 |
| `$Extension` | `string` | 檔案副檔名 |


## 44.2 __construct

```php
public function __construct($Path)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Path` | `string` | 檔案絕對路徑 |



## 44.3 Move

```php
public function Move($DestinationDIR)
```

移動本物件的檔案到指定的資料夾：在指定資料夾下建立當下日期的資料夾，然後移動並重新命名檔案到該資料夾  
```php  
$SheetFile = '/var/www/misa_manage/site/private-data/tmp/20220725/0rgsxfrxqoy01pxz.xlsx';  
$Sheet = new Spreadsheet($SheetFile);  
$Sheet->Move('/var/www/misa_manage/site/private-data/file');  
echo $Sheet->Path;  
// /var/www/misa_manage/site/private-data/file/20220930/0sihndso1vyd6gyw.xlsx  
```

| Param | Type | Description |
|:--|:--|:--|
| `$DestinationDIR` | `string` |  |

**回傳**

`true`



## 44.4 GetFileInfo

```php
public function GetFileInfo($CreatorID, $CreatorName)
```

回傳以 File 資料表欄位名稱為鍵的關聯陣列，包括 Title, FileName, StoreDIRPath, FileSize, ContentTYP, CreatorID, CreatorName 等  
其中，Title 與 FileName 內容相同，為檔案名稱(含副檔名)

| Param | Type | Description |
|:--|:--|:--|
| `$CreatorID` | `string` |  |
| `$CreatorName` | `string` |  |

**回傳**

`array` 以 File 資料表欄位名稱為鍵的關聯陣列，包括 Title, FileName, StoreDIRPath, FileSize, ContentTYP, CreatorID, CreatorName 等



# 45. UploadFileInfo extends \SplFileInfo


## 45.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Error` | `\Exception` | 執行中的錯誤 |
| `$UploadFilename` | `string` | **(protected)** 檔案上傳時的原始檔案名稱 |
| `$UploadType` | `string` | **(protected)** 檔案上傳時的原始檔案類型 (MIME) |
| `$UploadExtension` | `string` | **(protected)** 檔案上傳時的原始副檔名 (不包含 `.`) |


## 45.2 FromPost(static)

```php
static public function FromPost($Keys, $Index = null)
```

從 $_FILES 中取得檔案資訊，建構 UploadFileInfo 實例  
```php  
//當用戶以 POST 方式上傳填入 input[name=_UploadFiles[0][_FileBinary]][type=file][multiple] 的 "uploading_file.zip"，  
//伺服器端可用下的方式取得上傳的檔案資訊  
$File = UploadFileInfo::FromPost(['_UploadFiles', '0', '_FileBinary'], 0);  
echo $File->getUploadFilename(); // uploading_file.zip  
echo $File->getUploadType(); // application/zip  
echo $File->getUploadExtension(); // zip  
```

| Param | Type | Description |
|:--|:--|:--|
| `$Keys` | `array` | `$_FILES` 中的每一層鍵的數值陣列 (除了 `$_FILES` 固有的鍵以外) |
| `$Index` | `int` | `$_FILES` 最後一層的檔案索引，當 HTML 表單中的 `input[type=file]` 容許多個檔案時使用 |

**回傳**

UploadFileInfo



## 45.3 getUploadFilename

```php
public function getUploadFilename()
```

取得檔案上傳時的原始檔案名稱

**回傳**

`string`



## 45.4 setUploadFilename

```php
public function setUploadFilename($Filename)
```

設定檔案上傳時的原始檔案名稱

| Param | Type | Description |
|:--|:--|:--|
| `$Filename` | `string` |  |



## 45.5 getUploadType

```php
public function getUploadType()
```

取得檔案上傳時的原始檔案類型 (MIME)

**回傳**

`string`|`false`



## 45.6 setUploadType

```php
public function setUploadType($Type)
```

設定檔案上傳時的原始檔案類型 (MIME)

| Param | Type | Description |
|:--|:--|:--|
| `$Type` | `string` |  |



## 45.7 getUploadExtension

```php
public function getUploadExtension()
```

取得檔案上傳時的原始副檔名 (不包含 `.`)

**回傳**

`string`|`false`



## 45.8 setUploadExtension

```php
public function setUploadExtension($Extension)
```

設定檔案上傳時的原始副檔名

| Param | Type | Description |
|:--|:--|:--|
| `$Extension` | `string` |  |



## 45.9 rename

```php
public function rename($RootDIR, $Name = '', $DIR = '')
```

重新命名檔案並移動到 `$RootDIR/$DIR` 資料夾，並回傳新的檔案資訊物件 (\SplFileInfo)

**回傳**

\SplFileInfo



## 45.10 remove

```php
public function remove()
```

移除檔案



# 46. Crypt {


## 46.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$PassPhrase` | `string` | **(protected)** 加密/解密時使用的密碼片語 |
| `$CipherMethod` | `string` | **(protected)** 加密/解密時使用的演算法名稱，預設為 AES-128-ECB<br>可用的演算法名稱請參考：http://php.net/manual/en/function.openssl-get-cipher-methods.php |
| `$Key` | `string` | **(protected)** 雜湊後的密碼片語 |
| `$KeyBits` | `int` | **(protected)** 密碼片語雜湊的長度 |


## 46.2 __construct

```php
public function __construct($PassPhrase = '', $KeyBits = 128) {
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$PassPhrase` | `string` | 密碼片語，預設為空字串 |
| `$KeyBits` | `int` | 密碼片語雜湊的長度，預設為 128 |



## 46.3 Encrypt

```php
public function Encrypt($Content) {
```

加密

| Param | Type | Description |
|:--|:--|:--|
| `$Content` | `mixed` | 要加密的內容 |

**回傳**

`string`



## 46.4 Decrypt

```php
public function Decrypt($Content) {
```

解密

| Param | Type | Description |
|:--|:--|:--|
| `$Content` | `mixed` | 要解密的內容 |

**回傳**

`string`|`false`



## 46.5 SetCipherMethod

```php
public function SetCipherMethod($CipherMethod) {
```

設定加密演算法名稱

| Param | Type | Description |
|:--|:--|:--|
| `$CipherMethod` | `string` | 加密演算法名稱 |



## 46.6 GetCipherMethod

```php
public function GetCipherMethod() {
```

取得加密演算法名稱

**回傳**

`string`



## 46.7 SetPassPhrase

```php
public function SetPassPhrase($PassPhrase) {
```

設定密碼片語

| Param | Type | Description |
|:--|:--|:--|
| `$PassPhrase` | `string` | 密碼片語 |



## 46.8 GetPassPhrase

```php
public function GetPassPhrase() {
```

取得密碼片語

**回傳**

`string`



# 47. DBSAction


## 47.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | 資料庫連線物件 PDO |
| `$DBS` | `string` | 資料庫名稱 |
| `$DBSTable` | `string` | 資料表名稱 |
| `$Fields` | `array` | 查詢的資料表欄位名稱 |
| `$FieldValuePairs` | `array` | 待寫入的資料關聯陣列，鍵為資料表欄位名稱，值為欄位值，如 `['SERNO' => '123']` |
| `$ValueParams` | `array` | **(protected)** 在 `$FieldValuePairs` 陣列的值的變數與值的關聯陣列 |
| `$RowCount` | `int` | 上次執行的 SQL 語法影響的列數 |
| `$OrderBys` | `array` | 查詢資料的排序依據的數值陣列，如 `['CreateDateTime desc']` |
| `$ConjWhere` | `array` | 以 and 連接的查詢條件 (WHERE) 字串，如 `["(SERNO = '123')"]` |
| `$DisjWhere` | `array` | 以 or 連接的查詢條件 (WHERE) 字串，如 `["(SERNO = '123')"]` |
| `$WhereParams` | `array` | **(protected)** 條件式 (`$ConjWhere`, `$DisjWhere`) 的參數陣列，如 `['PMOID' => '123']` |
| `$JoinOns` | `array` | 連接其他資料表的查詢條件 (JOIN) 字串，如 `["join UserAUT on UserAUT.UserID = User.UserID"]` |
| `$GroupBys` | `array` | 資料分組的依據欄位名稱，如 `['SERNO']` |
| `$ConjHaving` | `array` | 以 and 連接的資料分組篩選條件 (HAVING) 字串，如 `["(sum(TotalPrice) > '1000')"]` |
| `$DisjHaving` | `array` | 以 or 連接的資料分組篩選條件 (HAVING) 字串，如 `["(sum(TotalPrice) > '1000')"]` |
| `$LimitString` | `string` | 資料查詢的筆數限制及偏移量，如 `limit 10, 0` |
| `$CommandString` | `string` | **(protected)** 自定義的 SQL 指令，當 `RenderSQL('_COMMAND')` 時，會優先使用此指令 |
| `$Error` | `\Exception` | 紀錄物件方法執行中拋出的錯誤 |
| `$ErrorInfo` | `string` | 紀錄物件方法執行中拋出的錯誤訊息 |
| `$State` | `string` | **(protected)** 組合 SQL 指令的模式，如 _SELECT, _INSERT, _UPDATE, _DELETE, _COMMAND |
| `$SQLString` | `string` | 組合後的 SQL 指令 |
| `$SQLStatement` | `\PDOStatement` | SQLStatement |


## 47.2 __construct

```php
public function __construct($DBSLink, $DBS, $DBSTable)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$DBSLink` | `\PDO` | 資料庫連線物件 PDO |
| `$DBS` | `string` | 資料庫名稱 |
| `$DBSTable` | `string` | 資料表名稱 |



## 47.3 AddSelect

```php
public function AddSelect($SelectField)
```

新增 SELECT 欄位  
當參數為關聯陣列 `[$Key => $Val]` 時，會將 `$Val` 視為欄位名稱，`$Key` 視為欄位別名  
```php  
$DBSAction->AddSelect('UserID');  
$DBSAction->AddSelect(['SERNO','FullName']);  
```

| Param | Type | Description |
|:--|:--|:--|
| `$SelectField` | `string|array` | string: 欄位名稱; array: 欄位名稱的陣列 |

**回傳**

`array`|`false` 回傳物件目前的查詢欄位數值陣列



## 47.4 AddPreSelect

```php
public function AddPreSelect($SelectField, $Parameters = [])
```

新增 SELECT 欄位 (包含變數)  
當參數為關聯陣列 `[$Key => $Val]` 時，會將 `$Val` 視為欄位名稱，`$Key` 視為欄位別名  
```php  
$DBSAction->AddPreSelect(':id', ['id' => 'UserID']);  
$DBSAction->AddPreSelect(['SERNO',':name'], ['name' => 'FullName']);  
```

| Param | Type | Description |
|:--|:--|:--|
| `$SelectField` | `string|array` | string: 欄位名稱; array: 欄位名稱的陣列 |
| `$Parameters` | `array` | 變數與值的映射 |

**回傳**

`array`|`false` 回傳物件目前的查詢欄位數值陣列



## 47.5 AddUpdate

```php
public function AddUpdate($UpdateField, $UpdateValue = '', $Quote = true)
```

新增 UPDATE 的欄位與值  
```php  
$DBSAction->AddUpdate('LoginName', 'EPY001');  
$DBSAction->AddUpdate(['SERNO' => 'EPY001', 'FullName' => 'John Doe']);  
$DBSAction->AddUpdate('ModifyCNT', 'ModifyCNT + 1', false);  
```

| Param | Type | Description |
|:--|:--|:--|
| `$UpdateField` | `string|array` | string: 欄位名稱; array: [欄位名稱 => 值] |
| `$UpdateValue` | `string` | 非必填，欄位的值，預設為空字串；若 $UpdateField 為 array 則此參數無效 |
| `$Quote` | `bool` | 非必填，值是否加上引號，預設為 true |

**回傳**

`array`|`false` 回傳欄位與值的關聯陣列



## 47.6 AddPreUpdate

```php
public function AddPreUpdate($UpdateField, $UpdateValue = '', $Parameters = [])
```

新增 UPDATE 的欄位與值 (包含變數)  
```php  
$DBSAction->AddPreUpdate('FullName', ':name', ['name' => 'John Doe']);  
$DBSAction->AddPreUpdate(['SERNO' => ':no', 'FullName' => ':name'], ['no' => 'EPY001', 'name' => 'John Doe']);  
```

| Param | Type | Description |
|:--|:--|:--|
| `$UpdateField` | `string|array` | string: 欄位名稱; array: [欄位名稱 => 值] |
| `$UpdateValue` | `string|array` | 非必填，欄位的值，預設為空字串；若 $UpdateField 與此參數皆為陣列，且 $Parameters 為空陣列時，此參數則為變數與值的映射 |
| `$Parameters` | `array` | 非必填，變數與值的映射 |

**回傳**

`array`|`false` 回傳欄位與值的關聯陣列



## 47.7 AddInsert

```php
public function AddInsert($InsertField, $InsertValue = '')
```

新增 INSERT 的欄位與值  
```php  
$DBSAction->AddInsert('LoginName', 'EPY001');  
$DBSAction->AddInsert(['SERNO' => 'EPY001', 'FullName' => 'John Doe']);  
```

| Param | Type | Description |
|:--|:--|:--|
| `$InsertField` | `string|array` | string: 欄位名稱; array: [欄位名稱 => 值] |
| `$InsertValue` | `string` | 非必填，欄位的值，預設為空字串；當 $InsertField 為 array 時，此參數無效 |

**回傳**

`array`|`false` 回傳欄位名稱與值的關聯陣列



## 47.8 AddPreInsert

```php
public function AddPreInsert($InsertField, $InsertValue = '', $Parameters = [])
```

新增 INSERT 的欄位與值 (包含變數)  
```php  
$DBSAction->AddPreInsert('FullName', ':name', ['name' => 'John Doe']);  
$DBSAction->AddPreInsert(['SERNO' => ':no', 'FullName' => ':name'], ['no' => 'EPY001', 'name' => 'John Doe']);  
```

| Param | Type | Description |
|:--|:--|:--|
| `$InsertField` | `string|array` | string: 欄位名稱; array: [欄位名稱 => 值] |
| `$InsertValue` | `string|array` | 非必填，欄位的值，預設為空字串；當 $InsertField 與此參數皆為陣列，且 $Parameters 為空陣列時，此參數則為變數與值的映射 |
| `$Parameters` | `array` | 非必填，變數與值的映射 |

**回傳**

`array`|`false` 回傳欄位名稱與值的關聯陣列



## 47.9 AddCommand

```php
public function AddCommand($CommandString)
```

直接寫入 SQL 指令

| Param | Type | Description |
|:--|:--|:--|
| `$CommandString` | `string` |  |



## 47.10 AddOrder

```php
public function AddOrder($OrderString, $Sort = "asc")
```

新增排序依據 (ORDER BY)

| Param | Type | Description |
|:--|:--|:--|
| `$OrderString` | `string` | 排序依據欄位 |
| `$Sort` | `string` | 排序方式 ASC|DESC，預設為 ASC |

**回傳**

`array`|`false` 回傳物件排序依據的陣列



## 47.11 AddCondition

```php
public function AddCondition($Condition, $LogicOperator = "")
```

新增查詢條件 (WHERE)

| Param | Type | Description |
|:--|:--|:--|
| `$Condition` | `string` | 條件式 |
| `$LogicOperator` | `string` | 邏輯運算子 AND|OR，預設為 AND，空字串也被視為 AND |

**回傳**

`bool`



## 47.12 AddPreCondition

```php
public function AddPreCondition($Condition, $Parameters = [], $LogicOperator = "")
```

新增包含變數的查詢條件 (WHERE)

| Param | Type | Description |
|:--|:--|:--|
| `$Condition` | `string` | 條件式，包含變數如 `UserID = :ID` |
| `$Parameters` | `array` | 變數與值的關聯陣列，如 ['ID' => '123'] |
| `$LogicOperator` | `string` | 邏輯運算子 AND|OR，預設為 AND，空字串也被視為 AND |

**回傳**

`bool`



## 47.13 AddJoinOn

```php
public function AddJoinOn($JoinTable, $OnCondition)
```

新增連接查詢條件 (JOIN ON)

| Param | Type | Description |
|:--|:--|:--|
| `$JoinTable` | `string` | 連接的資料表名稱 |
| `$OnCondition` | `string` | 連接條件式 |

**回傳**

`array`|`false` 回傳物件連接查詢條件的陣列



## 47.14 AddGroupBy

```php
public function AddGroupBy($GroupByField)
```

新增資料分組查詢條件 (GROUP BY)

| Param | Type | Description |
|:--|:--|:--|
| `$GroupByField` | `string` | 欄位名稱 |

**回傳**

`array`|`false` 回傳物件的 GROUP BY 陣列



## 47.15 AddHaving

```php
public function AddHaving($Having, $LogicOperator = "")
```

新增資料分組的篩選條件 (HAVING)

| Param | Type | Description |
|:--|:--|:--|
| `$Having` | `string` |  |
| `$LogicOperator` | `string` |  |

**回傳**

`array`|`false`



## 47.16 AddLimit

```php
public function AddLimit($StartRecord = 0, $Records = 0)
```

新增查詢筆數限制及偏移量 (LIMIT, OFFSET)

| Param | Type | Description |
|:--|:--|:--|
| `$StartRecord` | `int` |  |
| `$Records` | `int` |  |

**回傳**

`bool`



## 47.17 ClearSQL

```php
public function ClearSQL()
```

清空查詢條件、SQL語句、錯誤訊息



## 47.18 MergeCondition(protected)

```php
protected function MergeCondition()
```

合併物件的 ConjWhere, DisjWhere 屬性為 `where...` 字串

**回傳**

`string`



## 47.19 MergeHaving(protected)

```php
protected function MergeHaving()
```

合併物件的 ConjHaving, DisjHaving 屬性為 `having...` 字串

**回傳**

`string`



## 47.20 RenderSQL

```php
public function RenderSQL($State)
```

組合 SQL 語句

| Param | Type | Description |
|:--|:--|:--|
| `$State` | `string` | _SELECT|_INSERT|_UPDATE|_DELETE|_SUBQUERY |

**回傳**

`string`|`false` 回傳 SQL 語句



## 47.21 ExecuteCommand

```php
public function ExecuteCommand($SQLString, $CharSet = '')
```

執行 SQL 指令 (不參考物件的屬性，直接執行參數的 SQL 指令)  
                 SQL 指令不是 SELECT/SHOW 時，回傳成功與否的布林值

| Param | Type | Description |
|:--|:--|:--|
| `$SQLString` | `string` | SQL 指令 |
| `$CharSet` | `string` | 字元編碼，預設為空字串，也可指定為 UTF8|LATIN1 |

**回傳**

mixed SQL 指令為 SELECT/SHOW 時，回傳查詢結果的陣列 (\PDOStatement::fetchAll)，若無查詢結果，回傳 `false`；



## 47.22 ExecuteSQL

```php
public function ExecuteSQL($CharSet = '')
```

執行 SQL 指令 (參考物件的屬性 $SQLString)

| Param | Type | Description |
|:--|:--|:--|
| `$CharSet` | `string` | 字元編碼，預設為空字串，也可指定為 UTF8|LATIN1 |

**回傳**

mixed 若 SQL 指令為 SELECT/SHOW，則回傳查詢結果的陣列 (\PDOStatement::fetchAll)，否則回傳布林值



## 47.23 Count

```php
public function Count($Debug = false)
```

Count

| Param | Type | Description |
|:--|:--|:--|
| `$Debug` | `bool` | 是否只顯示 SQL 指令的組合結果而不執行，預設為 false |

**回傳**

mixed 若 $Debug 為 `true`，則回傳 SQL 指令的字串；若執行失敗，則回傳 `false`；若執行成功，則回傳符合查詢條件的記錄數



## 47.24 RowCount

```php
public function RowCount()
```

在執行過 ExecuteCommand, ExecuteSQL 之後呼叫此方法，取得 SQL 指令的執行影響列數

**回傳**

`int`|`false` 執行成功回傳影響列數，執行失敗回傳 `false`



## 47.25 ShowDatabases

```php
public function ShowDatabases()
```

取得資料庫名稱的數值陣列

**回傳**

`array` 資料庫名稱的數值陣列



## 47.26 ShowTables

```php
public function ShowTables()
```

取得資料表名稱的數值陣列

**回傳**

`array` 資料表名稱的數值陣列



## 47.27 ShowColumns

```php
public function ShowColumns($DBSTable = null)
```

ShowColumns

| Param | Type | Description |
|:--|:--|:--|
| `$DBSTable` | `string` | 資料表名稱 |

**回傳**

`array` 資料表欄位名稱的數值陣列



## 47.28 ShowPrimaryKey

```php
public function ShowPrimaryKey($DBSTable = null)
```

取得資料表指定欄位的資訊

| Param | Type | Description |
|:--|:--|:--|
| `$DBSTable` | `string` | 資料表名稱 |

**回傳**

`array` 資料表欄位名稱的數值陣列



## 47.29 DBSSearch

```php
public function DBSSearch($R_Search_Array, $SchemaSearch_Array, $NotFlag = false)
```

解析 MISA.UI 用戶端回傳的搜尋條件，並將其轉換成 SQL 指令的條件  
```php  
$SearchArray = [['equal' => ['_Name' => 'John']]];  
$SchemaSearchArray = ['_Name' => 'User.NickName'];  
$DBSAct = new DBSAct($Link, $DBS, 'User');  
$DBSAct->AddSelect('UserID');  
$DBSAct->AddSelect('NickName as _Name');  
$DBSAct->DBSSearch($SearchArray, $SchemaSearchArray);  
$DBSAct->RenderSQL('_SELECT');  
$Users = $DBSAct->ExecuteSQL();  
```

| Param | Type | Description |
|:--|:--|:--|
| `$R_Search_Array` | `array` | 搜尋條件的陣列 |
| `$SchemaSearch_Array` | `array` | 搜尋條件的資料表欄位名稱與 Schema 欄位的映射陣列 |
| `$NotFlag` | `bool` |  |



## 47.30 ThrowError(protected)

```php
protected function ThrowError($Error, $ToThrow = true)
```

紀錄執行中的錯誤

| Param | Type | Description |
|:--|:--|:--|
| `$Error` | `string|\Exception` | 錯誤訊息或例外物件 |
| `$ToThrow` | `bool` | 紀錄結束後是否拋錯 |



# 48. DBSConsistency


## 48.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Map` | `array` | 資料庫相互依存的關聯，在執行 DBSMOD::DBSDelete 時，會參考本陣列的資料，來決定要同步刪除或清除的資料表。 |


# 49. EZReceipt


## 49.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$isTest` | `bool` | **(private)** 是否測試版 |
| `$appName` | `string` | **(private)** 主位址前 |
| `$appKey` | `string` | **(private)** 程式金鑰 |
| `$accName` | `string` | **(private)** 店家帳號 |
| `$accPws` | `string` | **(private)** 店家密碼 |
| `$stID` | `string` | 店家代號 |


## 49.2 __construct

```php
public function __construct($TradeSettings = null)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$TradeSettings` | `ConfigTrade` | 交易設定，將讀取其中的 Receipt 屬性 |



## 49.3 Request(private)

```php
private function Request()
```

取得易發票 API 的令牌

**回傳**

`string` 若通過則回傳令牌



## 49.4 GenEndPoint(private)

```php
private function GenEndPoint($ep)
```

從資源名稱產生完整 API 網址的方法

| Param | Type | Description |
|:--|:--|:--|
| `$ep` | `string` | API 資源名稱 |

**回傳**

`string` 完整 API 網址



## 49.5 PostToEndpoint(private)

```php
private function PostToEndpoint($ep, $param, $token)
```

組成 HTTP 標頭，並呼叫易發票 API

| Param | Type | Description |
|:--|:--|:--|
| `$ep` | `string` | API 網址 |
| `$param` | `string` | 傳送的參數 (JSON 格式) |
| `$token` | `string` | 存取令牌 (以 `EZReceipt::Login()` 取得) |

**回傳**

`string` 易發票的回應 (JSON 格式)



## 49.6 Login

```php
public function Login()
```

使用 `accName`, `accPws`, 以及 `EZReceipt::request()` 取得的令牌，呼叫易發票 API 取得存取令牌

**回傳**

`string` 若通過則回傳存取令牌



## 49.7 InvoiceCreate

```php
public function InvoiceCreate($data, $invB2who = INVOICE_BUYER_B2C)
```

建立新發票  
```php  
$EZReceipt = new EZReceipt($TradeSettings);  
$data = array(  
    "poNo" => $SALODR_Data['SERNO'],  
    "user" => array(  
        "accName" => $User_Data['SERNO'],  
         "email" => $User_Data['EML1'],  
        "name" => $User_Data['FullName'],  
        "phone" => $User_Data['MobileTEL1'],  
        "addr" => ""  
    ),  
    "carrierType" => $R_Data['INVDMTCOMNO'] != "" ? 10 : 1, //1發票存入會員載具，10開立紙本證明(invNID、invTitle才有效)  
    "mobileCode" => "",  
    "delegateCode" => "",  
    "donate" => "",  
    "invNID" => $R_Data['INVDMTCOMNO'],  
    "invTitle" => $R_Data['INVTitle'],  
    "invAddr" => $R_Data['INVStreetADR'],  
    "invReceiver" => $User_Data['FullName'],  
    "invPhone" => $User_Data['MobileTEL1'],  
    "isCustom" => 0,  
    "cdc4" => $this->ReadFlag($SALODR_Data['PayFlag'], 2) == "C" ? $SALODR_Data['CreditCardNO'] : "",  
    "remarks" => "",  
    "prodList" => array()  
);  
$EZReceipt->CreateInvoice($data);  
```

| Param | Type | Description |
|:--|:--|:--|
| `$data` | `array` | 交易資料 |
| `$invB2who` | `int` | 買受人類別；`INVOICE_BUYER_B2C`: 買受人為自然人，`INVOICE_BUYER_B2B`: 買受人為公司 |

**回傳**

`string`



# 50. FileSet


## 50.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Set` | `array` | **(protected)** FileSet 的結果 |
| `$ElementSchema` | `array` | **(protected)** Set 中每個元素的格式標準 Schema<br>遵照 JSON Schema 規範 https://json-schema.org/draft/2020-12/json-schema-core.html |
| `$MaxSize` | `int` | 檔案大小的上限 |
| `$Error` | `\Exception` | 收集類別方法執行中發生的錯誤 |


## 50.2 __construct

```php
public function __construct($Set = [])
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Set` | `array|string` | 數值陣列或數值陣列的序列化字串(serialize, json_encode)，元素須符合 $ElementSchema 的定義 |



## 50.3 ValidateLoop(protected)

```php
protected function ValidateLoop($Element, $Schema)
```

`ValidateElement` 驗證資料時呼叫的遞迴方法

| Param | Type | Description |
|:--|:--|:--|
| `$Element` | `array` | 待驗證的子陣列 |
| `$Schema` | `array` | 子陣列的格式標準 |

**回傳**

`bool` 若通過驗證則回傳 ``true``，反之則回傳 ``false``



## 50.4 ValidateElement

```php
public function ValidateElement($Element)
```

驗證傳入的陣列格式是否符合格式標準 `$ElementSchema`  
```php  
$File = $PDTIFO['FileSet'][0];  
$FileSet = new FileSet();  
echo $FileSet->ValidateElement($File) ? 'pass validation' : 'fail validation';  
```

| Param | Type | Description |
|:--|:--|:--|
| `$Element` | `array` | 待驗證的 $Set 的元素 |

**回傳**

`bool` 若通過驗證則回傳 ``true``，反之則回傳 ``false``



## 50.5 Get

```php
public function Get()
```

取得屬性 $Set

**回傳**

`array` 回傳類別目前的 FileSet 結果



## 50.6 Set

```php
public function Set($Set)
```

寫入屬性 $Set

| Param | Type | Description |
|:--|:--|:--|
| `$Set` | `array|string` | 數值陣列或數值陣列的序列化字串(serialize, json_encode)，元素須符合 $ElementSchema 的定義 |

**回傳**

`bool`



## 50.7 GetElementSchema

```php
public function GetElementSchema()
```

取得屬性 $ElementSchema 元素格式標準

**回傳**

`array` 回傳類別的元素格式標準 (JSON Schema)



## 50.8 Append

```php
public function Append($Src, $Ext, $IsRemote = false, $Title = "", $Alt = "", $FileID = "")
```

在 FileSet 新增元素，若新增的檔案儲存在本機上，則會重新命名並遷移到 `$GLOBALS['MISASiteSetting']['DIRPath']`  
```php  
//新增本機檔案到 FileSet  
$FileSet = new FileSet($PDTIFO['FileSet']);  
$Appended = $FileSet->Append($_FILES['R_UploadFile']['tmp_name'], 'pdf', false, $R_Data['FileTitle'], $R_Data['FileAlt'], '');  
print_r($Appended);  
// Array  
// (  
//     [Directory] => 20211125  
//     [FileID] =>  
//     [Origin] => Array  
//         (  
//             [FileName] => 20211125xjduah3e.pdf  
//             [URL] =>  
//             [Title] => 說明手冊  
//             [Alt] => 若無法取得說明手冊，請來電詢問  
//         )  
// )  
```

| Param | Type | Description |
|:--|:--|:--|
| `$Src` | `string` | 檔案在本機的路徑或遠端連結位址 |
| `$Ext` | `string` | 檔案類型名稱 |
| `$IsRemote` | `bool` | 檔案來源是遠端連結位址(true)或是本機路徑(false) |
| `$Title` | `string` | 檔案標題 |
| `$Alt` | `string` | 檔案替代文字，當介面無法顯示檔案時的替代顯示文字 |
| `$FileID` | `string` | 檔案在 File 資料表的 FileID，當此值不為空值時，將以遠端連結位址的方式處理 |

**回傳**

`array`|`false` 回傳新增的元素



## 50.9 AppendExist

```php
public function AppendExist($Path, $Title = "", $Alt = "", $FileID = "")
```

在 FileSet 新增元素，目標檔案已儲存於本機上，不同於 `FileSet::Append`，此方法不會變更檔案的位置或檔案名稱  
```php  
//新增本機檔案到 FileSet  
$LocalFilePath = '/var/www/project_name/site/data/cht/20220805/20220805xjduah3e.pdf';  
$FileSet = new FileSet($PDTIFO['FileSet']);  
$Appended = $FileSet->AppendExist($LocalFilePath, '說明手冊', '若無法取得說明手冊，請來電詢問', '');  
print_r($Appended);  
// Array  
// (  
//     [Directory] => 20220805  
//     [FileID] =>  
//     [Origin] => Array  
//         (  
//             [FileName] => 20220805xjduah3e.pdf  
//             [URL] =>  
//             [Title] => 說明手冊  
//             [Alt] => 若無法取得說明手冊，請來電詢問  
//         )  
// )  
```

| Param | Type | Description |
|:--|:--|:--|
| `$Path` | `string` | 檔案在本機的路徑 |
| `$Title` | `string` | 檔案標題 |
| `$Alt` | `string` | 檔案替代文字，當介面無法顯示檔案時的替代顯示文字 |
| `$FileID` | `string` | 檔案在 File 資料表的 FileID |

**回傳**

`array`|`false` 回傳新增的元素



## 50.10 Remove

```php
public function Remove($Index, $DeleteFile = true)
```

在 FileSet 移除元素，若移除的檔案儲存在本機上，則一併刪除  
```php  
//從 FileSet 中移除名稱為 '20211125xjduah3e.pdf' 的檔案  
$FileSet = new FileSet($PDTIFO['FileSet']);  
$Set = $FileSet->Get();  
for ($i = 0; $i < count($Set); $i++) {  
  if ($Set[$i]['Origin']['FileName'] == '20211125xjduah3e.pdf') {  
    $Removed = $FileSet->Remove($i);  
    break;  
  }  
}  
print_r($Removed);  
// Array  
// (  
//     [Directory] => 20211125  
//     [FileID] => 0sh5rrx3hjsfrn4d  
//     [Origin] => Array  
//         (  
//             [FileName] => 20211125xjduah3e.pdf  
//             [URL] =>  
//             [Title] => 說明手冊  
//             [Alt] => 若無法取得說明手冊，請來電詢問  
//         )  
// )  
```

| Param | Type | Description |
|:--|:--|:--|
| `$Index` | `int` | 待移除的元素索引 |
| `$DeleteFile` | `bool` | 此值為真時，刪除檔案 |

**回傳**

`array` 回傳刪除的元素



## 50.11 GetURLs

```php
public function GetURLs($Size = 'Origin')
```

將屬性 $Set 轉換為檔案位址字串的陣列

| Param | Type | Description |
|:--|:--|:--|
| `$Size` | `string` |  |

**回傳**

`array` 檔案位址字串的數值陣列



## 50.12 HandleUpload

```php
public function HandleUpload($Src, $Ext, $DestRootDIR)
```

搬移並重新命名檔案到指定的根目錄，回傳包含檔案名稱及所在資料夾路徑的陣列；  
會在根目錄下建立 `yyyymmdd` 的目錄  
```php  
$FileSet = new FileSet();  
$Result = $FileSet->HandleUpload(  
    $_FILES['_UploadFiles']['tmp_name'][$i]['_FileBinary'][0],  
    array_pop(explode('.', $_FILES['_UploadFiles']['name'][$i]['_FileBinary'][0])),  
    $GLOBALS['MISASiteSetting']['DIRPath'],  
);  
print_r($Result);  
// Array  
// (  
//     [FileName] => 20211125xjduah3e.pdf  
//     [Directory] => 20211125  
//     [FullPath] => /var/www/project_name/site/data/cht/20211125/20211125xjduah3e.pdf  
// )  
```

| Param | Type | Description |
|:--|:--|:--|
| `$Src` | `string` | 檔案在本機的絕對路徑 |
| `$Ext` | `string` | 檔案類型名稱 |
| `$DestRootDIR` | `string` | 檔案的目標根目錄絕對路徑 |

**回傳**

`array`|`false` 檔案搬移成功後，回傳包含 FileName



# 51. Notice


## 51.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Method` | `int` | **(protected)** 通知發送的途徑 |
| `$Subject` | `string` | 通知的主旨 |
| `$Detail` | `string` | 通知的主要訊息內容 |
| `$AttachmentPath` | `string` | 通知的附加檔案 |
| `$ServiceMail` | `string` | 信件通知: 寄件人 |
| `$Title` | `string` | 信件通知: 信件標題 |
| `$SMTPConfig` | `ConfigSMTP` | 信件通知: 郵件伺服器的設定物件 |
| `$SMSConfig` | `ConfigSMS` | 手機簡訊通知: 簡訊服務商資訊的設定物件 |
| `$Error` | `\Exception` | Error |


## 51.2 __construct

```php
public function __construct($Method = NOTICE_EMAIL, $Settings)
```

建構子  
發送信件的範例  
```php  
//設定 SMTP 初始化  
$SMTPConfig = new ConfigSMTP(  
  'smtp.gmail.com',  
  'mailtest',  
  '40808532',  
  'service@misa.com.tw',  
  'MISA-NO-REPLY'  
);  
//設定信件服務位址  
$SMTPConfig->SetMailService(  
  'GCE_Send_Email_g1',  
  '45f4f9c8c911bc4705c2bf16e6899ef2',  
  'https://mr.misa.com.tw/misa-mail/api/',  
  true                                       //加入佇列，若為 false 則立即發送  
);  
//通知內容樣板  
$TPLDOC = file_get_contents($FilePath, true);  
//接收通知用戶資訊  
$User = [  
    'EML1' => 'fido@gmail.com',  
    'NickName' => 'Frank'  
];  
$Notice = new Notice(NOTICE_EMAIL, $SMTPConfig);        //建構物件  
$Notice->Subject = "You've logged in on new device";    //設定信件主旨  
$Notice->SetDetailFromDOC($TPLDOC, $User);              //設定信件通知內容  
$R_Mail = $Notice->Send($User['EML1']);                 //發送信件通知  
echo $R_Mail ? 'sent successfully' : 'failed to send';  
```  
發送簡訊的範例  
```php  
//設定簡訊服務商資訊  
$SMSConfig = new ConfigSMS(  
  'admin@dearsoft.com',  
  'adminpassword',  
  'https://msg.mitake.com/b2c/mtk/SmSend'  
);  
//通知內容樣板  
$TPLDOC = file_get_contents($FilePath, true);  
//接收通知用戶資訊  
$User = [  
    'MobileTEL1' => '0987123456',  
    'NickName' => 'Frank'  
];  
$Notice = new Notice(NOTICE_MOBILE, $SMSConfig);        //建構物件  
$Notice->SetDetailFromDOC($TPLDOC, $User);              //設定簡訊通知內容  
$R_SMS = $Notice->Send($User['MobileTEL1']);            //發送簡訊通知  
echo $R_SMS ? 'sent successfully' : 'failed to send';  
```

| Param | Type | Description |
|:--|:--|:--|
| `$Method` | `int` | 發送途徑，可能的值: `NOTICE_EMAIL`, `NOTICE_MOBILE`, `NOTICE_FCM` |
| `$Settings` | `Config` | 發送服務供應者的設定，依照發送途徑而不同 |



## 51.3 ReplaceDOC(protected)

```php
protected function ReplaceDOC($DOC, $ReplaceArray)
```

替換文件範本中的待替換文字；  
待替換的文字在文件中如 `{{ToBeReplaced}}`

| Param | Type | Description |
|:--|:--|:--|
| `$DOC` | `string` | 文件範本 |
| `$ReplaceArray` | `array` | 待替換字串的關聯陣列 |

**回傳**

`string` 回傳替換完畢的文件字串



## 51.4 SetDetailFromDOC

```php
public function SetDetailFromDOC($TPLDOC, $ReplaceArray = array())
```

替換文件範本，並將其設定為通知內容

| Param | Type | Description |
|:--|:--|:--|
| `$TPLDOC` | `string` | 文件範本 |
| `$ReplaceArray` | `array` | 待替換字串的關聯陣列 |

**回傳**

`string` 回傳物件屬性 `$Detail`



## 51.5 SetSubjectFromDOC

```php
public function SetSubjectFromDOC($TPLDOC, $ReplaceArray = array())
```

替換文件範本，並將其設定為通知主旨

| Param | Type | Description |
|:--|:--|:--|
| `$TPLDOC` | `string` | 文件範本 |
| `$ReplaceArray` | `array` | 待替換字串的關聯陣列 |

**回傳**

`string` 回傳物件屬性 `$Subject`



## 51.6 Send

```php
public function Send($Recipient)
```

發送通知

| Param | Type | Description |
|:--|:--|:--|
| `$Recipient` | `string` | 收件人資訊，如電子信箱或手機號碼 |

**回傳**

`bool` 若成功發送即回傳 ``true``，反之則回傳 ``false``



## 51.7 SendEmail(protected)

```php
protected function SendEmail($Email)
```

發送通知信件

| Param | Type | Description |
|:--|:--|:--|
| `$Email` | `string` | 收件人的電子信箱 |

**回傳**

`bool` 若成功發送即回傳 ``true``，反之則回傳 ``false``



## 51.8 SendSMS(protected)

```php
protected function SendSMS($MobileTEL)
```

發送 SMS

| Param | Type | Description |
|:--|:--|:--|
| `$MobileTEL` | `string` | 收件人的手機號碼 |

**回傳**

`bool` 若成功發送即回傳 ``true``，反之則回傳 ``false``



## 51.9 SendMailByProxy

```php
public function SendMailByProxy($Mail)
```

發送信件：加入郵件伺服器的待送郵件佇列

| Param | Type | Description |
|:--|:--|:--|
| `$Mail` | `MailEntity` | 信件物件 |

**回傳**

`array` 回傳信件發送結果



## 51.10 SendMailByService

```php
public function SendMailByService($Mail)
```

[Deprecated] 發送信件：加入郵件伺服器的待送郵件佇列

| Param | Type | Description |
|:--|:--|:--|
| `$Mail` | `MailEntity` | 信件物件 |

**回傳**

`array` 回傳信件發送結果



# 52. PICSet extends FileSet


## 52.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$ElementSchema` | `array` | **(protected)** Set 中每個元素的格式標準 Schema<br>遵照 JSON Schema 規範 https://json-schema.org/draft/2020-12/json-schema-core.html |
| `$MaxWidth` | `array` | **(protected)** 各尺寸圖片的最大長寬 |


## 52.2 Append

```php
public function Append($Src, $Ext, $IsRemote = false, $Title = "", $Alt = "", $FileID = "")
```

加入元素並新增對應的本機檔案

| Param | Type | Description |
|:--|:--|:--|
| `$Src` | `string` | 檔案在本機的路徑或遠端連結位址 |
| `$Ext` | `string` | 檔案類型名稱 |
| `$IsRemote` | `bool` | 檔案來源是遠端連結位址(true)或是本機路徑(false) |
| `$Title` | `string` | 檔案標題 |
| `$Alt` | `string` | 檔案替代文字，當介面無法顯示檔案時的替代顯示文字 |
| `$FileID` | `string` | 檔案在 File 資料表的 FileID |

**回傳**

`array`|`false` 回傳符合 ElementSchema 格式的陣列



## 52.3 AppendExist

```php
public function AppendExist($Path, $Title = "", $Alt = "", $FileID = "")
```

加入元素，目標圖片已儲存於本機上；並檢查不同尺寸的圖片檔案是否已儲存於本機，若本機無對應尺寸的檔案則新建；不同於 `PICSet::Append`，此方法不會變更檔案的位置或檔案名稱

| Param | Type | Description |
|:--|:--|:--|
| `$Path` | `string` | 檔案在本機的路徑 |
| `$Title` | `string` | 檔案標題 |
| `$Alt` | `string` | 檔案替代文字，當介面無法顯示檔案時的替代顯示文字 |
| `$FileID` | `string` | 檔案在 File 資料表的 FileID |

**回傳**

`array`|`false` 回傳新增的元素



## 52.4 CopyResizeImage(protected)

```php
protected function CopyResizeImage($Src, $Dest, $MaxWidth, $MaxHeight, $Quality)
```

複製並壓縮圖片

| Param | Type | Description |
|:--|:--|:--|
| `$Src` | `string` | 原始圖片檔案路徑 |
| `$Dest` | `string` | 目標檔案路徑 |
| `$MaxWidth` | `int` | 圖片最大寬度 |
| `$MaxHeight` | `int` | 圖片最大高度 |
| `$Quality` | `int` | 圖片壓縮品質 |

**回傳**

`bool`



## 52.5 GetMaxWidth

```php
public function GetMaxWidth()
```

取得屬性 MaxWidth



## 52.6 SetMaxWidth

```php
public function SetMaxWidth($MaxWidth)
```

設定屬性 MaxWidth

| Param | Type | Description |
|:--|:--|:--|
| `$MaxWidth` | `mixed` |  |



# 53. RedisAction


## 53.1 Properties

| Prop | Type | Description |
|:--|:--|:--|
| `$Link` | `\Predis\Client` | Redis 資料庫驅動 |
| `$Error` | `\Exception` | 錯誤訊息 |
| `$ErrorInfo` | `string` | 錯誤訊息 (字串型別) |
| `$DBSTable` | `string` | 當前操作的資料表名稱 |


## 53.2 __construct

```php
public function __construct($Link, $DBSTable)
```

建構子

| Param | Type | Description |
|:--|:--|:--|
| `$Link` | `\Predis\Client` | Redis 資料庫驅動 |
| `$DBSTable` | `string` | 資料表名稱 |



## 53.3 FromConnection(static)

```php
static public function FromConnection($DBSTable, $Host, $Password = '', $Port = 6379)
```

從 Redis 連線資訊建立 RedisAction 物件

| Param | Type | Description |
|:--|:--|:--|
| `$DBSTable` | `string` | 資料表名稱 |
| `$Host` | `string` | Redis 伺服器位址 |
| `$Password` | `string` | Redis 伺服器密碼，無密碼時請傳入空字串 |
| `$Port` | `int` | Redis 伺服器埠號，預設為 `6379` |

**回傳**

RedisAction



## 53.4 GetKey(protected)

```php
protected function GetKey($ID)
```

取得資料庫中的鍵

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |

**回傳**

`string`|`false` 資料庫的鍵



## 53.5 SetError(protected)

```php
protected function SetError($Message)
```

設定錯誤訊息

| Param | Type | Description |
|:--|:--|:--|
| `$Message` | `string` | 錯誤訊息 |

**回傳**

RedisAction



## 53.6 Set

```php
public function Set($ID, $Value)
```

寫入資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |
| `$Value` | `mixed` | 資料的值 |

**回傳**

`bool` 是否寫入成功



## 53.7 Get

```php
public function Get($ID)
```

讀取資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |

**回傳**

mixed 資料的值



## 53.8 Delete

```php
public function Delete($ID)
```

刪除資料

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |

**回傳**

`int`



## 53.9 Exists

```php
public function Exists($ID)
```

查詢資料是否存在

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |

**回傳**

`bool` 存在時回傳 ``true``，不存在時回傳 ``false``



## 53.10 Expire

```php
public function Expire($ID, $Seconds = 86400)
```

設定資料的過期時間，舉例來說，如果你希望資料在 1 小時後過期，則可以使用以下的程式碼：  
```php  
$Redis->Expire('data-id', 3600);  
```

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |
| `$Seconds` | `int` | 過期時間，單位為秒，預設為 1 天 |



## 53.11 Ping

```php
public function Ping()
```

測試是否連線成功



## 53.12 GetType

```php
public function GetType($ID)
```

取得資料的類型

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |

**回傳**

`string`|`false`



## 53.13 ListPush

```php
public function ListPush($ID, $Value)
```

新增元素到指定的陣列中，若陣列不存在則會自動建立

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |
| `$Value` | `array|string` | 要新增的元素 |

**回傳**

`int`|`false` 新增的元素數量



## 53.14 ListGet

```php
public function ListGet($ID, $Start, $End = 100)
```

取得陣列中的元素

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |
| `$Start` | `int` | 起始位置 |
| `$End` | `int` | 結束位置，預設為 100 |

**回傳**

`array`|`false` 陣列中的元素



## 53.15 ListRemove

```php
public function ListRemove($ID, $Value)
```

從陣列中刪除指定的元素

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |
| `$Value` | `string` | 要刪除的元素 |

**回傳**

`int`|`false` 刪除的元素數量



## 53.16 SetGet

```php
public function SetGet($ID)
```

取得集合中的所有元素

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |

**回傳**

`array`|`false` 集合中的所有元素



## 53.17 SetAdd

```php
public function SetAdd($ID, $Value)
```

新增元素到集合中

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |
| `$Value` | `array|string` | 要新增的元素 |

**回傳**

`int`|`false` 新增的元素數量



## 53.18 SetRemove

```php
public function SetRemove($ID, $Value)
```

從集合中刪除指定的元素

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |
| `$Value` | `array|string` | 要刪除的元素 |

**回傳**

`int`|`false` 刪除的元素數量



## 53.19 SetExists

```php
public function SetExists($ID, $Value)
```

測試指定的元素是否存在於集合中

| Param | Type | Description |
|:--|:--|:--|
| `$ID` | `string` | 資料的 ID |
| `$Value` | `string` | 要測試的元素 |

**回傳**

`bool` 存在時回傳 ``true``，不存在時回傳 ``false``



# 54. Utility


## 54.1 DebugPrint(static)

```php
static public function DebugPrint($Message = '')
```

偵測當前網域，若為測試環境則輸出訊息

| Param | Type | Description |
|:--|:--|:--|
| `$Message` | `mixed` | 待輸出訊息 |



## 54.2 DebugShow(static)

```php
static public function DebugShow()
```

偵測當前網域是否為測試環境

**回傳**

`bool`



## 54.3 GetDBSID(static)

```php
static public function GetDBSID()
```

產生隨機字串作為資料庫的 UID

**回傳**

`string` 產生的隨機字串



## 54.4 GetDBSSERNO(static)

```php
static public function GetDBSSERNO($Type, $Link, $DBS, $DBSTable, $DBSField, $Prefix = '', $Format = "%05d")
```

產生隨機序號，不與指定的資料表既有資料重複

| Param | Type | Description |
|:--|:--|:--|
| `$Type` | `string` | 序號產生的機制，可能的值為: _STEP|_STEP_IN_TODAY|_TIMESTAMP |
| `$Link` | `\PDO` | 資料庫連線 |
| `$DBS` | `string` | 資料庫名稱 |
| `$DBSTable` | `string` | 資料表名稱 |
| `$DBSField` | `string` | 資料表欄位名稱 |
| `$Prefix` | `string` | 序號前綴，預設為空字串 |
| `$Format` | `string` | 序號格式，預設為 %05d |

**回傳**

`string` 產生的序號



## 54.5 GetRandom36(static)

```php
static public function GetRandom36($Length)
```

產生指定長度的隨機字串 (36進位)

| Param | Type | Description |
|:--|:--|:--|
| `$Length` | `int` | 隨機字串長度 |

**回傳**

`string` 產生的隨機字串



## 54.6 ValidateEmail(static)

```php
static public function ValidateEmail($Email)
```

驗證字串是否為有效的 Email 格式

| Param | Type | Description |
|:--|:--|:--|
| `$Email` | `string` | 待驗證的 Email |

**回傳**

`bool` 是否為有效的 Email 格式



## 54.7 ValidateNationalID(static)

```php
static public function ValidateNationalID($NationalID)
```

驗證字串是否為有效的中華民國身分證字號格式

| Param | Type | Description |
|:--|:--|:--|
| `$NationalID` | `string` | 待驗證的身分證字號 |

**回傳**

`bool` 是否為有效的身分證字號



## 54.8 LinkURL(static)

```php
static public function LinkURL($URL = '', $Message = '', $ReplaceParent = false)
```

輸出轉頁至其他頁面的 HTML 碼，轉頁前彈出提示訊息

| Param | Type | Description |
|:--|:--|:--|
| `$URL` | `string` | 轉頁目標的 URL，若為空則轉頁至上一頁 |
| `$Message` | `string` | 轉頁前彈出的訊息，若為空則不彈出訊息 |
| `$ReplaceParent` | `string` | 轉頁的範圍是否為父視窗 (window.parent)，預設為否 (window) |



## 54.9 LinkURLSwal(static)

```php
static public function LinkURLSwal($URL = '', $Message = '', $ReplaceParent = false)
```

輸出轉頁至其他頁面的 HTML 碼，轉頁前彈出 SweetAlert2 的提示訊息

| Param | Type | Description |
|:--|:--|:--|
| `$URL` | `string` | 轉頁目標的 URL，若為空則轉頁至上一頁 |
| `$Message` | `string` | 轉頁前彈出的訊息，若為空則不彈出訊息 |
| `$ReplaceParent` | `string` | 轉頁的範圍是否為父視窗 (window.parent)，預設為否 |



## 54.10 SafeSQL(static)

```php
static public function SafeSQL($Value, $DBSLink)
```

抵禦 SQL 注入攻擊

| Param | Type | Description |
|:--|:--|:--|
| `$Value` | `mixed` | 待處理的值 |
| `$DBSLink` | `\PDO` | 資料庫連線物件 |

**回傳**

mixed 處理後的值



## 54.11 SafeScript(static)

```php
static public function SafeScript($Value)
```

抵禦 Script 注入攻擊

| Param | Type | Description |
|:--|:--|:--|
| `$Value` | `mixed` |  |

**回傳**

mixed 處理後的值



## 54.12 SafeXSS(static)

```php
static public function SafeXSS($Var)
```

抵禦 Cross-Site Scripting (XSS) 攻擊

| Param | Type | Description |
|:--|:--|:--|
| `$Var` | `array|string` | 要過濾的變數 |

**回傳**

`array`|`string` 過濾後的變數



## 54.13 CheckMethod(static)

```php
static public function CheckMethod($AllowedMethods = [])
```

檢查請求的方法是否在允許的方法清單中

| Param | Type | Description |
|:--|:--|:--|
| `$AllowedMethods` | `array` |  |

**回傳**

`bool`



## 54.14 ReplaceTPL(static)

```php
static public function ReplaceTPL($Template, $ReplacingArray)
```

取代樣板文件中的變數

| Param | Type | Description |
|:--|:--|:--|
| `$Template` | `string` | 樣板文件的內容 |
| `$ReplacingArray` | `array` | 要取代的變數及值的映射陣列 |

**回傳**

`string` 取代後的文件內容



## 54.15 ConvertDBSPICToURI(static)

```php
static public function ConvertDBSPICToURI($PICString)
```

彙整資料庫中的 PICSet/PICQUE 欄位資料為陣列

| Param | Type | Description |
|:--|:--|:--|
| `$PICString` | `string|array` | PICSet/PICQUE 欄位資料 |

**回傳**

`array`|`false` 彙整後的數值陣列，每個元素為一關聯陣列，包含 FileName, Title, Alt, Origin, Medium, Small 等鍵



## 54.16 ConvertDBSFileToURI(static)

```php
static public function ConvertDBSFileToURI($FileString)
```

彙整資料庫中的 FileSet/FileQUE 欄位資料為陣列

| Param | Type | Description |
|:--|:--|:--|
| `$FileString` | `string|array` | FileSet/FileQUE 欄位資料 |

**回傳**

`array`|`false` 彙整後的數值陣列，每個元素為一關聯陣列，包含 FileName, Title, Alt, Origin 等鍵



## 54.17 ConvertDBSPathToURI(static)

```php
static public function ConvertDBSPathToURI($PathString)
```

彙整資料庫中的 PathSet 欄位資料為陣列

| Param | Type | Description |
|:--|:--|:--|
| `$PathString` | `string|array` | PathSet 欄位資料 |

**回傳**

`array`|`false` 彙整後的數值陣列，每個元素為一關聯陣列，包含 FileName, Title, Alt, Origin 等鍵



## 54.18 GetTimeDiff(static)

```php
static public function GetTimeDiff($Unit, $BaseDateTime, $TargetDateTime)
```

計算兩個時間之間的差距

| Param | Type | Description |
|:--|:--|:--|
| `$Unit` | `string` | 計算單位，可選擇的值為：`w|d|h|i|s`，分別代表：週、日、時、分、秒 |
| `$BaseDateTime` | `string` | 計算基準時間字串，如 2017-01-01 00:00:00 |
| `$TargetDateTime` | `string` | 計算目標時間字串，如 2017-01-01 00:00:00 |

**回傳**

`int`|`false` 兩個時間之間的差距，單位為 $Unit 所指定的值



## 54.19 ReadFlag(static)

```php
static public function ReadFlag($Flag, $Index)
```

旗標字串讀取函式，以最右側的字元為 `0` 位

| Param | Type | Description |
|:--|:--|:--|
| `$Flag` | `string` | 待讀取的旗標 |
| `$Index` | `int` | 指定的索引，以字串中最右邊的字元為 `0` 位 |

**回傳**

`string`|`false` 回傳指定索引的旗標字元



## 54.20 WriteFlag(static)

```php
static public function WriteFlag($Flag, $Index, $NewChar = "")
```

旗標字串寫入函式，以最右側的字元為 `0` 位

| Param | Type | Description |
|:--|:--|:--|
| `$Flag` | `string` | 待寫入的旗標 |
| `$Index` | `int` | 指定的索引，以字串中最右邊的字元為 `0` 位 |
| `$NewChar` | `string` | 寫入旗標指定索引的字元 |

**回傳**

`string`|`false` 回傳修改後的旗標字串



## 54.21 FilterSensitiveIFO(static)

```php
static public function FilterSensitiveIFO($Data, $ExcludeFields = array())
```

處理敏感資料的屏蔽

| Param | Type | Description |
|:--|:--|:--|
| `$Data` | `array` | 待處理的資料關聯陣列，鍵為欄位名稱，值為待處理的值 |
| `$ExcludeFields` | `array` | 不屏蔽的欄位名稱陣列 |



## 54.22 ConvertDataTimeToTimestamp(static)

```php
static public function ConvertDataTimeToTimestamp($DateTime)
```

轉換日期字串或數字為時間戳記

| Param | Type | Description |
|:--|:--|:--|
| `$DateTime` | `string|int` | 日期字串或數字 |

**回傳**

`int`|`false` 回傳時間戳記



## 54.23 ConvertTimestampToDataTime(static)

```php
static public function ConvertTimestampToDataTime($Timestamp)
```

轉換時間戳記或日期字串為日期字串

| Param | Type | Description |
|:--|:--|:--|
| `$Timestamp` | `int|string` | 時間戳記 |

**回傳**

`string`|`false` 回傳日期字串



## 54.24 TryDecodeJson(static)

```php
static public function TryDecodeJson($JsonString)
```

TryDecodeJson

| Param | Type | Description |
|:--|:--|:--|
| `$JsonString` | `mixed` | JSON 字串 |

**回傳**

mixed 回傳解碼後的資料，若解碼失敗則回傳引數



## 54.25 TryEncodeJson(static)

```php
static public function TryEncodeJson($Data)
```

TryEncodeJson

| Param | Type | Description |
|:--|:--|:--|
| `$Data` | `mixed` | 資料 |

**回傳**

mixed 回傳編碼後的 JSON 字串，若編碼失敗則回傳引數



## 54.26 GetChineseWeekday(static)

```php
static public function GetChineseWeekday($DateTime)
```

取得中文星期幾

| Param | Type | Description |
|:--|:--|:--|
| `$DateTime` | `string` | 日期字串 |

**回傳**

`string` 回傳中文星期幾



## 54.27 GetEmbedYoutubeURL(static)

```php
static public function GetEmbedYoutubeURL($YoutubeURL)
```

從 Youtube 網址取得影片的嵌入網址

| Param | Type | Description |
|:--|:--|:--|
| `$YoutubeURL` | `string` | Youtube 網址 |

**回傳**

`string` 回傳嵌入網址



## 54.28 ReplaceBlank(static)

```php
static public function ReplaceBlank($String)
```

移除字串中的空白字元，包括全半形空白、換行、Tab

| Param | Type | Description |
|:--|:--|:--|
| `$String` | `string` | 待處理的字串 |

**回傳**

`string` 回傳不包含空白字元的字串



## 54.29 ConvertNumToLetter(static)

```php
static public function ConvertNumToLetter($Num)
```

將數字轉換為英文字母，如 0=>A、1=>B、26=>AA...以此類推

| Param | Type | Description |
|:--|:--|:--|
| `$Num` | `int` | 數字 |

**回傳**

`string` 回傳英文字母



## 54.30 ConvertLetterToNum(static)

```php
static public function ConvertLetterToNum($Letter)
```

將英文字母轉換為數字，如 A=>0、B=>1、AA=>26...以此類推

| Param | Type | Description |
|:--|:--|:--|
| `$Letter` | `string` | 英文字母 |

**回傳**

`int` 回傳數字



## 54.31 ConvertNumToChinese(static)

```php
static public function ConvertNumToChinese($Number, $IsCurrency = false)
```

將數字轉換為中文數字  
[dearsoft-com/php-number2chinese](https://github.com/dearsoft-com/php-number2chinese)

| Param | Type | Description |
|:--|:--|:--|
| `$Number` | `int|string` | 數字 |
| `$IsCurrency` | `bool` | 是否為金額，預設為否 |

**回傳**

`string` 回傳中文數字



## 54.32 ConvertNewLine(static)

```php
static public function ConvertNewLine($String)
```

將參數中的換行符號 `\r\n` `\r` `\n` 轉換成PHP_EOL換行

| Param | Type | Description |
|:--|:--|:--|
| `$String` | `mixed` | 要轉換的字串或字串數值陣列 |

**回傳**

`string`|`array`



## 54.33 ReplaceLinkInText(static)

```php
static public function ReplaceLinkInText($Text)
```

取代字串中的連結為超連結 `<a href="...">...</a>`

| Param | Type | Description |
|:--|:--|:--|
| `$Text` | `string` | 待處理的字串 |

**回傳**

`string` 處理後的字串



## 54.34 GetLanguagePack(static)

```php
static public function GetLanguagePack($LangDIR)
```

根據請求標頭的 Accept-Language 取得語言包映射陣列

| Param | Type | Description |
|:--|:--|:--|
| `$LangDIR` | `string` | 語言包存放的目錄 |

**回傳**

`array` 語言包映射陣列



## 54.35 ParseRawHttpRequest(static)

```php
static public function ParseRawHttpRequest()
```

解析 Request Body



## 54.36 HandleRequestData(static)

```php
static public function HandleRequestData()
```

處理請求的資料，過濾可能形成 SQL/Script Injection 的資料，並將 Request Body 資料寫入到 `$R_Data`|`$R_data`



## 54.37 GetLanguage(static)

```php
static public function GetLanguage($Supported, $Default = 'zh-TW') {
```

處理 HTTP Headers 中的 Accept-Language，並回傳最適合的語言代碼

| Param | Type | Description |
|:--|:--|:--|
| `$Supported` | `array` | 可用的語言代碼 |
| `$Default` | `string` | 預設的語言代碼 |

**回傳**

`string` 最適合的語言代碼

