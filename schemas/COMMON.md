# COMMON — схемы

> **Что здесь:** определения типов запросов/ответов сервиса COMMON. Ручки, ссылающиеся на них — `endpoints/COMMON.md`.

```
type ApplicationResult { code?: str /* Кодовое обозначение приложения */, nameRu?: str /* Название приложения на русском */ }
type Attachments.GetResult { created?: datetime /* Дата загрузки UTC */, description?: str /* Описание файла */, fileName?: str /* Название файла (с расширением) */, id?: int /* Идентификатор файла */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, size?: int /* Размер файла в байтах */ }
type Attachments.ListResult { created?: datetime /* Дата загрузки UTC */, description?: str /* Описание файла */, fileName?: str /* Название файла (с расширением) */, id?: int /* Идентификатор файла */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */, isUploaded?: bool, publicUrl?: str /* Публичная ссылка на файл (только для опубликованных файлов) */, size?: int /* Размер файла в байтах */ }
type Attribute.AddData { attributeTypeID: int, domainID?: int, isPublic: bool, isRelevantForAsset?: bool, isRelevantForCheckList?: bool, isRelevantForCompany?: bool, isRelevantForCompletedWork?: bool, isRelevantForContract?: bool, isRelevantForCustomer?: bool, isRelevantForTask?: bool, isRelevantForTechnician?: bool, measurementUnitID?: int, name: str }
type Attribute.UpdateData { attributeTypeID: int, domainID?: int, id?: int, isPublic: bool, isRelevantForAsset?: bool, isRelevantForCheckList?: bool, isRelevantForCompany?: bool, isRelevantForCompletedWork?: bool, isRelevantForContract?: bool, isRelevantForCustomer?: bool, isRelevantForTask?: bool, isRelevantForTechnician?: bool, measurementUnitID?: int, name: str }
type AttributeResultGet { deleted?: datetime /* Метка времени удаления атрибута */, domain?: DomainResult, isPublic?: bool /* Признак публичного пользоваетльского поля (поля будет доступно на шильде) */, listOfValues?: KeyValueDeleted<String, String>[] /* Список доступных значений */, measurementUnit?: MeasurementUnitResult, name?: str /* Название пользовательского поля */, relevantFor?: RelevantAttributeResult, type?: AttributeTypeResult }
type AttributeResultList { deleted?: datetime /* Метка времени удаления атрибута */, domain?: DomainResult, isPublic?: bool /* Признак публичного пользоваетльского поля (поля будет доступно на шильде) */, listOfValues?: map<str> /* Список доступных значений */, measurementUnit?: MeasurementUnitResult, name?: str /* Название пользовательского поля */, relevantFor?: RelevantAttributeResult, type?: AttributeTypeResult }
type AttributeTypeResult { code?: str /* Код атрибута */, id?: int, name?: str }
type AttributeTypes.ListResult { code?: str /* Код типа атрибута */, name?: str /* Название типа атрибута */ }
type BankResult { address?: str /* Адрес */, bic?: str /* БИК (банковский идентификационный код) */, correspondingAccount?: str /* Корреспондентский счет */, eMail?: str /* E-mail */, id?: int /* Идентификатор банка */, isActive?: bool /* Статус активности */, name?: str /* Название банка */, phone?: str /* Телефон */, swift?: str /* SWIFT */ }
type Contact.AddData { description?: str, email?: str, fullName: str, phone?: str, position?: str }
type Contact.UpdateData { description?: str, email?: str, fullName: str, id: int, phone?: str, position?: str }
type Contacts.GetResult { deleted?: datetime /* Отметка удаления контакта */, description?: str /* Комментарий к контакту */, email?: str /* Электронная почта контакта */, fullName?: str /* ФИО контакта */, id?: int /* Идентификатор контакта */, phone?: str /* Мобильный телефон контакта */, position?: str /* Должность контакта */ }
type Contacts.ListResult { deleted?: datetime /* Отметка удаления контакта */, description?: str /* Комментарий к контакту */, email?: str /* Электронная почта контакта */, fullName?: str /* ФИО контакта */, id?: int /* Идентификатор контакта */, isUsed?: bool /* Отметка что контакт используется */, phone?: str /* Мобильный телефон контакта */, position?: str /* Должность контакта */ }
type Countries.ListResult { name?: str /* Название страны */, threeSymbolCode?: str /* Трехсимвольный код страны */, twoSymbolCode?: str /* Двухсимвольный код страны */ }
type Currencies.ListResult { asciiCode?: str /* ASCII код валюты */, name?: str /* Полное название валюты */, shortName?: str /* Краткое название валюты */ }
type DomainResult { code?: str, id?: int /* Внутренний идентификатор домена */, name?: str /* Описание для UI домена */ }
type DownloadLinkResult { downloadUrl?: str, expiresAfter?: datetime, failures?: str[], headers?: HttpHeader[] }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type Events.ListResult { code?: str /* Код события */, id?: int, name?: str }
type ExtListResult { code?: str /* Код типа атрибута */, domain?: DomainResult, id?: int /* Идентификатор типа атрибута */, name?: str /* Название типа атрибута */ }
type FromBodyUploadData { checkSum?: str, contentLength?: int, contentStream?: file, contentType: str, coordinate?: str, description?: str, file: str, fileName: str, isIgnorePossibleDuplication?: bool, isPublic?: bool, md5Hash?: str, roles?: int[], uid?: uuid }
type FromFormUploadData { contentLength?: int, contentStream?: file, contentType?: str, coordinate?: str, description?: str, file: file, fileName?: str, isIgnorePossibleDuplication?: bool, isPublic?: bool, md5Hash?: str, roles?: int[], uid?: uuid }
type HttpHeader { name?: str, value?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type IdNameResult<Int16> { id?: int, name?: str }
type KeyValueDeleted<String, String> { deleted?: datetime /* Признак удаленного */, key?: str /* Ключ */, value?: str /* Значение */ }
type ListOfValueData { key: str, value: str }
type MeasurementUnitResult { abbreviation?: str /* Аббревиатура единицы измерения */, designation?: str /* Обозначение единицы измерения */, id?: int /* Идентификатор единицы измерения */, name?: str /* Название единицы измерения */ }
type MergeData { attributeID?: int, data: ListOfValueData[] }
type PowerBIReportResult { id?: int, name?: str, reportID?: str /* Идентификатор отчета */, reportType?: IdNameResult<Byte> }
type PublishResult { attachmentID?: int /* Идентификатор вложенного файла */, publicUrl?: str /* Публичная ссылка */ }
type RelevantAttributeResult { asset?: bool /* Флаг применимости к оборудованию */, checkList?: bool /* Флаг применимости к чек-листу */, company?: bool /* Флаг применимости к компании */, completedWork?: bool /* Флаг применимости к выполненной работе */, contract?: bool /* Флаг применимости к договорам */, customer?: bool /* Флаг применимости к заказчику */, task?: bool /* Флаг применимости к задаче */, technician?: bool /* Флаг применимости к сотруднику */ }
type TimezoneGetResult { name?: str /* Название временной зоны */, utcTimeOffsetMinutes?: int /* Разница во времени относительно UTC */ }
type Timezones.ListResult { name?: str /* Название временной зоны */, utcTimeOffset?: str /* Разница во времени относительно UTC */ }
type UploadResult { attachmentID?: int /* Идентификатор вложенного файла */, checkSum?: str /* Проверочная сумма MD5 */, fileName?: str /* Имя загруженного файла */, isProtected?: bool /* Признак того, что вложенный файл доступен ограниченному набору ролей */ }
```
