# AUTH — схемы

> **Что здесь:** определения типов запросов/ответов сервиса AUTH. Ручки, ссылающиеся на них — `endpoints/AUTH.md`.

```
type AccountAddResultEntity { id?: int, isEmailVerified?: bool, isMobilePhoneVerified?: bool, isNewAccount?: bool, isPasswordDefined?: bool, verificationRequestValidTill?: datetime }
type ApplicationListResult { application?: ApplicationResult, client?: ClientResult, pushToken?: str /* Токен push-уведомлений */, timestamp?: datetime /* Метка времени актуальности данных */ }
type ApplicationResult { id?: int, name?: str, version?: str /* Версия */ }
type BanResult { banReason?: IdNameResult<Byte>, dateTill?: datetime /* Срок действия бана */ }
type BaseLogoutData { applicationID: int, uniqueClientIdentifier: str }
type CheckData { code?: str /* Верификационный код из SMS. */, codeHash?: str, email?: str /* Адрес электронной почты, на который был отправлен код подтверждения. */, mobilePhone?: str /* Номер мобильного телефона, на котрый был отправлен код подтверждения. */ }
type ClientResult { agent?: str /* Операционная система */, clientType?: IdNameResult<Byte>, id?: int /* Идентификатор */, uniqueClientIdentifier?: str /* UniqueClientIdentifier */ }
type CreateData { domainLogin?: str /* Логин домена аккаунта пользователя */, email?: str /* Адрес эл.почты (UrlEncoded) */, mobilePhone?: str /* Номер мобильного телефона */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type GetResult { ban?: BanResult, credential?: str /* Учетные данные */, domainLogin?: str /* Логин домена аккаунта пользователя */, id?: int /* Идентификатор учетной записи */, isAnonymous?: bool, isCrossTenantAdmin?: bool, socialProfiles?: SocialProfileResult[] /* Связь с социальными профилями */ }
type IdNameResult<Byte> { id?: int, name?: str }
type ListResult { content?: str /* Содержимое уведомления */, created?: datetime /* Дата и время создания уведомления */, notificationID?: int /* дентификатор уведомления */, providerID?: int /* Идентификатор метода отсылки уведомления */, sent?: datetime /* Дата и время отправки уведомления */, subject?: str /* Тема уведомления */ }
type MergeData { agent?: str, applicationID: int, applicationVersion?: str, clientTypeID: int, pushToken?: str, uniqueClientIdentifier: str }
type PasswordSetData { code?: str /* Верификационный код из SMS. */, codeHash?: str, currentPassword?: str, email?: str /* Адрес электронной почты, на который был отправлен код подтверждения. */, mobilePhone?: str /* Номер мобильного телефона, на котрый был отправлен код подтверждения. */, password: str /* Новый пароль (UrlEncoded) */ }
type RemoveData { applicationID: int, uniqueClientIdentifier: str }
type RequestPasswordChangeData { credentials: str }
type SocialProfileResult { dateFrom?: datetime /* Дата начала использования соц.сети для аутентификации */, dateTill?: datetime /* Дата окончания использования соц.сети для аутентификации */, id?: int, name?: str }
type VerificationResult { id?: int /* Идентификатор уч.записи */, isEmailVerified?: bool /* Признак пройденной проверки адреса эл.почты */, isNewAccount?: bool /* Признак новой уч.записи */, isPasswordDefined?: bool /* Признак наличия пароля */, isPhoneVerified?: bool /* Признак пройденной проверки телефона */, verificationCodeRepeatTimeout?: int /* Количество секунд через сколько можно повторить запрос на верификацию */, verificationRequestValidTill?: datetime /* Признак пройденной проверки телефона */ }
type VerifyEmailData { accountID?: int, email?: str }
type VerifyPhoneData { accountID?: int, phone?: str }
```
