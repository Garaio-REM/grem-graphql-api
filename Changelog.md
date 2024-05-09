# Changelog

## 1.22.pre5 (2024-05-09)

- support all kinds of kindOfAdministration
- make zipCode and city nullable (since not null is not forced in the database)

## 1.22.pre4 (2024-05-07)

- internal stuff

## 1.22.pre3 (2024-05-03)

- do not expose locked bank accounts

## 1.22.pre2 (2024-03-12)

- internal stuff

## 1.22.pre1 (2024-03-09)

- callDbFunction mutation added
- bankAccount added to person type
- allow damage cases and property checks for condominiums
- ownedBy and published filter arguments for damageCases query
- authorizedApps addoded to user type
- creationDate added to damage cases and property checks

## 1.17.4 (2023-01-23)

- fix idxUnitType queries

## 1.17.3 (2023-01-12)

- internal docker config fix

## 1.17.2 (2023-01-11)

- idxUnitType added to unit

## 1.17.1 (2022-11-21)

- internal refactorings

## 1.16.4 (2022-09-29)

- new query `condominiumCommunity(reference: String!)`

## 1.16.3 (2022-08-16)

- Fix for edge case when a tenantReport query is executed with a keyDate that matches the end date of a unit history time period. In that case the unit was not returned, now it will

## 1.16.2 (2022-07-18)

- new query tenantReport added
- fixed a typo: properyManagementResponsibility -> propertyManagementResponsibility

## 1.16.1 (2022-07-13)

- bug fixed that raised an internal error when a query tried to access condominiums.ownerships
- added association field to CondominiumCommunity

## 1.15.6 (2022-03-05)

- page size for paginated queries has been reduced from 250 to 50 in order to handle very complex queries

## 1.15.5 (2022-03-05)

- filter for tags code tables query removed, all defined tags are returned

## 1.14.7 / 1.15.4 (2022-04-07)

- allPhoneNumbers and allEmails added to supplier type

## 1.15.3 (2022-03-29)

- `user` query has been deprecated
- `liableUntil` added to `unit`
- `bankAccount.notes` can be nil
- support for generic cost centers
- support for additional accounting types (`turnoverRentProperty`, `thirdPartyRentProperty`)
- optional filter argument `tags` for `paginatedAccountings`, `paginatedCondominiumCommunities` and `paginatedProperties`
- **Breaking change**: the root queries `accountings`, `condominiumCommunities`, `properties`, `suppliers` and `supplierOrders` have been deprecated and replaced by corresponding paginated queries (see README for further instructions); adapt your queries since the deprecated queries will be removed in a future release

## 1.15.2 (2022-02-10)

- added account class filter arg for Accounting.accounts

## 1.15.1 (2022-02-07)

- added `addDamageCaseDocumentUrl` and `deleteDamageCaseDocumentUrl`
- removed `UpdateDamageCaseDocumentUrlsInput`
- all damage case documents use `reference` instead of `id`

## 1.15.0 (2022-01-27)

- added `mediaServerConfiguration` query
- fixed possible appearance of duplicated DamageCases/OnSiteMessages
- fixed timezone issue
- fixed CORS issue

## 1.14.6 (2022-01-18)

**Caution: This release will work with any v1.14.x minor release of GARAIO REM; however, in order to deliver responsibilities GARAIO REM v_20220113_master or newer is required**

- unit#availableFrom added
- property#responsibilities added
- condominiumCommunity#responsibilities added

## 1.14.5 (2022-01-03)

- code table taxCodes added
- allPhoneNumbers and allEmails added to person and condominium owner type

## 1.14.4 (2021-11-30)

- code tables developments and developmentAccountingPlans added

## 1.14.3 (2021-11-16)

- fix duplicate properties from properties queries with complex data permissions config

## 1.14.2 (2021-11-04)

- fix timestamps on various tables

## 1.14.1 (2021-10-27)

- added `validFrom` and `valid_until` to `costCenter`
- return proper error response when an exception is raised
- added `discount`, `discountDeadline` and `rebate` to `supplierOrder`
- added `kindOfAdministration` to `property`
- fixed `postalAddress.street` raising an error when null
- added fields `elevatorCount`, `storeyCountOverTerrain`, `storeyCountUnderTerrain`, `buildingCode` to `building`
- added `buildingTypes` to `codeTables`
- added `rentalCosts` and `additionalCostComponents` to `units`
- added `tenancyAgreementTermsAndConditions` to `units`
- renamed `damageCaseDrafts` to `damageCase`
- added `reference`, `documentUrls` and `state` to `damageCase`
- added `damageCase` query to fetch a damage case by its reference value
- added `publishDamageCase` mutation to publish a damage case
- added `updateDamageCaseDocumentUrls` mutation to store document urls for a damage case
- added `deleteDamageCase` mutation to delete a damage case
- renamed `tenancy.noticePer` to `tenancy.expirationDate`

## 1.13.7 (backported to 1.10.8) (2021-08-19)

- `properties` and `condominium_communities` can now be locally limited by providing an optional `latitude_longitude_bounds` parameter

## 1.13.6 (backported to 1.10.8) (2021-08-13)

- fix for a critical bug that returned incomplete / incorrect tenancy data in complex contract / addendum scenarios

## 1.13.5 (2021-07-16)

- server ping endpoint implemented

## 1.13.4 (backported to 1.10.7) (2021-07-09)

- tenancy query can be used with client_credentials authentication

## 1.13.3 (2021-07-06)

- Condominium#location returns german text of corresponding unit-location-code or free text in case unit data in REM has not been migrated to unit-location-code yet
- managementTeam added to condominiumCommunity

## 1.13.2 (2021-06-28)

- salutation added to tenancyApplicantInput

## v1.13.1 (2021-06-15), requires GARAIO REM v1.13.x or later

- createDamageCase mutation implemented
- updateDamageCase mutation implemented
- subscriptions for newDamageCase and updateDamageCase implemented
- damageCaseDrafts query implemented
- Unit#location returns german text of corresponding unit-location-code or free text in case unit data in REM has not been migrated to unit-location-code yet

## 1.10.6 (2021-04-14)

- accounting#accounts has an optional account group numbers filter
- Fallback for email and phone number to the first in list if no appropriate type (private, professional) was added to the person

## 1.10.5 (2021-04-09)

- tenancy#noticePer implemented
- condominiumCommunities query implemented
- condominiumCommunity type implemented
- condominiumBuilding type implemented
- condominium type implemented
- condominiumOwnership type implemented
- condominiumOwner type implemented

## 1.10.4 (2021-02-15)

- internal stuff

## 1.10.3 (2020-12-05)

- Tenancy.isPrimaryTenant added
- Units with a validFrom date in the future are returned again (regression fixed)
- startOfAdministration and endOfAdministration on Building return the the dates of the building
- startOfAdministration, endOfAdministration fields deprecated on Unit
- zipCode and city on Building deprecated

## 1.10.2 (2020-11-04)

- unit query implemented
- startOfAdministration and endOfAdministration on a building are aligned with startOfAdministration and endOfAdministration of the property, regardless  of the actual stored dates
- the queries ```authenticate``` and ```authenticateService``` are deprecated and will be removed in a future release. To authenticate, send a post request to /external/graphql/authenticate/token instead (see README for details)
- optional ```withHistory``` query paramater added for the properties query and the tenancies field
- fixed wrong tenancy start- / endDates in a assumption of contract scenario (Vertragsumschreibung)
- properties query returns properties that are managed in the future, not only properties that managed as of today
- fields validFrom, validUntil added to Unit

## 1.10.1 (2020-10-08)

- scope authorization added on owner, supplier, accounting and concierge data

## 1.10.0 (2020-08-25)

- type, fullName, postalAddress fields added to Person
- owner field added to Property
- tenancyAgreementTypes code table query added
- tenancyAgreementTypeCode added to Tenancy
- supplierRatings code table query added
- Supplier and suppliers query added
- preferredSuppliers fields added to Property
- Accounting, AccountingAccount  added
- accounting, accountings queries added
- properties query filters non active mandates
- accounting field added to Property
- SupplierOrder added
- supplierOrders query added
- VatRate and vatRates query added
- userId field added to TeamMember
- ConciergeContact added
- conciergeRoles code table query added
- conciergeContracts field added to Property and Building
- surface, cubature fields added to Unit
- startOfAdministration, endOfAdministration fields added to Property and Building
- Complexity limiter implemented (see schema docs for details)

## 1.9.2 (2020-07-30)

- tenancy query added
- determine email and phone number of a Person depending on its type
- ECh0010Address added
- Organisation added
- phoneNumber, email, postalAddress and organisation fields added to User
- admWhgNrBfs field added to unit

## 1.9.1 (2020-05-30)

- internal stuff to enable automated service provisioning

## 1.9.0 (2020-05-14)

- internal refactorings and enhancements

## 1.3.4 (2020-05-01)

- tags code table query added

## 1.3.3 (2020-03-14)

- authenticateService query implemented

## 1.3.2 (2020-01-16)

- better namings in TenancyApplicationDossierInput
- tenancies field for a unit has to deliver tenancies that are valid in the future

## 1.3.1 (2019-08-31)

- tenantName field resolver on Unit handles edge cases

## 1.3.0 (2019-08-30)

- tenantName field on Unit got scope protection
- unitCategoryCode added to Unit
- unitCategories code table query added
- units field on Building got optional unitCategoryCodes filter argument

## 1.2.0 (2019-07-07)

- internal refactorings

## 1.1.0 (2019-07-07)

First public release
