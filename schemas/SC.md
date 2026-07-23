# SC — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса SC. Ручки, ссылающиеся на них — `endpoints/SC.md`.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type AssetResultBase { assetID?: int /* Идентификатор объекта */, contractID?: int /* Идентификатор договора */, tenantID?: int /* Идентификатор тенанта */ }
type AttachmentListResult { created?: datetime /* Дата загрузки UTC */, description?: str /* Описание */, fileName?: str /* Название файла (с расширением) */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, size?: int /* Размер файла в байтах */, thumbnailUrl?: str /* Ссылка на эскиз изображения */ }
type AttachmentResult { attachmentID?: int /* Идентификатор прикрепленного к договору файла */, created?: datetime /* Дата загрузки UTC */, description?: str /* Описание */, fileName?: str /* Название файла (с расширением) */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, size?: int /* Размер файла в байтах */, thumbnailUrl?: str /* Ссылка на эскиз изображения */ }
type AttributeTypeResult { code?: str /* Код типа пользовательского поля */, id?: int, name?: str }
type ContactResultBase { contactID?: int /* Идентификатор контакта */, contractID?: int /* Идентификатор договора */ }
type ContractAttributeResult { attribute?: IdNameDeletedResult<Int16>, attributeType?: AttributeTypeResult, domain?: DomainResult, isPublic?: bool /* Флаг, показывающий что поле является публичным */, listOfValues?: map<str> /* список допустимых значений в результатах по атрибутам */, measurementUnit?: MeasurementUnitResult, values?: str[] /* Значение пользовательского поля */ }
type ContractGetResult { companyID?: int /* Идентификатор компании контрагента */, companyName?: str /* Наименование компании контрагента */, conditions?: str /* Условия договора - полное описание */, contractID?: int /* Идентификатор договора */, dateFrom?: datetime /* Дата начала действия договора */, dateTill?: datetime /* Дата окончания действия договора */, description?: str /* Краткое описание договора */, isDeleted?: bool /* Контракт имеет пометку об удалении */, name?: str /* Наименовоние договора (в нашем понимании - идентификатор) */, number?: str, remindExpirationDate?: bool /* Включены или нет напоминания о приближении даты окончания договора */, reminderDate?: datetime /* Дата срабатывания напоминания (уведомление контактных лиц) */ }
type ContractListResult { companyID?: int /* Идентификатор компании контрагента */, companyName?: str /* Наименование компании контрагента */, conditions?: str /* Условия договора - полное описание */, contractID?: int /* Идентификатор договора */, dateFrom?: datetime /* Дата начала действия договора */, dateTill?: datetime /* Дата окончания действия договора */, description?: str /* Краткое описание договора */, name?: str /* Наименовоние договора (в нашем понимании - идентификатор) */, number?: str }
type DomainResult { code?: str, id?: int /* Внутренний идентификатор домена */, name?: str /* Описание для UI домена */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type IdNameDeletedResult<Int16> { deleted?: datetime, id?: int, name?: str }
type MeasurementUnitResult { abbreviation?: str /* Аббревиатура единицы измерения */, designation?: str /* Обозначение единицы измерения */, id?: int, name?: str }
```
