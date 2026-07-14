# SC — схемы

> **Что здесь:** определения типов запросов/ответов сервиса SC. Ручки, ссылающиеся на них — `endpoints/SC.md`.
> **Источник:** `snapshots/SC.json` · файл генерируется пайплайном — руками не править.

```
type ActionData { data: MergeData[], contractID: int }
type AssetResultBase { assetID?: int /* Идентификатор объекта */, contractID?: int /* Идентификатор договора */, tenantID?: int /* Идентификатор тенанта */ }
type AttachmentActionResultBase { tenantID?: int /* Идентификатор тенанта */, contractID?: int /* Идентификатор договора */, attachmentID?: int /* Идентификатор вложения */ }
type AttachmentListResult { fileName?: str /* Название файла (с расширением) */, description?: str /* Описание */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, thumbnailUrl?: str /* Ссылка на эскиз изображения */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, size?: int /* Размер файла в байтах */, created?: datetime /* Дата загрузки UTC */ }
type AttachmentResult { fileName?: str /* Название файла (с расширением) */, description?: str /* Описание */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, thumbnailUrl?: str /* Ссылка на эскиз изображения */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, size?: int /* Размер файла в байтах */, created?: datetime /* Дата загрузки UTC */, attachmentID?: int /* Идентификатор прикрепленного к договору файла */ }
type AttributeTypeResult { id?: int, name?: str, code?: str /* Код типа пользовательского поля */ }
type ContactResultBase { contractID?: int /* Идентификатор договора */, contactID?: int /* Идентификатор контакта */ }
type ContractAssetAddProjection { tenantID?: int, contractID?: int, assetID?: int, isNew?: bool }
type ContractAssetData { assetID?: int, includeChildren?: bool }
type ContractAttributeResult { attribute?: IdNameDeletedResult<Int16>, values?: str[] /* Значение пользовательского поля */, isPublic?: bool /* Флаг, показывающий что поле является публичным */, attributeType?: AttributeTypeResult, measurementUnit?: MeasurementUnitResult, listOfValues?: map<str> /* список допустимых значений в результатах по атрибутам */, domain?: DomainResult }
type ContractContactAddProjection { tenantID?: int, contractID?: int, contactID?: int, isNew?: bool }
type ContractGetResult { contractID?: int /* Идентификатор договора */, companyID?: int /* Идентификатор компании контрагента */, companyName?: str /* Наименование компании контрагента */, name?: str /* Наименовоние договора (в нашем понимании - идентификатор) */, number?: str, description?: str /* Краткое описание договора */, conditions?: str /* Условия договора - полное описание */, dateFrom?: datetime /* Дата начала действия договора */, dateTill?: datetime /* Дата окончания действия договора */, remindExpirationDate?: bool /* Включены или нет напоминания о приближении даты окончания договора */, reminderDate?: datetime /* Дата срабатывания напоминания (уведомление контактных лиц) */, isDeleted?: bool /* Контракт имеет пометку об удалении */ }
type ContractListResult { contractID?: int /* Идентификатор договора */, companyID?: int /* Идентификатор компании контрагента */, companyName?: str /* Наименование компании контрагента */, name?: str /* Наименовоние договора (в нашем понимании - идентификатор) */, number?: str, description?: str /* Краткое описание договора */, conditions?: str /* Условия договора - полное описание */, dateFrom?: datetime /* Дата начала действия договора */, dateTill?: datetime /* Дата окончания действия договора */ }
type ContractMergeData { id?: int, companyID: int, number?: str, name: str, description?: str, agreementConditions?: str, remindExpirationDate?: bool, reminderDate?: datetime, dateFrom: datetime, dateTill?: datetime }
type DomainResult { id?: int /* Внутренний идентификатор домена */, name?: str /* Описание для UI домена */, code?: str }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type FromBodyUploadData { uid?: uuid, contentStream?: file, md5Hash?: str, contentLength?: int, file: str, fileName: str, contentType: str, roles?: int[], coordinate?: str, description?: str, isPublic?: bool, isIgnorePossibleDuplication?: bool, checkSum?: str }
type FromFormUploadData { uid?: uuid, contentStream?: file, md5Hash?: str, contentLength?: int, description?: str, isPublic?: bool, isIgnorePossibleDuplication?: bool, roles?: int[], coordinate?: str, file: file, fileName?: str, contentType?: str }
type IdNameDeletedResult<Int16> { id?: int, name?: str, deleted?: datetime }
type MeasurementUnitResult { id?: int, name?: str, abbreviation?: str /* Аббревиатура единицы измерения */, designation?: str /* Обозначение единицы измерения */ }
type MergeData { attributeID: int, value: str[], isPublic: bool }
type UploadResult { attachmentID?: int /* Идентификатор вложенного файла */, md5Hash?: str /* Проверочная сумма MD5 */, fileName?: str /* Имя загруженного файла */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, contractID?: int /* Идентификатор договора */ }
```
