---
description: "Learn more about: CDaoRecordView Class"
title: "CDaoRecordView Class"
ms.date: "11/04/2016"
f1_keywords: ["CDaoRecordView", "AFXDAO/CDaoRecordView", "AFXDAO/CDaoRecordView::CDaoRecordView", "AFXDAO/CDaoRecordView::IsOnFirstRecord", "AFXDAO/CDaoRecordView::IsOnLastRecord", "AFXDAO/CDaoRecordView::OnGetRecordset", "AFXDAO/CDaoRecordView::OnMove"]
helpviewer_keywords: ["CDaoRecordView [MFC], CDaoRecordView", "CDaoRecordView [MFC], IsOnFirstRecord", "CDaoRecordView [MFC], IsOnLastRecord", "CDaoRecordView [MFC], OnGetRecordset", "CDaoRecordView [MFC], OnMove"]
---
# CDaoRecordView Class

A view that displays database records in controls.

> [!NOTE]
> DAO is supported through Office 2013. DAO 3.6 is the final version, and it's considered obsolete.

## Syntax

```
class AFX_NOVTABLE CDaoRecordView : public CFormView
```

## Members

### Protected Constructors

|Name|Description|
|----------|-----------------|
|[CDaoRecordView::CDaoRecordView](#cdaorecordview)|Constructs a `CDaoRecordView` object.|

### Public Methods

|Name|Description|
|----------|-----------------|
|[CDaoRecordView::IsOnFirstRecord](#isonfirstrecord)|Returns nonzero if the current record is the first record in the associated recordset.|
|[CDaoRecordView::IsOnLastRecord](#isonlastrecord)|Returns nonzero if the current record is the last record in the associated recordset.|
|[CDaoRecordView::OnGetRecordset](#ongetrecordset)|Returns a pointer to an object of a class derived from `CDaoRecordset`. ClassWizard overrides this function for you and creates the recordset if necessary.|
|[CDaoRecordView::OnMove](#onmove)|If the current record has changed, updates it on the data source, then moves to the specified record (next, previous, first, or last).|

## Remarks

The view is a form view directly connected to a `CDaoRecordset` object. The view is created from a dialog template resource and displays the fields of the `CDaoRecordset` object in the dialog template's controls. The `CDaoRecordView` object uses dialog data exchange (DDX) and DAO record field exchange (DFX) to automate the movement of data between the controls on the form and the fields of the recordset. `CDaoRecordView` also supplies a default implementation for moving to the first, next, previous, or last record and an interface for updating the record currently in view.

> [!NOTE]
> The DAO database classes are distinct from the MFC database classes based on Open Database Connectivity (ODBC). All DAO database class names have the "CDao" prefix. You can still access ODBC data sources with the DAO classes; the DAO classes generally offer superior capabilities because they use the Microsoft Jet database engine.

The most common way to create your record view is with the Application Wizard. The Application Wizard creates both the record view class and its associated recordset class as part of your skeleton starter application.

If you simply need a single form, the Application Wizard approach is easier. ClassWizard lets you decide to use a record view later in the development process. If you don't create the record view class with the Application Wizard, you can create it later with ClassWizard. Using ClassWizard to create a record view and a recordset separately and then connect them is the most flexible approach because it gives you more control in naming the recordset class and its .H/.CPP files. This approach also lets you have multiple record views on the same recordset class.

To make it easy for end-users to move from record to record in the record view, the Application Wizard creates menu (and optionally toolbar) resources for moving to the first, next, previous, or last record. If you create a record view class with ClassWizard, you need to create these resources yourself with the menu and bitmap editors.

For information about the default implementation for moving from record to record, see `IsOnFirstRecord` and `IsOnLastRecord` and the article [Using a Record View](../../data/using-a-record-view-mfc-data-access.md), which applies to both `CRecordView` and `CDaoRecordView`.

`CDaoRecordView` keeps track of the user's position in the recordset so that the record view can update the user interface. When the user moves to either end of the recordset, the record view disables user interface objects — such as menu items or toolbar buttons — for moving further in the same direction.

For more information about declaring and using your record view and recordset classes, see "Designing and Creating a Record View" in the article [Record Views](../../data/record-views-mfc-data-access.md). For more information about how record views work and how to use them, see the article [Using a Record View](../../data/using-a-record-view-mfc-data-access.md). All the articles mentioned above apply to both `CRecordView` and `CDaoRecordView`.

## Inheritance Hierarchy

[CObject](../../mfc/reference/cobject-class.md)

[CCmdTarget](../../mfc/reference/ccmdtarget-class.md)

[CWnd](../../mfc/reference/cwnd-class.md)

[CView](../../mfc/reference/cview-class.md)

[CScrollView](../../mfc/reference/cscrollview-class.md)

[CFormView](../../mfc/reference/cformview-class.md)

`CDaoRecordView`

## Requirements

**Header:** `afxdao.h`

## <a name="cdaorecordview"></a> CDaoRecordView::CDaoRecordView

When you create an object of a type derived from `CDaoRecordView`, call either form of the constructor to initialize the view object and identify the dialog resource on which the view is based.

```
explicit CDaoRecordView(LPCTSTR lpszTemplateName);
explicit CDaoRecordView(UINT nIDTemplate);
```

### Parameters

*lpszTemplateName*<br/>
Contains a null-terminated string that is the name of a dialog template resource.

*nIDTemplate*<br/>
Contains the ID number of a dialog template resource.

### Remarks

You can either identify the resource by name (pass a string as the argument to the constructor) or by its ID (pass an unsigned integer as the argument). Using a resource ID is recommended.

> [!NOTE]
> Your derived class must supply its own constructor. In the constructor of your derived class, call the constructor `CDaoRecordView::CDaoRecordView` with the resource name or ID as an argument.

`CDaoRecordView::OnInitialUpdate` calls `CWnd::UpdateData`, which calls `CWnd::DoDataExchange`. This initial call to `DoDataExchange` connects `CDaoRecordView` controls (indirectly) to `CDaoRecordset` field data members created by ClassWizard. These data members cannot be used until after you call the base class `CFormView::OnInitialUpdate` member function.

> [!NOTE]
> If you use ClassWizard, the wizard defines an **`enum`** value `CDaoRecordView::IDD` in the class declaration and uses it in the member initialization list for the constructor.

[!code-cpp[NVC_MFCDatabase#35](../../mfc/codesnippet/cpp/cdaorecordview-class_1.cpp)]

## <a name="isonfirstrecord"></a> CDaoRecordView::IsOnFirstRecord

Call this member function to determine whether the current record is the first record in the recordset object associated with this record view.

```
BOOL IsOnFirstRecord();
```

### Return Value

Nonzero if the current record is the first record in the recordset; otherwise 0.

### Remarks

This function is useful for writing your own implementations of the default command update handlers written by ClassWizard.

If the user moves to the first record, the framework disables any user interface objects (for example, menu items or toolbar buttons) you have for moving to the first or the previous record.

## <a name="isonlastrecord"></a> CDaoRecordView::IsOnLastRecord

Call this member function to determine whether the current record is the last record in the recordset object associated with this record view.

```
BOOL IsOnLastRecord();
```

### Return Value

Nonzero if the current record is the last record in the recordset; otherwise 0.

### Remarks

This function is useful for writing your own implementations of the default command update handlers that ClassWizard writes to support a user interface for moving from record to record.

> [!CAUTION]
> The result of this function is reliable except that the view may not be able to detect the end of the recordset until the user has moved past it. The user might have to move beyond the last record before the record view can tell that it must disable any user interface objects for moving to the next or last record. If the user moves past the last record and then moves back to the last record (or before it), the record view can track the user's position in the recordset and disable user interface objects correctly.

## <a name="ongetrecordset"></a> CDaoRecordView::OnGetRecordset

Returns a pointer to the `CDaoRecordset`-derived object associated with the record view.

```
virtual CDaoRecordset* OnGetRecordset() = 0;
```

### Return Value

A pointer to a `CDaoRecordset`-derived object if the object was successfully created; otherwise a NULL pointer.

### Remarks

You must override this member function to construct or obtain a recordset object and return a pointer to it. If you declare your record view class with ClassWizard, the wizard writes a default override for you. ClassWizard's default implementation returns the recordset pointer stored in the record view if one exists. If not, it constructs a recordset object of the type you specified with ClassWizard and calls its `Open` member function to open the table or run the query, and then returns a pointer to the object.

For more information and examples, see the article [Record Views: Using a Record View](../../data/using-a-record-view-mfc-data-access.md).

## <a name="onmove"></a> CDaoRecordView::OnMove

Call this member function to move to a different record in the recordset and display its fields in the controls of the record view.

```
virtual BOOL OnMove(UINT nIDMoveCommand);
```

### Parameters

*nIDMoveCommand*<br/>
One of the following standard command ID values:

- ID_RECORD_FIRST Move to the first record in the recordset.

- ID_RECORD_LAST Move to the last record in the recordset.

- ID_RECORD_NEXT Move to the next record in the recordset.

- ID_RECORD_PREV Move to the previous record in the recordset.

### Return Value

Nonzero if the move was successful; otherwise 0 if the move request was denied.

### Remarks

The default implementation calls the appropriate Move member function of the `CDaoRecordset` object associated with the record view.

By default, `OnMove` updates the current record on the data source if the user has changed it in the record view.

The Application Wizard creates a menu resource with First Record, Last Record, Next Record, and Previous Record menu items. If you select the Initial Toolbar option, the Application Wizard also creates a toolbar with buttons corresponding to these commands.

If you move past the last record in the recordset, the record view continues to display the last record. If you move backward past the first record, the record view continues to display the first record.

> [!CAUTION]
> Calling `OnMove` throws an exception if the recordset has no records. Call the appropriate user interface update handler function — `OnUpdateRecordFirst`, `OnUpdateRecordLast`, `OnUpdateRecordNext`, or `OnUpdateRecordPrev` — before the corresponding move operation to determine whether the recordset has any records.

## See also

[CFormView Class](../../mfc/reference/cformview-class.md)<br/>
[Hierarchy Chart](../../mfc/hierarchy-chart.md)<br/>
[CDaoRecordset Class](../../mfc/reference/cdaorecordset-class.md)<br/>
[CDaoTableDef Class](../../mfc/reference/cdaotabledef-class.md)<br/>
[CDaoQueryDef Class](../../mfc/reference/cdaoquerydef-class.md)<br/>
[CDaoDatabase Class](../../mfc/reference/cdaodatabase-class.md)<br/>
[CDaoWorkspace Class](../../mfc/reference/cdaoworkspace-class.md)<br/>
[CFormView Class](../../mfc/reference/cformview-class.md)
