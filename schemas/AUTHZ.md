# AUTHZ — схемы

> **Что здесь:** определения типов запросов/ответов сервиса AUTHZ. Ручки, ссылающиеся на них — `endpoints/AUTHZ.md`.
> **Источник:** `snapshots/AUTHZ.json` · файл генерируется пайплайном — руками не править.

```
type AuthorizeData { tenantID: int /* ИД тенанта, в который будет авторизован пользователь. */, tenantMemberID: int /* ИД члена тенанта, в который этот член будет авторизован. */ }
type GenerateData { validity?: str /* Срок действия токена */ }
type IdCodeNameResult<Int16> { id?: int, code?: str, name?: str }
type IdNameResult<Byte> { id?: int, name?: str }
type JwtResultBase { access_token?: str /* JWT-токен для доступа к ресурсам */, refresh_token?: str /* JWT-токен для обновления JWT-токена для доступа к ресурсам */, expires_in?: int /* Количество секунд, через которой токен будет просрочен */, jwtValidTill?: datetime /* Метка времени в UTC, до которой действует JWT */ }
type PostResult { token?: str /* Токен */, created?: datetime /* Метка времени создания токена */, validTill?: datetime /* Срок действия токена */ }
type RefreshData { jwt?: str /* JWT refresh-токен */, refreshJwt?: str /* JWT refresh-токен */, accessJwt?: str, oneTimeLoginToken?: str /* Токен для одноразовой авторизации в тенанте */, tenantID?: int, serviceToken?: str /* Сервисный токен для упрощенной авторизации */ }
type TenantLicenseCurrentResult { license?: IdCodeNameResult<Int16>, dateTill?: datetime /* Дата окончания лицензии */, isTrialPeriod?: bool /* Флаг пробного периода */, dateFrom?: datetime /* Дата начала лицензии */, trialPeriodDays?: int /* Длина пробного периода в днях */ }
type TenantMemberAuthorizationResult { access_token?: str /* JWT-токен для доступа к ресурсам */, refresh_token?: str /* JWT-токен для обновления JWT-токена для доступа к ресурсам */, expires_in?: int /* Количество секунд, через которой токен будет просрочен */, jwtValidTill?: datetime /* Метка времени в UTC, до которой действует JWT */, profile?: UserProfileResult, permissions?: map<str> /* Данные пользователя как члена тенанта. */, refreshToken?: JwtResultBase, tenant?: TenantResult, tenantMember?: TenantMemberResult, tenantLicenses?: TenantLicenseCurrentResult[] /* Данные лицензий тенанта */, featureFlags?: str[] /* Список флагов нового функционала, доступных тенанту */, roleTaskAttribute?: int[] /* Список доступных атрибутов для ролей пользователя по заявке */ }
type TenantMemberResult { id?: int, description?: str /* Описание */, userID?: int /* Идентификатор пользователя */, accountID?: int /* Идентификатор учетной записи */ }
type TenantResult { id?: int, name?: str, fullName?: str /* Полное название тенанта */, uriName?: str /* Uri-постфикс */ }
type UserProfileResult { userID?: int /* Идентификатор пользователя */, firstName?: str /* Имя */, lastName?: str /* Фамилия */, middleName?: str /* Отчество */, email?: str /* Адрес эл.почты */, mobilePhone?: str /* Мобильный телефон */, workPhone?: str /* Рабочий телефон */, otherPhone?: str /* Другой телефон */, avatarUrl?: str /* Ссылка на аватар пользователя */, geoTrackingMode?: IdNameResult<Byte>, accountDomainLogin?: str /* Domain login аккаунта пользователя */, defaultPageWeb?: str /* Стартовая страница для WEB */, defaultPageMobile?: str /* Стартовая страница для МП инженера */ }
```
