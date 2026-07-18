# AUTH — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса AUTH. Ручки, ссылающиеся на них — `endpoints/AUTH.md`.
> **Источник:** swagger сервиса AUTH · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type ApplicationListResult { application?: ApplicationResult, client?: ClientResult, pushToken?: str /* Токен push-уведомлений */, timestamp?: datetime /* Метка времени актуальности данных */ }
type ApplicationResult { id?: int, name?: str, version?: str /* Версия */ }
type BanResult { banReason?: IdNameResult<Byte>, dateTill?: datetime /* Срок действия бана */ }
type ClientResult { agent?: str /* Операционная система */, clientType?: IdNameResult<Byte>, id?: int /* Идентификатор */, uniqueClientIdentifier?: str /* UniqueClientIdentifier */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type GetResult { ban?: BanResult, credential?: str /* Учетные данные */, domainLogin?: str /* Логин домена аккаунта пользователя */, id?: int /* Идентификатор учетной записи */, isAnonymous?: bool, isCrossTenantAdmin?: bool, socialProfiles?: SocialProfileResult[] /* Связь с социальными профилями */ }
type IdNameResult<Byte> { id?: int, name?: str }
type ListResult { content?: str /* Содержимое уведомления */, created?: datetime /* Дата и время создания уведомления */, notificationID?: int /* дентификатор уведомления */, providerID?: int /* Идентификатор метода отсылки уведомления */, sent?: datetime /* Дата и время отправки уведомления */, subject?: str /* Тема уведомления */ }
type SocialProfileResult { dateFrom?: datetime /* Дата начала использования соц.сети для аутентификации */, dateTill?: datetime /* Дата окончания использования соц.сети для аутентификации */, id?: int, name?: str }
```
