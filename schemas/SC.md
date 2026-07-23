# SC — схемы

> **Что здесь:** определения типов запросов/ответов сервиса SC. Ручки, ссылающиеся на них — `endpoints/SC.md`.

```
type ActionData { contractID: int, data: MergeData[] }
type AssetResultBase { assetID?: int /* Идентификатор объекта */, contractID?: int /* Идентификатор договора */, tenantID?: int /* Идентификатор тенанта */ }
type AttachmentActionResultBase { attachmentID?: int /* Идентификатор вложения */, contractID?: int /* Идентификатор договора */, tenantID?: int /* Идентификатор тенанта */ }
type AttachmentListResult { created?: datetime /* Дата загрузки UTC */, description?: str /* Описание */, fileName?: str /* Название файла (с расширением) */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, size?: int /* Размер файла в байтах */, thumbnailUrl?: str /* Ссылка на эскиз изображения */ }
type AttachmentResult { attachmentID?: int /* Идентификатор прикрепленного к договору файла */, created?: datetime /* Дата загрузки UTC */, description?: str /* Описание */, fileName?: str /* Название файла (с расширением) */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, size?: int /* Размер файла в байтах */, thumbnailUrl?: str /* Ссылка на эскиз изображения */ }
type AttributeTypeResult { code?: str /* Код типа пользовательского поля */, id?: int, name?: str }
type ContactResultBase { contactID?: int /* Идентификатор контакта */, contractID?: int /* Идентификатор договора */ }
type ContractAssetAddProjection { assetID?: int, contractID?: int, isNew?: bool, tenantID?: int }
type ContractAssetData { assetID?: int, includeChildren?: bool }
type ContractAttributeResult { attribute?: IdNameDeletedResult<Int16>, attributeType?: AttributeTypeResult, domain?: DomainResult, isPublic?: bool /* Флаг, показывающий что поле является публичным */, listOfValues?: map<str> /* список допустимых значений в результатах по атрибутам */, measurementUnit?: MeasurementUnitResult, values?: str[] /* Значение пользовательского поля */ }
type ContractContactAddProjection { contactID?: int, contractID?: int, isNew?: bool, tenantID?: int }
type ContractGetResult { companyID?: int /* Идентификатор компании контрагента */, companyName?: str /* Наименование компании контрагента */, conditions?: str /* Условия договора - полное описание */, contractID?: int /* Идентификатор договора */, dateFrom?: datetime /* Дата начала действия договора */, dateTill?: datetime /* Дата окончания действия договора */, description?: str /* Краткое описание договора */, isDeleted?: bool /* Контракт имеет пометку об удалении */, name?: str /* Наименовоние договора (в нашем понимании - идентификатор) */, number?: str, remindExpirationDate?: bool /* Включены или нет напоминания о приближении даты окончания договора */, reminderDate?: datetime /* Дата срабатывания напоминания (уведомление контактных лиц) */ }
type ContractListResult { companyID?: int /* Идентификатор компании контрагента */, companyName?: str /* Наименование компании контрагента */, conditions?: str /* Условия договора - полное описание */, contractID?: int /* Идентификатор договора */, dateFrom?: datetime /* Дата начала действия договора */, dateTill?: datetime /* Дата окончания действия договора */, description?: str /* Краткое описание договора */, name?: str /* Наименовоние договора (в нашем понимании - идентификатор) */, number?: str }
type ContractMergeData { agreementConditions?: str, companyID: int, dateFrom: datetime, dateTill?: datetime, description?: str, id?: int, name: str, number?: str, remindExpirationDate?: bool, reminderDate?: datetime }
type DomainResult { code?: str, id?: int /* Внутренний идентификатор домена */, name?: str /* Описание для UI домена */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type FromBodyUploadData { checkSum?: str, contentLength?: int, contentStream?: file, contentType: str, coordinate?: str, description?: str, file: str, fileName: str, isIgnorePossibleDuplication?: bool, isPublic?: bool, md5Hash?: str, roles?: int[], uid?: uuid }
type FromFormUploadData { contentLength?: int, contentStream?: file, contentType?: str, coordinate?: str, description?: str, file: file, fileName?: str, isIgnorePossibleDuplication?: bool, isPublic?: bool, md5Hash?: str, roles?: int[], uid?: uuid }
type IdNameDeletedResult<Int16> { deleted?: datetime, id?: int, name?: str }
type MeasurementUnitResult { abbreviation?: str /* Аббревиатура единицы измерения */, designation?: str /* Обозначение единицы измерения */, id?: int, name?: str }
type MergeData { attributeID: int, isPublic: bool, value: str[] }
type UploadResult { attachmentID?: int /* Идентификатор вложенного файла */, contractID?: int /* Идентификатор договора */, fileName?: str /* Имя загруженного файла */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, md5Hash?: str /* Проверочная сумма MD5 */ }
```
