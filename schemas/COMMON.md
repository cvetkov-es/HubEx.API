# COMMON — схемы

> **Что здесь:** определения типов запросов/ответов сервиса COMMON. Ручки, ссылающиеся на них — `endpoints/COMMON.md`.
> **Источник:** `snapshots/COMMON.json` · файл генерируется пайплайном — руками не править.

```
type ApplicationResult { code?: str /* Кодовое обозначение приложения */, nameRu?: str /* Название приложения на русском */ }
type Attachments.GetResult { id?: int /* Идентификатор файла */, fileName?: str /* Название файла (с расширением) */, description?: str /* Описание файла */, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, isUploaded?: bool, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, size?: int /* Размер файла в байтах */, created?: datetime /* Дата загрузки UTC */ }
type Attachments.ListResult { id?: int /* Идентификатор файла */, fileName?: str /* Название файла (с расширением) */, description?: str /* Описание файла */, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, isUploaded?: bool, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, size?: int /* Размер файла в байтах */, created?: datetime /* Дата загрузки UTC */ }
type Attribute.AddData { name: str, attributeTypeID: int, domainID?: int, isPublic: bool, measurementUnitID?: int, isRelevantForTask?: bool, isRelevantForAsset?: bool, isRelevantForCheckList?: bool, isRelevantForCompletedWork?: bool, isRelevantForContract?: bool, isRelevantForCompany?: bool, isRelevantForCustomer?: bool, isRelevantForTechnician?: bool }
type Attribute.UpdateData { name: str, attributeTypeID: int, domainID?: int, isPublic: bool, measurementUnitID?: int, isRelevantForTask?: bool, isRelevantForAsset?: bool, isRelevantForCheckList?: bool, isRelevantForCompletedWork?: bool, isRelevantForContract?: bool, isRelevantForCompany?: bool, isRelevantForCustomer?: bool, isRelevantForTechnician?: bool, id?: int }
type AttributeResultGet { name?: str /* Название пользовательского поля */, type?: AttributeTypeResult, domain?: DomainResult, isPublic?: bool /* Признак публичного пользоваетльского поля (поля будет доступно на шильде) */, measurementUnit?: MeasurementUnitResult, deleted?: datetime /* Метка времени удаления атрибута */, relevantFor?: RelevantAttributeResult, listOfValues?: KeyValueDeleted<String, String>[] /* Список доступных значений */ }
type AttributeResultList { name?: str /* Название пользовательского поля */, type?: AttributeTypeResult, domain?: DomainResult, isPublic?: bool /* Признак публичного пользоваетльского поля (поля будет доступно на шильде) */, measurementUnit?: MeasurementUnitResult, deleted?: datetime /* Метка времени удаления атрибута */, relevantFor?: RelevantAttributeResult, listOfValues?: map<str> /* Список доступных значений */ }
type AttributeTypeResult { id?: int, name?: str, code?: str /* Код атрибута */ }
type AttributeTypes.ListResult { code?: str /* Код типа атрибута */, name?: str /* Название типа атрибута */ }
type BankResult { id?: int /* Идентификатор банка */, name?: str /* Название банка */, bic?: str /* БИК (банковский идентификационный код) */, correspondingAccount?: str /* Корреспондентский счет */, swift?: str /* SWIFT */, phone?: str /* Телефон */, eMail?: str /* E-mail */, address?: str /* Адрес */, isActive?: bool /* Статус активности */ }
type Contact.AddData { fullName: str, email?: str, phone?: str, position?: str, description?: str }
type Contact.UpdateData { fullName: str, email?: str, phone?: str, position?: str, description?: str, id: int }
type Contacts.GetResult { id?: int /* Идентификатор контакта */, fullName?: str /* ФИО контакта */, email?: str /* Электронная почта контакта */, phone?: str /* Мобильный телефон контакта */, position?: str /* Должность контакта */, description?: str /* Комментарий к контакту */, deleted?: datetime /* Отметка удаления контакта */ }
type Contacts.ListResult { id?: int /* Идентификатор контакта */, fullName?: str /* ФИО контакта */, email?: str /* Электронная почта контакта */, phone?: str /* Мобильный телефон контакта */, position?: str /* Должность контакта */, description?: str /* Комментарий к контакту */, deleted?: datetime /* Отметка удаления контакта */, isUsed?: bool /* Отметка что контакт используется */ }
type Countries.ListResult { name?: str /* Название страны */, twoSymbolCode?: str /* Двухсимвольный код страны */, threeSymbolCode?: str /* Трехсимвольный код страны */ }
type Currencies.ListResult { name?: str /* Полное название валюты */, shortName?: str /* Краткое название валюты */, asciiCode?: str /* ASCII код валюты */ }
type DomainResult { id?: int /* Внутренний идентификатор домена */, name?: str /* Описание для UI домена */, code?: str }
type DownloadLinkResult { downloadUrl?: str, headers?: HttpHeader[], expiresAfter?: datetime, failures?: str[] }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type Events.ListResult { id?: int, name?: str, code?: str /* Код события */ }
type ExtListResult { code?: str /* Код типа атрибута */, name?: str /* Название типа атрибута */, id?: int /* Идентификатор типа атрибута */, domain?: DomainResult }
type FromBodyUploadData { uid?: uuid, contentStream?: file, md5Hash?: str, contentLength?: int, file: str, fileName: str, contentType: str, roles?: int[], coordinate?: str, description?: str, isPublic?: bool, isIgnorePossibleDuplication?: bool, checkSum?: str }
type FromFormUploadData { uid?: uuid, contentStream?: file, md5Hash?: str, contentLength?: int, description?: str, isPublic?: bool, isIgnorePossibleDuplication?: bool, roles?: int[], coordinate?: str, file: file, fileName?: str, contentType?: str }
type HttpHeader { name?: str, value?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type KeyValueDeleted<String, String> { key?: str /* Ключ */, value?: str /* Значение */, deleted?: datetime /* Признак удаленного */ }
type ListOfValueData { key: str, value: str }
type MeasurementUnitResult { id?: int /* Идентификатор единицы измерения */, name?: str /* Название единицы измерения */, abbreviation?: str /* Аббревиатура единицы измерения */, designation?: str /* Обозначение единицы измерения */ }
type MergeData { data: ListOfValueData[], attributeID?: int }
type PowerBIReportResult { id?: int, name?: str, reportID?: str /* Идентификатор отчета */, reportType?: IdNameResult<Byte> }
type PublishResult { attachmentID?: int /* Идентификатор вложенного файла */, publicUrl?: str /* Публичная ссылка */ }
type RelevantAttributeResult { task?: bool /* Флаг применимости к задаче */, asset?: bool /* Флаг применимости к оборудованию */, checkList?: bool /* Флаг применимости к чек-листу */, completedWork?: bool /* Флаг применимости к выполненной работе */, contract?: bool /* Флаг применимости к договорам */, company?: bool /* Флаг применимости к компании */, customer?: bool /* Флаг применимости к заказчику */, technician?: bool /* Флаг применимости к сотруднику */ }
type TimezoneGetResult { name?: str /* Название временной зоны */, utcTimeOffsetMinutes?: int /* Разница во времени относительно UTC */ }
type Timezones.ListResult { name?: str /* Название временной зоны */, utcTimeOffset?: str /* Разница во времени относительно UTC */ }
type UploadResult { attachmentID?: int /* Идентификатор вложенного файла */, checkSum?: str /* Проверочная сумма MD5 */, fileName?: str /* Имя загруженного файла */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */ }
```
