# WH — схемы

> **Что здесь:** определения типов запросов/ответов сервиса WH. Ручки, ссылающиеся на них — `endpoints/WH.md`.
> **Источник:** `snapshots/WH.json` · файл генерируется пайплайном — руками не править.

```
type AssetResult { id?: int, name?: str, deleted?: datetime, host?: IdNameDeletedResult<Int32> }
type BarcodeAddData { barcodeTypeID?: int, value: str }
type BarcodeTypes.ListResult { name?: str /* Имя типа штрихкода */ }
type BarcodeUpdateData { id?: int, barcodeTypeID?: int, value: str }
type CountryResult { id?: int, name?: str, twoSymbolCode?: str /* Двухбуквенный код страны */ }
type CurrencyResult { id?: int /* Идентификатор валюты */, shortName?: str /* Краткое наименование валюты */, asciiCode?: str /* Ascii код валюты */ }
type DocumentStatuses.ListResult { name?: str /* Имя статуса складского документа */, code?: str /* Код складского документа */ }
type DocumentTypes.ListResult { name?: str /* Имя типа складского документа */, code?: str /* Код типа складского документа */ }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type FromBodyUploadData { uid?: uuid, contentStream?: file, md5Hash?: str, contentLength?: int, file: str, fileName: str, contentType: str, roles?: int[], coordinate?: str, description?: str, isPublic?: bool, isIgnorePossibleDuplication?: bool, checkSum?: str }
type FromFormUploadData { uid?: uuid, contentStream?: file, md5Hash?: str, contentLength?: int, description?: str, isPublic?: bool, isIgnorePossibleDuplication?: bool, roles?: int[], coordinate?: str, file: file, fileName?: str, contentType?: str }
type GetResult { id?: int, name?: str, erpID?: str /* Идентификатор склада в сторонней системе */, isDefault?: bool /* Признак склада по умолчанию */, location?: LocationResult, description?: str /* Описание склада */, deleted?: datetime /* Дата удаления склада */, deletedBy?: int /* Член тенанта, который удалил склад */ }
type IdCodeNameResult<Byte> { id?: int, code?: str, name?: str }
type IdNameDeletedResult<Int32> { id?: int, name?: str, deleted?: datetime }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type IdNameResult<Int32> { id?: int, name?: str }
type Inventories.ListResult { id?: int /* Идентификатор инвентаризации */, dateFrom?: datetime /* Дата начала инвентаризации */, dateTill?: datetime /* Дата окончания инвентаризации */ }
type Inventories.PostResult { id?: int /* Идентификатор инвентаризации */, dateFrom?: datetime /* Дата начала инвентаризации */, dateTill?: datetime /* Дата окончания инвентаризации */ }
type Inventory.AddData { inventoryDateFrom: datetime, materials?: InventoryMaterialData[] }
type Inventory.UpdateData { inventoryID: int, inventoryDateFrom?: datetime, materials?: InventoryMaterialData[] }
type InventoryMaterialData { materialErpID?: str, materialName?: str, quantity?: float, measurementUnitID?: int, materialCurrencyID?: int, materialCost?: float, warehouseErpID?: str, warehouseName?: str }
type Issue.AddData { warehouseID: int, operationTypeID: int, documentDate?: datetime, number?: str, description?: str, erpID?: str, relatedTaskID?: int, responsiblePersonID?: int }
type Issue.UpdateData { warehouseID: int, operationTypeID: int, documentDate?: datetime, number?: str, description?: str, erpID?: str, relatedTaskID?: int, responsiblePersonID?: int, id?: int }
type IssueItemData { materialID: int, measurementUnitID: int, quantity: float, sortOrder: int }
type IssueItemDeleteData { issueID?: int, items?: int[] }
type IssueItemMergeData { issueID?: int, items?: IssueItemData[] }
type IssueItems.ListResult { issueID?: int /* Идентификатор списания материалов */, material?: MaterialResult, measurementUnit?: IdNameResult<Int16>, quantity?: float /* Количество материала */, sortOrder?: int /* Номер строки */ }
type IssueResult { id?: int, name?: str, warehouseID?: int /* Идентификатор склада */, warehouseName?: str /* Название склада */, documentStatus?: IdCodeNameResult<Byte>, documentDate?: datetime /* Дата документа */, number?: str /* Номер документа */, erpID?: str /* Идентификатор документа во внешней системе */, description?: str /* Описание документа */, deleted?: datetime /* Дата удаления списания материала */, operationType?: IdNameResult<Int16>, created?: datetime /* Дата создания списания материала */, modified?: datetime /* Дата изменения списания материала */, posted?: datetime /* Дата проведения списания материала */, relatedTaskID?: int /* Идентификатор связанной заявки */, taskNumber?: str /* Номер связанной заявки */, responsiblePerson?: IdNameResult<Int32> }
type ListRequiredResult { id?: int /* Идентификатор материала */, name?: str /* Наименование материала */, erpID?: str /* Код материала */, description?: str /* Описание материала */, materialIsMarkable?: bool /* Признак обязательности маркировки */, vendorCode?: str /* Код поставщика */, cost?: float /* Стоимость материала */, currency?: CurrencyResult, warehouse?: WarehouseResult, importQuantity?: float /* Импортированное количество */, actualQuantity?: float /* Акутальное количество */, measurementUnit?: IdNameResult<Int16>, sortOrder?: int /* Индекс сортировки */ }
type ListShortResult { id?: int, name?: str, erpID?: str /* Идентификатор склада в сторонней системе */, isDefault?: bool /* Признак склада по умолчанию */, deleted?: datetime /* Дата удаления склада */ }
type LocationResult { id?: int, address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, description?: str /* Описание локации */, deleted?: datetime /* Дата удаления */, country?: CountryResult }
type LocationShortResult { id?: int, address?: str /* Адрес объекта */, coordinate?: str /* Координаты объекта в формате LAT:LNG */, description?: str /* Описание локации */ }
type Material.AddData { name: str, erpID?: str, vendorCode?: str, description?: str, measurementUnitID?: int, costCurrencyID?: int, cost?: float, purchaseCostCurrencyID?: int, purchaseCost?: float, isMarkable?: bool }
type Material.UpdateData { name: str, erpID?: str, vendorCode?: str, description?: str, measurementUnitID?: int, costCurrencyID?: int, cost?: float, purchaseCostCurrencyID?: int, purchaseCost?: float, isMarkable?: bool, id?: int }
type MaterialActionData<Int16> { data: int[], materialID?: int }
type MaterialAttachmentListResult { fileName?: str /* Название файла (с расширением) */, description?: str /* Описание */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, thumbnailUrl?: str /* Ссылка на эскиз изображения */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, size?: int /* Размер файла в байтах */, created?: datetime /* Дата загрузки UTC */ }
type MaterialAttachmentPostResult { tenantID?: int /* Идентификатор тенанта */, materialID?: int /* Идентификатор материала */, attachmentID?: int /* Идентификатор вложения */ }
type MaterialAttachmentResult { fileName?: str /* Название файла (с расширением) */, description?: str /* Описание */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, thumbnailUrl?: str /* Ссылка на эскиз изображения */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, size?: int /* Размер файла в байтах */, created?: datetime /* Дата загрузки UTC */, attachmentID?: int /* Идентификатор прикрепленного к материалу файла */ }
type MaterialBarcode.AddData { materialID?: int, barcodes?: BarcodeAddData[] }
type MaterialBarcode.UpdateData { materialID?: int, barcodes?: BarcodeUpdateData[] }
type MaterialBarcodes.ListResult { id?: int, barcodeType?: IdNameResult<Byte>, value?: str /* Значение штрихкода */ }
type MaterialBarcodes.PostResult { id?: int, materialID?: int /* Идентификатор материала */ }
type MaterialConsumptionsResult { id?: int /* Идентификатор материала */, name?: str /* Наименование материала */, erpID?: str /* Код материала */, description?: str /* Описание материала */, cost?: float /* Стоимость материала */, totalCost?: float /* Общая стоимость материалов */, currency?: CurrencyResult, warehouse?: WarehouseResult, consumption?: float /* Израсходованное количество */, measurementUnit?: IdNameResult<Int16>, task?: TaskResult, consumed?: datetime /* Дата последнего взятия материала */, consumedBy?: UserResult, sortOrder?: int /* Индекс сортировки */ }
type MaterialInventoryResult { date?: datetime /* дата импорта/инвентаризации */, id?: int /* Идентификатор импорта/инвентаризации */, sort?: int /* Ключ сортировки */, materials?: MaterialConsumptionsResult[] /* Расход материалов */ }
type MaterialListResult { id?: int, name?: str, erpID?: str /* Идентификатор материала во внешней системе */, vendorCode?: str /* Артикул материала */, description?: str /* Описание материала */, isMarkable?: bool /* Признак маркируемости материала */, measurementUnitID?: int /* Единица измерения материала */, cost?: float /* Закупочная стоимость материала */, costCurrencyID?: int /* Валюта закупочной стоимости материала */, purchaseCost?: float /* Стоимость материала для клиента */, purchaseCostCurrencyID?: int /* Валюта стоимости материала для клиента */, deleted?: datetime /* Дата удаления материала */, measurementUnit?: MeasurementUnitResult, costCurrency?: CurrencyResult, purchaseCostCurrency?: CurrencyResult, sortOrder?: int /* Порядок сортировки */ }
type MaterialResult { id?: int, name?: str, erpID?: str /* Идентификатор материала во внешней системе */, vendorCode?: str /* Артикул материала */, description?: str /* Описание материала */, isMarkable?: bool /* Признак маркируемости материала */, measurementUnitID?: int /* Единица измерения материала */, cost?: float /* Закупочная стоимость материала */, costCurrencyID?: int /* Валюта закупочной стоимости материала */, purchaseCost?: float /* Стоимость материала для клиента */, purchaseCostCurrencyID?: int /* Валюта стоимости материала для клиента */, deleted?: datetime /* Дата удаления материала */, measurementUnit?: MeasurementUnitResult, costCurrency?: CurrencyResult, purchaseCostCurrency?: CurrencyResult }
type Materials.ListResult { id?: int /* Идентификатор материала */, name?: str /* Наименование материала */, erpID?: str /* Код материала */, description?: str /* Описание материала */, materialIsMarkable?: bool /* Признак обязательности маркировки */, vendorCode?: str /* Код поставщика */, cost?: float /* Стоимость материала */, currency?: CurrencyResult, warehouse?: WarehouseResult, importQuantity?: float /* Импортированное количество */, actualQuantity?: float /* Акутальное количество */, measurementUnit?: IdNameResult<Int16>, task?: TaskResult, taken?: datetime /* Дата последнего взятия материала */, takenBy?: UserResult, sortOrder?: int /* Индекс сортировки */ }
type MeasurementUnitResult { id?: int /* Идентификатор */, name?: str /* Наименование */, abbreviation?: str /* Аббревиатура */, designation?: str /* Обозначение */ }
type ModifyData { documentTypeID: int, lastNumber?: int, prefix?: str }
type NumberSequenceResult { prefix?: str /* Префикс маски номера документа */, lastNumber?: int /* Последний занятый номер маски номера документа */, documentType?: IdCodeNameResult<Byte> }
type OperationType.AddData { name: str, documentTypeID?: int, erpID?: str }
type OperationType.UpdateData { name: str, documentTypeID?: int, erpID?: str, id?: int }
type OperationTypeAddResult { id?: int /* Идентификатор типа операции */ }
type OperationTypeResult { id?: int /* Идентификатор типа операции */, name?: str /* Наименование типа операции */, erpID?: str /* Код типа операции во внешней системе */, deleted?: datetime /* Метка удаления типа операции */, documentType?: IdCodeNameResult<Byte> }
type Receipt.AddData { warehouseID: int, operationTypeID: int, documentDate?: datetime, number?: str, description?: str, erpID?: str, relatedTaskID?: int, responsiblePersonID?: int }
type Receipt.UpdateData { warehouseID: int, operationTypeID: int, documentDate?: datetime, number?: str, description?: str, erpID?: str, relatedTaskID?: int, responsiblePersonID?: int, id?: int }
type ReceiptItemData { materialID: int, measurementUnitID: int, quantity: float, sortOrder: int }
type ReceiptItemDeleteData { receiptID?: int, items?: int[] }
type ReceiptItemMergeData { receiptID?: int, items?: ReceiptItemData[] }
type ReceiptItems.ListResult { receiptID?: int /* Идентификатор оприходывания материалов */, material?: MaterialResult, measurementUnit?: IdNameResult<Int16>, quantity?: float /* Количество материала */, sortOrder?: int /* Номер строки */ }
type ReceiptResult { id?: int, name?: str, warehouseID?: int /* Идентификатор склада */, warehouseName?: str /* Название склада */, documentStatus?: IdCodeNameResult<Byte>, documentDate?: datetime /* Дата документа */, number?: str /* Номер документа */, erpID?: str /* Идентификатор документа во внешней системе */, description?: str /* Описание документа */, deleted?: datetime /* Дата удаления оприходывания материала */, operationType?: IdNameResult<Int16>, created?: datetime /* Дата создания оприходывания материала */, modified?: datetime /* Дата изменения оприходывания материала */, posted?: datetime /* Дата проведения оприходывания материала */, relatedTaskID?: int /* Идентификатор связанной заявки */, taskNumber?: str /* Номер связанной заявки */, responsiblePerson?: IdNameResult<Int32> }
type TaskResult { id?: int /* Идентификатор */, number?: str /* Наименование заявки */, asset?: AssetResult }
type UploadResult { materialID?: int /* Идентификатор материала */, attachmentID?: int /* Идентификатор вложенного файла */, md5Hash?: str /* Проверочная сумма MD5 */, fileName?: str /* Имя загруженного файла */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */ }
type UserResult { id?: int, firstName?: str, lastName?: str, middleName?: str, avatarUrl?: str, deleted?: datetime }
type UserWarehouseListResult { warehouseID?: int /* Идентификатор склада */, name?: str /* Наименование склада */, erpID?: str /* Код склада */ }
type UserWarehousesData { userID: int, warehouseIDs: int[] }
type Warehouse.AddData { name: str, erpID?: str, description?: str, isDefault?: bool, locationID?: int }
type Warehouse.UpdateData { name: str, erpID?: str, description?: str, isDefault?: bool, locationID?: int, id?: int }
type WarehouseResult { id?: int /* Идентификатор склада */, name?: str /* Наименование склада */, erpID?: str /* Код склада */, location?: LocationShortResult }
type Warehouses.ListResult { id?: int, name?: str, erpID?: str /* Идентификатор склада в сторонней системе */, isDefault?: bool /* Признак склада по умолчанию */, deleted?: datetime /* Дата удаления склада */, description?: str /* Описание склада */, userCount?: int /* Количество пользователей назначенных на склад */, location?: LocationShortResult }
type WarehouseUserListResult { userFullName?: str /* Полное имя пользователя */, userID?: int /* Идентификатор пользователя */ }
type WarehouseUsersData { warehouseID: int, userIDs?: int[], isRelatedToAnyUser?: bool }
type WarehouseUsersDeleteData { warehouseID: int, userIDs?: int[], isRelatedToAnyUser?: bool }
```
