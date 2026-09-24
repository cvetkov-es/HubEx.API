# AUTHN — схемы

> **Что здесь:** определения типов запросов/ответов сервиса AUTHN. Ручки, ссылающиеся на них — `endpoints/AUTHN.md`.

```
type AccountRealmResult { realm?: str, tenantID?: int, tenantName?: str }
type AuthenticationResult { access_token?: str, accountHasUserProfile?: bool, accountUserTypeID?: int, expires_in?: int, isAnonymous?: bool, isCrossTenantAdmin?: bool, jwtValidTill?: datetime, refresh_token?: str, requests?: TenantCreationRequestEntity[], tenantEntities?: TenantAuthorizationProjection[] }
type AuthSmsDto { code?: str, phone?: str }
type CredentialData { credential: str }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type JwtResultBase { access_token?: str, accountUserTypeID?: int, expires_in?: int, jwtValidTill?: datetime, refresh_token?: str }
type PhoneDto { phone?: str }
type SetData { code?: str, codeHash?: str, mobilePhone?: str, password: str }
type TenantAuthorizationProjection { accountID?: int, banReasonCode?: str, banReasonID?: int, banTill?: datetime, email?: str, firstName?: str, fullName?: str, hasUserProfile?: bool, isTenantArchived?: bool, isTenantDeleted?: bool, isUserBanned?: bool, lastName?: str, middleName?: str, name?: str, tenantID?: int, tenantMemberDescription?: str, tenantMemberID?: int, tenantMemberValidTill?: datetime, uriName?: str, userBanReasonCode?: str, userBanReasonID?: int, userBanTill?: datetime, userID?: int }
type TenantCreationRequestEntity { accountID?: int, approved?: datetime, created?: datetime, id?: str, isSuccess?: bool, licenseID?: int, message?: str, ownerFirstName?: str, ownerLastName?: str, ownerMiddleName?: str, processed?: datetime, rejected?: datetime, rejectionReason?: str, templateID?: int, tenantFullName?: str, tenantID?: int, tenantName?: str, tenantUriName?: str }
```
