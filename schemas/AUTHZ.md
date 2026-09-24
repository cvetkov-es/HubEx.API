# AUTHZ — схемы

> **Что здесь:** определения типов запросов/ответов сервиса AUTHZ. Ручки, ссылающиеся на них — `endpoints/AUTHZ.md`.

```
type AuthorizeData { tenantID: int /* ИД тенанта, в который будет авторизован пользователь. */, tenantMemberID: int /* ИД члена тенанта, в который этот член будет авторизован. */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type GenerateData { validity?: str /* Срок действия токена */ }
type IdCodeNameResultOfShort { code?: str, id?: int, name?: str }
type IdNameResultOfByte { id?: int, name?: str }
type JwtResultBase { access_token?: str /* JWT-токен для доступа к ресурсам */, expires_in?: int /* Количество секунд, через которой токен будет просрочен */, jwtValidTill?: datetime /* Метка времени в UTC, до которой действует JWT */, refresh_token?: str /* JWT-токен для обновления JWT-токена для доступа к ресурсам */ }
type PostResult { created?: datetime /* Метка времени создания токена */, token?: str /* Токен */, validTill?: datetime /* Срок действия токена */ }
type RefreshData { accessJwt?: str, jwt?: str /* JWT refresh-токен */, oneTimeLoginToken?: str /* Токен для одноразовой авторизации в тенанте */, refreshJwt?: str /* JWT refresh-токен */, serviceToken?: str /* Сервисный токен для упрощенной авторизации */, tenantID?: int }
type TenantLicenseCurrentResult { dateFrom?: datetime /* Дата начала лицензии */, dateTill?: datetime /* Дата окончания лицензии */, isTrialPeriod?: bool /* Флаг пробного периода */, license?: IdCodeNameResultOfShort, trialPeriodDays?: int /* Длина пробного периода в днях */ }
type TenantMemberAuthorizationResult { access_token?: str /* JWT-токен для доступа к ресурсам */, expires_in?: int /* Количество секунд, через которой токен будет просрочен */, featureFlags?: str[] /* Список флагов нового функционала, доступных тенанту */, jwtValidTill?: datetime /* Метка времени в UTC, до которой действует JWT */, permissions?: map<str> /* Данные пользователя как члена тенанта. */, profile?: UserProfileResult, refreshToken?: JwtResultBase, refresh_token?: str /* JWT-токен для обновления JWT-токена для доступа к ресурсам */, roleTaskAttribute?: int[] /* Список доступных атрибутов для ролей пользователя по заявке */, tenant?: TenantResult, tenantLicenses?: TenantLicenseCurrentResult[] /* Данные лицензий тенанта */, tenantMember?: TenantMemberResult }
type TenantMemberResult { accountID?: int /* Идентификатор учетной записи */, description?: str /* Описание */, id?: int /* Идентификатор члена тенанта */, userID?: int /* Идентификатор пользователя */ }
type TenantResult { fullName?: str /* Полное название тенанта */, id?: int /* Идентификатор тенанта */, name?: str /* Краткое название тенанта */, uriName?: str /* Uri-постфикс */ }
type UserProfileResult { accountDomainLogin?: str /* Domain login аккаунта пользователя */, avatarUrl?: str /* Ссылка на аватар пользователя */, defaultPageMobile?: str /* Стартовая страница для МП инженера */, defaultPageWeb?: str /* Стартовая страница для WEB */, email?: str /* Адрес эл.почты */, firstName?: str /* Имя */, geoTrackingMode?: IdNameResultOfByte, lastName?: str /* Фамилия */, middleName?: str /* Отчество */, mobilePhone?: str /* Мобильный телефон */, otherPhone?: str /* Другой телефон */, userID?: int /* Идентификатор пользователя */, workPhone?: str /* Рабочий телефон */ }
```
