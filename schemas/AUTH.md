# AUTH — схемы

> **Что здесь:** определения типов запросов/ответов сервиса AUTH. Ручки, ссылающиеся на них — `endpoints/AUTH.md`.
> **Источник:** `snapshots/AUTH.json` · файл генерируется пайплайном — руками не править.

```
type AccountAddResultEntity { id?: int, verificationRequestValidTill?: datetime, isEmailVerified?: bool, isMobilePhoneVerified?: bool, isPasswordDefined?: bool, isNewAccount?: bool }
type ApplicationListResult { client?: ClientResult, application?: ApplicationResult, pushToken?: str /* Токен push-уведомлений */, timestamp?: datetime /* Метка времени актуальности данных */ }
type ApplicationResult { id?: int, name?: str, version?: str /* Версия */ }
type BanResult { dateTill?: datetime /* Срок действия бана */, banReason?: IdNameResult<Byte> }
type BaseLogoutData { uniqueClientIdentifier: str, applicationID: int }
type CheckData { codeHash?: str, code?: str /* Верификационный код из SMS. */, mobilePhone?: str /* Номер мобильного телефона, на котрый был отправлен код подтверждения. */, email?: str /* Адрес электронной почты, на который был отправлен код подтверждения. */ }
type ClientResult { id?: int /* Идентификатор */, uniqueClientIdentifier?: str /* UniqueClientIdentifier */, agent?: str /* Операционная система */, clientType?: IdNameResult<Byte> }
type CreateData { email?: str /* Адрес эл.почты (UrlEncoded) */, mobilePhone?: str /* Номер мобильного телефона */, domainLogin?: str /* Логин домена аккаунта пользователя */ }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type GetResult { id?: int /* Идентификатор учетной записи */, credential?: str /* Учетные данные */, ban?: BanResult, isAnonymous?: bool, isCrossTenantAdmin?: bool, domainLogin?: str /* Логин домена аккаунта пользователя */, socialProfiles?: SocialProfileResult[] /* Связь с социальными профилями */ }
type IdNameResult<Byte> { id?: int, name?: str }
type ListResult { notificationID?: int /* дентификатор уведомления */, providerID?: int /* Идентификатор метода отсылки уведомления */, subject?: str /* Тема уведомления */, content?: str /* Содержимое уведомления */, created?: datetime /* Дата и время создания уведомления */, sent?: datetime /* Дата и время отправки уведомления */ }
type MergeData { uniqueClientIdentifier: str, applicationID: int, clientTypeID: int, agent?: str, applicationVersion?: str, pushToken?: str }
type PasswordSetData { codeHash?: str, code?: str /* Верификационный код из SMS. */, mobilePhone?: str /* Номер мобильного телефона, на котрый был отправлен код подтверждения. */, email?: str /* Адрес электронной почты, на который был отправлен код подтверждения. */, password: str /* Новый пароль (UrlEncoded) */, currentPassword?: str }
type RemoveData { uniqueClientIdentifier: str, applicationID: int }
type RequestPasswordChangeData { credentials: str }
type SocialProfileResult { id?: int, name?: str, dateFrom?: datetime /* Дата начала использования соц.сети для аутентификации */, dateTill?: datetime /* Дата окончания использования соц.сети для аутентификации */ }
type VerificationResult { id?: int /* Идентификатор уч.записи */, isEmailVerified?: bool /* Признак пройденной проверки адреса эл.почты */, isPhoneVerified?: bool /* Признак пройденной проверки телефона */, verificationRequestValidTill?: datetime /* Признак пройденной проверки телефона */, isPasswordDefined?: bool /* Признак наличия пароля */, isNewAccount?: bool /* Признак новой уч.записи */, verificationCodeRepeatTimeout?: int /* Количество секунд через сколько можно повторить запрос на верификацию */ }
type VerifyEmailData { accountID?: int, email?: str }
type VerifyPhoneData { accountID?: int, phone?: str }
```
