# GSM Data Dictionary

**Model:** GSM

**Generated:** 2026-11-04 11:27:43 AM

---

**Table Name:** egm_profile_group_status_type

**Description**

Lookup table for device profile group status types.  

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each profile group status type.   |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_profile_group_status_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_h

**Description**

Contains the historical changes made to the site records within the required retention period. 

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| site_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each site type. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| ref_number | varchar | 10 | NOT NULL | Unique site number assigned to each site. |
| DESCR | varchar | 100 | NOT NULL | Description of the site. |
| REVISION_NUMBER | bigint | 8 | NOT NULL | Revision number used to synchronize configuration changes. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| domain_id | integer | 4 | NOT NULL | - |
| time_zone_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each time zone type. |
| entity_status_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each entity status in the system. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| cross_valid_all_flag | character | 1 | NOT NULL | Identifies if the site can validate tickets from any other site. |
| cross_valid_chain_flag | character | 1 | NOT NULL | Identifies if the site can validate tickets from another site belonging to the same chain (aka company). |
| tito_enabled_flag | character | 1 | NOT NULL | Flag to identify if tito is enabled on the site. Default is N. |
| invoice_enabled_flag | character | 1 | NOT NULL | Flag to identify if invoicing is enabled on the site. Default is N. |
| AUDIT Type | character | 1 | NOT NULL | Identifies the operation resulting in the creation of the record.  The valid values are (I) Insert, (U) Update and (D) Delete. |
| activation_date | timestamp | 8 | NULL | Date on which the site was activated.  If null then site was not activated at that time. |
| deactivation_date | timestamp | 8 | NULL | Date on which the site was deactivated.  If null then site was still active at that time. |
| cashout_header_use_gaming_site_name_flag | character | 1 | NOT NULL | Indicates if the cashout ticket header should use the gaming site name as the ticket header. |
| cashout_header_use_gaming_site_address_flag | character | 1 | NOT NULL | Indicates if the cashout ticket header should use the gaming site address as the ticket header. |
| entity_reason_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity reason type in the system. |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_entity_status_detail

**Description**

Table contains site entity status details.

### Primary Key

**Primary Key Columns:** ID, VERSION_NUMBER

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| ID | integer | 4 | NOT NULL | Unique identiifer assigned to each site_entity_status_detail record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_entity_status_detail_pk | id, version_number |
| site_entity_status_detail_i1 | site_id, entity_status_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| site_entity_status_detail_fk1 | site_entity_status_detail | entity_status_type |
| site_entity_status_detail_fk2 | site_entity_status_detail | site |

**Table Name:** user_audit_log

**Description**

This table contains details of user activity that alters data that has been configured to be monitored.  It provides an audit log by tracking the entity/object

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | System generated identifier that uniquely identifies a specific user audit log entry based on a single transaction. |
| operation_type | varchar | 100 | NOT NULL | The name of the transaction being processed. |
| entity_type | varchar | 50 | NOT NULL | The name of the entity that is the main target of this transaction. For example, if you were updating the address of a site, site would be the entity_type while site_address would be the item_type. |
| entity_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the record that corresponds to the entity_type, and is the record that was inserted/updated/deleted. |
| entity_display_value | varchar | 255 | NOT NULL | A textual description or name of the record that would be displayed to the User. |
| anonymized_flag | character | 1 | NOT NULL | A Y/N flag indicating if the data has been anonymized so that identifying data is not displayed. |
| audit_user_id | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| operation_id | varchar | 50 | NULL | An application generated identifier to uniquely identify an operation being performed. |
| parent_operation_id | varchar | 50 | NULL | An application generated identfier to identify the parent operation. |
| item_id | integer | 4 | NULL | A system generated identifier that uniquely identifies the record that corresponds to the item_type, and is the record that was inserted/updated/deleted. |
| item_type | varchar | 50 | NULL | The sub-entity in a transaction, that is being updated.  For example, if you are updating the site address, site would be the main entity while the site_address would be the sub-entity/item type. |
| item_display_value | varchar | 255 | NULL | A textual description of the sub-enttiy data you are inserting/updateing/deleting. |

### Indexes

| Index Name | Columns |
|------------|---------|
| user_audit_log_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** user_audit_log_reference

**Description**

Stored the pre & post values for data that was updated.

### Primary Key

**Primary Key Columns:** ID

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| ID | integer | 4 | NOT NULL | System gernerated identifier that uniquely identifies a single change to a data value. |
| attribute_name | character | 100 | NOT NULL | The name of the data that was inserted/updated/deleted. |
| old_value | varchar | 1000 | NULL | The value of the data prior to the insert/update/delete. On insert old is null and new is inserted value, on delete new is null and old is the deleted value. |
| new_value | varchar | 1000 | NULL | The value of the data after the insert/update/delete. On insert old is null and new is inserted value, on delete new is null and old is the deleted value. |
| level | integer | 4 | NULL | Undefined. |
| id | integer | 4 | NOT NULL | System genrated identifier that uniquely identifies a specific user audit log entry based on a single transaction. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| user_audit_log_reference_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| user_audit_log_reference_fk1 | user_audit_log_reference | user_audit_log |

**Table Name:** vendor_domain

**Description**

Identifies which domains can used to use which vendors.  Vendors can be assigned to EGMs that have access to the same domains if the domain_access_list_flag in the vendor table is set to 'Y'.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vendor domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated vendor. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the Vendors access.   |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vendor. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vendor_domain_pk | id |
| vendor_domain_uk1 | domain_id, vendor_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vendor_domain_fk1 | vendor_domain | vendor |

**Table Name:** vsc_config_domain

**Description**

Identifies which domains can used to use which VSC Configurations. VSC Configurations can be assigned to EGMs that have access to the same domains if the domain_access_list_flag in the vendor table is set to 'Y'.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC Configuration domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated VSC Configuration. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the VSC Configs access.   |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC Configuration. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_config_domain_pk | id |
| vsc_config_domain_uk1 | domain_id, vsc_config_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_config_domain_fk1 | vsc_config_domain | vsc_config |

**Table Name:** vsc_config_domain_h

**Description**

The table holds the history of the vsc_config and domain_id relationships for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC Configuration domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated VSC Configuration. |
| deleted_flag | character | 1 | NOT NULL | dentifies if the domain has been removed from the VSC Configs access.  |
| vsc_config_id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC Configuration. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_config_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** license_domain

**Description**

Identifies which domains can use which licenses.  Licenses can be assigned to Sites that have access to the same domains if the domain_access_list_flag in the license table is set to 'Y'.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each license domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated license. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the licenses access.   |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each License in the system. |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_domain_pk | id |
| license_domain_uk1 | domain_id, license_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| license_domain_fk1 | license_domain | license |

**Table Name:** license_domain_h

**Description**

Contains a history of license domains up to the configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each license domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated license. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the Licenses access.   |
| license_id | integer | 4 | NOT NULL | Unique identifier assigned to each License in the system. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** contact_h

**Description**

Contains a history of the contacts managed by the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each contact in the system. |
| phone_number_backup | varchar | 24 | NULL | Contact backup phone number. |
| phone_number | varchar | 24 | NULL | Contact primary phone number. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| last_name | varchar | 50 | NOT NULL | Last name of contact. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| middle_name | varchar | 50 | NULL | Middle name of contact. |
| fax_number | varchar | 24 | NULL | Contact fax number. |
| first_name | varchar | 50 | NOT NULL | First name of contact. |
| email_addr | varchar | 100 | NULL | Contact email address. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| contact_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** model_domain

**Description**

Identifies which domains can used to use which model.  Models can be assigned to EGMs that have access to the same domains if the domain_access_list_flag in the model table is set to 'Y'.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each model domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated model. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the models access.   |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each model. |

### Indexes

| Index Name | Columns |
|------------|---------|
| model_domain_pk | id |
| model_domain_uk1 | domain_id, model_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| model_domain_fk1 | model_domain | model |

**Table Name:** model_domain_h

**Description**

The table holds the history of the model and domain relationships for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each model domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated model. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the models access.   |
| model_id | integer | 4 | NOT NULL | Unique identifier assigned to each model. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| model_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** trait_domain

**Description**

Identifies which domains can use which traits.  Traits can be assigned to entities that have access to the same domains if the domain_access_list_flag in the license table is set to 'Y'.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated trait. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the Traits access.   |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_domain_pk | id |
| trait_domain_uk1 | domain_id, trait_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| trait_domain_fk1 | trait_domain | trait |

**Table Name:** trait_domain_h

**Description**

Contains a history of domain traits for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated trait. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the traits access.   |
| trait_id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** addr_h

**Description**

Contains a history of the addresses managed by the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| zip | varchar | 25 | NOT NULL | Postal or Zip code. |
| line2 | varchar | 100 | NULL | Second Line of an Address. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| po_box | varchar | 10 | NULL | Postal office box number. |
| city | varchar | 30 | NOT NULL | City. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each Address. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| line1 | varchar | 100 | NOT NULL | First Line of an Address. |
| state | varchar | 25 | NOT NULL | State or Province. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| addr_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** contact_addr_h

**Description**

Contains the contact addresses managed by the application.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| addr_id | integer | 4 | NOT NULL | Unique identifier assigned to each address in the system. |
| contact_id | integer | 4 | NOT NULL | Unique identifier assigned to each contact in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each contact address. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| addr_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each address type in the system. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| contact_addr_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_contact_h

**Description**

Contains a history of the site contacts managed by the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site contact. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| contact_id | integer | 4 | NOT NULL | Unique identifier assigned to each contact in the system. |
| contact_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each contact type. |
| site_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| primary_flag | character | 1 | NOT NULL | Indicates if the contact is the primary contact or not. Default is N. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_contact_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** profile_group_domain_h

**Description**

Contains the history of domain profile group assignments for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each configuration profile domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| domain_id | integer | 4 | NOT NULL | Unique identifier assigned to each domain.  The domain in this table will represent jurisdictions. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| profile_group_id | integer | 4 | NULL | Unique identifier assigned to each profile group. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| profile_group_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** gaming_hours_profile_domain_h

**Description**

Table holds the history of Gaming Hours Profile domains for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each Gaming Hours Profile Domain combination.   |
| gaming_hours_profile_id | integer | 4 | NOT NULL | unique identifier assigned to each gaming hours profile. |
| domain_id | integer | 4 | NOT NULL | Unique identifier assigned to each domain. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| gaming_hours_profile_domain_h_pk | id, audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** egm_h

**Description**

Contains a history of the EGMs managed by the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DESCR | varchar | 100 | NOT NULL | Description of the EGM. |
| ip_addr | character | 15 | NULL | EGM IP Address. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM in the system. |
| entity_status_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system. |
| REVISION_NUMBER | bigint | 8 | NOT NULL | Revision number used to synchronize configuration changes. |
| position_number | integer | 4 | NOT NULL | EGM position number. |
| egm_protocol_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each EGM protocol. |
| comm_idn | varchar | 50 | NOT NULL | Network Id for EGM. Legacy CLIENT_ID, ie: IGT_00010010
. |
| install_date | timestamp | 8 | NOT NULL | Date on which the EGM was installled. |
| purchase_amount | decimal | 16 | NULL | Purchase amount of the EGM. |
| asset_ref_number | varchar | 32 | NOT NULL | Customer assigned asset number. |
| deinstall_date | timestamp | 8 | NULL | Date on which the EGM was uninstalled. NULL if EGM still installed. |
| model_id | integer | 4 | NOT NULL | Unique identifier assigned to each model. |
| serial_number | varchar | 32 | NOT NULL | EGM serial number. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| purchase_date | timestamp | 8 | NULL | Date on which the EGM was purchased. |
| vsc_id | integer | 4 | NOT NULL | Unique identifier assigned to a VSC. |
| invoice_enabled_flag | character | 1 | NOT NULL | Flag to identify if tito is enabled on the egm. Default is Y. Site also has to be invoice enabled for the egms to be included in the invoice. |
| domain_id | integer | 4 | NOT NULL | System generated identifier that uniquely identifies the domain that is associated to the site where this egm is installed.  |
| egm_gaming_hours_profile_id | integer | 4 | NULL | Unique identifier assigned to each EGM Gaming Hours Profile. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vendor_h

**Description**

Contains a history of the vendors managed by the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vendor. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| DESCR | varchar | 100 | NOT NULL | Vendor description. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| owner_domain_id | integer | 4 | NULL | The domain that generated or updated the vendor. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access by domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in VENDOR_DOMAIN table. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. |
| entity_type_key_code | varchar | 50 | NOT NULL | A value that uniquely identifies the entity type supplied by this vendor. Ex EGM, SRU. |
| manufacturer_code | varchar | 3 | NULL | Manfacturer code associated to the vendor. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vendor_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** model_h

**Description**

Contains the models history managed by the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DESCR | varchar | 100 | NOT NULL | Model description. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| vendor_id | integer | 4 | NOT NULL | Unique identifier assigned to each vendor. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each model. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the model. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in model_domain table. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. |

### Indexes

| Index Name | Columns |
|------------|---------|
| model_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_h

**Description**

Contains a history of the VSCs (VLT site controllers) managed by the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| entity_status_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC in the system. |
| vsc_config_id | integer | 4 | NOT NULL | - |
| asset_ref_number | varchar | 32 | NULL | Customer assigned asset number. |
| serial_number | varchar | 32 | NOT NULL | VSC Serial number. |
| comm_idn | varchar | 50 | NOT NULL | Network Id for Site Controller. Legacy CLIENT_ID from ESConnect. |
| comm_active_flag | character | 1 | NOT NULL | Flag to identify whether the VSC communications are active ot not.  Default is N. |
| install_date | timestamp | 8 | NULL | Date on which the VSC was installed. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| site_id | integer | 4 | NOT NULL | - |
| purchase_date | timestamp | 8 | NULL | Date on which the VSC was purchased. |
| REVISION_NUMBER | bigint | 8 | NOT NULL | Revision number used to synchronize configuration changes. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if the entity has been logically deleted. Default is N. |
| ip_addr | varchar | 15 | NULL | VSC IP address. |
| DESCR | varchar | 100 | NOT NULL | Description of the VSC. |
| deinstall_date | timestamp | 8 | NULL | Date on which the VSC is deinstalled.  If null then still installed. |
| domain_id | integer | 4 | NOT NULL | System generated identifier that uniquely identifies the domain that is associated to the site where this vsc is installed. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vendor_domain_h

**Description**

Contains a history of vendor domains for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vendor domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated vendor. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the Vendors access.   |
| vendor_id | integer | 4 | NOT NULL | Unique identifier assigned to each vendor. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| vendor_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** license_h

**Description**

Contains a history of licenses managed by the application for a configurable time period.


### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| issue_date | timestamp | 8 | NULL | License issue date. |
| documentation_ref | varchar | 250 | NULL | License documentation reference. |
| status_change_comment | varchar | 250 | NULL | Comment to explain the status change on the the license. |
| license_status_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each license status in the system.Unique identifier for license status. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| expire_date | timestamp | 8 | NULL | License expiration date. |
| comment | varchar | 250 | NULL | License comment. |
| license_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each license type in the system. |
| max_egms | integer | 4 | NOT NULL | Maximum number of EGMs allowed by this license. |
| license_ref_number | varchar | 20 | NOT NULL | License reference number. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each License in the system. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | GUI user identifier of who last updated record. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the License. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in license_domain table. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_license_h

**Description**

Contains a history of site licenses managed by the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| license_id | integer | 4 | NOT NULL | Unique identifier assigned to each license in the system. |
| site_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site_license. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_license_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** cabinet_dvc_cfg_profile_h

**Description**

Contains the history of the parameters that are associated to the cabinet device configuration profile for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| large_win_limit | decimal | 16 | NOT NULL | Large win amount. |
| idle_time_period | integer | 4 | NOT NULL | Amount of time, in milliseconds, with a 0 (zero) credit meter and no player input before an EGM is considered idle. |
| report_denom_id | integer | 4 | NOT NULL | Unique identifier associated to the report denomination. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| locale_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code for each locale type. |
| sync_meter_to_host_flag | character | 1 | NOT NULL | Identifies if the meters should be sync to the host. |
| currency_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each currency tracked in the system. |
| reel_stop_flag | character | 1 | NOT NULL | This will allow the host to enable/disable whether the EGM will allow the player to stop the reels during game play, effectively ending the game cycle. |
| time_zone_offset | varchar | 6 | NOT NULL | The offset from Universal Coordinate Time (UCT) to local time that should be used when displaying date and time to a locak user of the EGM. |
| no_response_timer | integer | 4 | NULL | Amount of time a device will wait for a response before the timeout logic is invoked. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| accept_non_cash_amount_type_key_code | varchar | 50 | NOT NULL | Controls when an EGM may accept non-cashable transfers. |
| auto_cashout_behaviour_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to auto cashout behaviour. |
| outcome_tax_percent | integer | 4 | NOT NULL | This is to support winner taxation parameters. Tax percentage value |
| auto_cashout_amount | decimal | 16 | NULL | Amount to cashout  if the AUTO_CASHOUT_LIMIT is reached or exceeded by the EGM.  If this amount exceeds the credit meter, only the credit meter amount is cashoed out. |
| auto_cashout_limit | decimal | 16 | NULL | When the credit meter reaches or exceeeds this value, the EGM must initiate a voucher cashout. |
| outcome_tax_threshold | integer | 4 | NOT NULL | This is to support winner taxation parameters. Tax treshold value |
| reel_duration | integer | 4 | NOT NULL | This provides a method for a host to control the duration of a game’s game-cycle, that is, the duration of the reel spin animation. |
| min_log_entries | integer | 4 | NULL | Minimum number of log entries that the EGM must maintain in persistent memory. |
| max_credit_meter | decimal | 16 | NOT NULL | Maximum value permitted on the credit meter. |
| idle_text | varchar | 500 | NULL | Text message that will be displayed on the VLT when the cabinet is idle. |
| money_input_disable_limit | decimal | 16 | NULL | When the credit meter reaches or exceeds this value, all money input devices must be disabled by the EGM. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| cabinet_dvc_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** printer_dvc_cfg_profile_h

**Description**

Contains a history of the parameters that are associated to the printer device configuration profile for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| printer_dvc_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** coin_acceptor_dvc_cfg_profile_h

**Description**

Contains a history of parameters that are associated to the coin acceptor device configuration profile for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| time_to_live_timer | integer | 4 | NULL | Time-to-live value for requests originated by the device. |
| no_response_timer | integer | 4 | NULL | Amount of time a device will wait for a response before the timeout logic is invoked. |
| host_acknowledge_coin_flag | character | 1 | NOT NULL | Indicates whether the device should accept any notes. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| coin_acceptor_dvc_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** note_acceptor_dvc_cfg_profile_h

**Description**

Contains a history of the parameters that are associated to the note acceptor device configuration profile for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| voucher_enabled_flag | character | 1 | NOT NULL | Indicates whether the device should accept any vouchers. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| host_authorize_notes_flag | character | 1 | NOT NULL | Indicates whether EGM must seek authorization from a host in order to redeem each note inserted. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| time_to_live_timer | integer | 4 | NULL | Time-to-live value for requests originated by the device. |
| no_response_timer | integer | 4 | NULL | Amount of time a device will wait for a response before the timeout logic is invoked. |
| note_enabled_flag | character | 1 | NOT NULL | Indicates whether the device should accept any notes. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| note_acceptor_dvc_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** voucher_dvc_cfg_profile_h

**Description**

Contains the history of the parameters that are associated to the voucher device configuration profile for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| validation_id_list_refresh_timer | bigint | 8 | NULL | A timer is reset to the value each time EGM receives a  validationData command.  The default is 12 hours.  If the timer expires, EGM must send getValidationData command. |
| cash_promo_expiration_period | integer | 4 | NOT NULL | Number of days before cashable promo vouchers expire. |
| min_number_validation_ids | integer | 4 | NULL | Minimum number of validation identifiers that the EGM should have at all times. |
| validation_id_list_life_timer | bigint | 8 | NULL | A timer is reset to the value each time the EGM receives a  validationData command.  The default is 24 hours.  If the timer expires, validation identifiers may not be used. |
| print_offline_flag | character | 1 | NOT NULL | Allows vouchers to be printed while the host is offline. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| max_number_validation_ids | integer | 4 | NULL | Maximum number of validation identifiers that the EGM may buffer. |
| time_to_live_timer | integer | 4 | NULL | Time-to-live value for requests originated by the device. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| voucher_dvc_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** event_handler_dvc_cfg_profile_h

**Description**

Contains the history of parameters that are associated to the event handler device configuration profile for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| time_to_live_timer | integer | 4 | NULL | Time-to-live value for requests originated by the device. |
| min_log_entries | integer | 4 | NULL | Minimum number of log entries that the EGM must maintain in persistent memory. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| event_handler_dvc_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** note_acceptor_dvc_cfg_profile_note_h

**Description**

Contains a history of notes that are associated to the note acceptor device configuration profile retained for a configurable time period.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| note_enabled_flag | character | 1 | NOT NULL | Indicates whether the device will accept the note. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| note_acceptor_dvc_cfg_profile_id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each note acceptor device configuration profile note. |
| VERSION_NUMBER | integer | 4 | NOT NULL | The version number will be used on some of the tables to handle locking.  When a user selects a record for update, the version number will be used in the UPDATEs WHERE clause.  If the version number no longer matches an error will be displayed to the use |
| note_acceptor_note_id | integer | 4 | NOT NULL | Unique identifier assigned to each note acceptor note tracked in the application. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| note_acceptor_dvc_cfg_profile_note_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** note_acceptor_note_h

**Description**

Contains the history of note acceptor notes for a a configurable retention period.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DESCR | varchar | 100 | NOT NULL | Description of the note acceptor note. |
| number_of_base_units | decimal | 16 | NOT NULL | Amount applied to the players cashable amount for each note accepted. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each note acceptor note tracked in the application. |
| currency_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each currency tracked in the system. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| note_acceptor_note_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** cfg_profile_h

**Description**

Table holds the history of the defined device configuration profiles used in the system for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| cfg_profile_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each configuration profile type. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| DESCR | varchar | 100 | NOT NULL | Description of the configuration profile. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| revision_number | bigint | 8 | NOT NULL | This revision number will hold the true revision of the configuration profile.  It will not be used for locking.  Implemented to accommodate they way in which configuration profiles are being updated. |
| allow_update_cfg_profile_flag | character | 1 | NOT NULL | Indicates whether the default profile is updateable. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** profile_group_h

**Description**

Table holds the history of logical groupings of configurations to facilitate grouping profiles on the GUI for a configurable retention period.


### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| profile_group_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each group profile type. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each profile group. |
| descr | varchar | 100 | NOT NULL | Description of the profile group. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in profile_group_domain table. |
| owner_domain_id | integer | 4 | NULL | The domain that generated or updated the profile group. |

### Indexes

| Index Name | Columns |
|------------|---------|
| profile_group_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** profile_group_cfg_profile_h

**Description**

Table holds the history of logical grouping of profiles to facilitate grouping the profiles on the GUI for a configurable retention period.


### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| cfg_profile_id | integer | 4 | NOT NULL | - |
| profile_group_id | integer | 4 | NOT NULL | Unique identifier assigned to each profile group. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each record that links profile groups and profiles. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| profile_group_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** egm_profile_group_h

**Description**

Contains the history of the synchronized and unsynchronized/in progress profile groups assigned to an EGM for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| egm_id | integer | 4 | NOT NULL | - |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Profile Group assignment. |
| profile_group_id | integer | 4 | NOT NULL | Unique identifier assigned to each profile group. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| egm_profile_group_status_typ_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each profile group status type.   |
| configuration_start_datetime | timestamp | 8 | NULL | Date the device configuration started. |
| configuration_complete_datetime | timestamp | 8 | NULL | Date the device configuration completed. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_profile_group_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** sas_dvc_cfg_profile_h

**Description**

History of the SAS device configuration profile for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| egm_protocol_revision_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each EGM protocol revision type. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| protocol_version | integer | 4 | NULL | 'SAS EGM protocol version. |

### Indexes

| Index Name | Columns |
|------------|---------|
| sas_dvc_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** g2s_host_config_profile_h

**Description**

Contains a history of G2S Host configuration profile details for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each G2S Host Config Profile record. |
| g2s_host_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each G2S Host. |
| can_modify_remote_flag | character | 1 | NOT NULL | Identifies if the host is remotely modifiable before changing some params for the host.  Default is ''Y''. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| can_modify_local_flag | character | 1 | NOT NULL | Identifies if the host is locally modifiable before changing some params for the host.  Default is 'N'. |
| authorized_host_flag | character | 1 | NOT NULL | Indicates whether it is an authorized host or not.  Default is 'N'. |
| display_communication_fault_flag | character | 1 | NOT NULL | Indicates whether a communications fault message should be displayed if the communications channel is unavailable. Default is 'Y'. |
| allow_multicast_flag | character | 1 | NOT NULL | Indicates whether the host is authorized to send multicast messages. Not required if hostRegistered is set to false.  Default is 'N'. |
| no_response_timer | integer | 4 | NOT NULL | The no-response timer used to determine whether the host has lost communications with another host.  Amount of time the host will wait for a response before the timeout logic is invoked.   |
| time_to_live_timer | integer | 4 | NOT NULL | Time-to-live value for requests originated by the host. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| g2s_host_config_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** license_type_site_type_h

**Description**

Contains a history of the valid site types associated to each license type for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | - |
| license_type_key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each license type. |
| site_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each site type. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_type_site_type_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** system_gaming_hours_override_h

**Description**

Contains a history of the override hours that the EGMS are allowed to be playable for a configurable retention period.


### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each system gaming hours override record. |
| end_datetime | timestamp | 8 | NOT NULL | The date and time of the override period end. |
| DESCR | varchar | 100 | NOT NULL | Description of override reason. |
| gaming_hours_profile_id | integer | 4 | NOT NULL | Unique identifier assigned to each gaming hours profile. |
| start_datetime | timestamp | 8 | NOT NULL | The date and time of the override period start. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| system_gaming_hours_override_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** gaming_hours_profile_h

**Description**

Contains the gaming hour profiles used in the application.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each gaming hours profile. |
| DESCR | varchar | 100 | NOT NULL | Description of the gaming hours profile. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the gaming hours profile. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in gaming_hours_profile_domain table. |
| external_id | varchar | 16 | NULL | Captures id from legacy system during data conversion. |

### Indexes

| Index Name | Columns |
|------------|---------|
| gaming_hours_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** egm_gaming_hours_override_h

**Description**

Contains a history of override hours for specific days in an EGM Gaming Hours Group for a configurable retention period. 
. 

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| technical_override_flag | character | 1 | NOT NULL | Flag to indicate if the override record represents a technical override.  Technical Override available time does not change the timeline setting but keeps the system on for Technicians and suppresses log events to main system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Group Override for a specific day and period of time. |
| egm_gaming_hours_profile_id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Profile. |
| start_datetime | timestamp | 8 | NOT NULL | The date and time of the override period start. |
| end_datetime | timestamp | 8 | NOT NULL | The date and time of the override period end. |
| close_all_day_flag | character | 1 | NOT NULL | Flag to indicate if the vlt will not be operating all day.  The default is 'N'. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_gaming_hours_override_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** system_gaming_hours_h

**Description**

Contains a history of the hours that the EGMS are allowed to be playable for a configurable retention period. 


### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| weekday_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each weekday. |
| gaming_hours_profile_id | integer | 4 | NOT NULL | Unique identifier assigned to each gaming hours profile. |
| start_time | timestamp | 8 | NOT NULL | Time that the EGMs are operational.  1900-01-01-00.00.00 represents midnight. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| end_time | timestamp | 8 | NOT NULL | Time that the EGMs end operation.  1900-01-01-00.00.00 represents midnight.
 |
| id | integer | 4 | NOT NULL | - |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| system_gaming_hours_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** egm_gaming_hours_profile_h

**Description**

History of EGM Gaming Hour Groups - allows one or more egms assigned to a a profile to override specific daily hours or regular weekly hours for a configurable retention period. 

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| site_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| gaming_hours_profile_id | integer | 4 | NULL | Unique identifier assigned to each Gaming Hours Profile Domain combination. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Profile. |
| descr | varchar | 100 | NOT NULL | Description of the EGM Gaming Hours Profile |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_gaming_hours_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** egm_gaming_hours_h

**Description**

Contains the history of the regular opening schedule excluding the override hours for an egm_gaming_hours_profile.  Same as the weekly hours in INTELLIGEN for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Group Weekly Override. |
| egm_gaming_hours_profile_id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Profile. |
| weekday_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each weekday. |
| start_time | timestamp | 8 | NOT NULL | Start Time of a period of time. |
| end_time | timestamp | 8 | NOT NULL | End Time of a period of time. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_gaming_hours_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** license_gaming_hours_override_h

**Description**

Contains the history of override hours associated to a license that the EGMS at the licensed site are allowed to be playable for a configurable retention period.


### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each license hours override record. |
| zip | varchar | 10 | NOT NULL | - |
| DESCR | varchar | 100 | NOT NULL | Description of override reason. |
| end_datetime | timestamp | 8 | NOT NULL | The date and time of the override period end. |
| license_id | integer | 4 | NOT NULL | Unique identifier assigned to each License in the system. |
| start_datetime | timestamp | 8 | NOT NULL | The date and time of the override period start. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_gaming_hours_override_h_pk | id, audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** license_gaming_hours_h

**Description**

Contains the history of hours that the EGMS are allowed to be playable for an assigned license.  If no records exist for a license then egm, site and system hours will be used to get effective site hours  for a configurable retention period.



### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each license gaming hours record. |
| end_time | timestamp | 8 | NOT NULL | Time that the EGMs end operation.  1900-01-01-00.00.00 represents midnight.
 |
| weekday_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each weekday. |
| license_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| start_time | timestamp | 8 | NOT NULL | Time that the EGMs are operational.  1900-01-01-00.00.00 represents midnight. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_gaming_hours_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_addr_h

**Description**

Contains a history of site addresses for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| site_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to site address record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| addr_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each address type in the system. |
| addr_id | integer | 4 | NOT NULL | Unique identifier assigned to each Address. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_addr_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_entity_status_detail_h

**Description**

Table contains a history of site entity status details for a configurable retention period.

### Primary Key

**Primary Key Columns:** ID, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| ID | integer | 4 | NOT NULL | Unique identiifer assigned to each site_entity_status_detail record. |
| entity_status_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| site_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_entity_status_detail_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** user_news_message_h

**Description**

This table stores user news messages created for one or more VSCs.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Message ID. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| message | json | -2 | NOT NULL | Text of the message. |
| all_sites_flag | character | 1 | NOT NULL | - |
| AUDIT_USER_ID | integer | 4 | NOT NULL | GUI user identifier of who last updated record. |
| print_flag | character | 1 | NOT NULL | Flag that indicates if the message should be automatically printed/displayed on the Site Controller. |
| acknowledge_flag | character | 1 | NOT NULL | Flag to indicate if acknowledgment must be received before further action on the VSC is taken. |
| end_datetime | timestamp | 8 | NOT NULL | The end date of the message being available for the Site Controllers. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| start_datetime | timestamp | 8 | NOT NULL | The start date of the message being available for the Site Controllers. |
| priority_flag | character | 1 | NOT NULL | Flag to indicate if the message must be displayed at the top of the message list.  Messages are sorted by START_DATETIME. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the special message. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in special_msg_domain table. |

### Indexes

| Index Name | Columns |
|------------|---------|
| user_news_message_h_pk | id, audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** user_news_message_site_h

**Description**

This table stores user news messages assignments for the VSCs.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | GUI user identifier of who last updated record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Timestamp of when this record was updated. |
| user_news_message_id | integer | 4 | NOT NULL | Message ID. |
| site_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| id | integer | 4 | NOT NULL | - |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| user_news_message_site_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** system_parameter_h

**Description**

Table that contains the history of the system parameters tracked in the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each system parameter used in the application. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| entity_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity type. |
| DESCR | varchar | 100 | NOT NULL | System parameter key value description. |
| gui_editable_flag | character | 1 | NOT NULL | Flag to identify if the parameter is editable in the GUI. |
| numeric_parameter_flag | character | 1 | NOT NULL | Flag to identify if the parameter is numeric.    |
| default_value | varchar | 30 | NOT NULL | Default value for the parameter. |
| parameter_key | character | 50 | NOT NULL | System parameter key value to uniquely identify the parameter. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| system_parameter_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** trait_type_h

**Description**

Contains the history of the trait types used in the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| trait_generation_type_key_code | varchar | 50 | NULL | Unique identifier/code assigned to each trait generation type |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| entity_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity type. |
| trait_uniqueness_type_key_code | varchar | 50 | NULL | Unique identifier/code assigned to each trait uniqueness type. |
| trait_category_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each trait category. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to trait type in the system. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| descr | varchar | 100 | NOT NULL | JSON formatted document describing the internationalization for the description in the table.
JSON format:i18n : [locale : <iso639-1_language_code>,description : <localized_description_text>] |
| display_order | integer | 4 | NOT NULL | Display order of trait types. |
| i18n | varchar | 8192 | NULL | JSON formatted document describing the internationalization for the description in the table.
JSON format:i18n : [locale : <iso639-1_language_code>,description : <localized_description_text>] |
| parent_id | integer | 4 | NULL | Parent trait type. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_type_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_trait_h

**Description**

Contains the history of traits assigned to Sites for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site trait combination in the system. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| site_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| trait_id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_trait_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_trait_h

**Description**

Contains the history of the traits assigned to VSCs for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | - |
| trait_id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| vsc_id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC in the system. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_trait_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** egm_trait_h

**Description**

Contains the history of the traits assigned to EGMs for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| trait_id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each egm trait combination in the system. |
| egm_id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM in the system. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_trait_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** trait_h

**Description**

Contains the history of the traits used in the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |
| DESCR | varchar | 100 | NOT NULL | Description of the trait. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| source_entity_ref | integer | 4 | NULL | ID of the entity which resulted in this trait being generated; NULL for user generated traits.
 |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| trait_type_id | integer | 4 | NOT NULL | Unique identifier assigned to each trait type. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the trait. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in trait_domain table. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| parent_trait_id | integer | 4 | NULL | Parent trait id. |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_function_h

**Description**

This table stores historical data for the menu functions that are available on the VMT/VSC for a configurable retention period.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Internal identifier for VMT/VSC function. |
| DESCR | varchar | 100 | NOT NULL | VMT/VSC function description. |
| parent_id | integer | 4 | NULL | Internal identifier for VMT/VSC function. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_function_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** egm_sas_data_h

**Description**

Table holds the SAS specific data for SAS egms.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | - |
| card | smallint | 2 | NOT NULL | Card for the EGM. |
| cable | smallint | 2 | NOT NULL | Cable type for the EGM. |
| cpu_address | integer | 4 | NOT NULL | CPU Address. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_sas_data_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** egm_tracking_operation

**Description**

EGM operating hours stores the daily override/ weekly hours that computed based on hours in egm_gaming_hours and egm_gaming_hours_override for day and sent to the ilink.  This is calculated daily in EVO via a scheduled task and send to the iLINK if the hours have changed. It update as day at a time but sends all the 7 day data to the ilink.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each record in the table. |
| operation_datetime | timestamp | 8 | NOT NULL | Date and time that the EGM remove, move, replace or install took place. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each EGM tracking operation type in the system.
 |
| id | integer | 4 | NULL | The EGM being removed. moved or replaced in the system. |
| id | integer | 4 | NULL | The EGM replacing an EGM or the EGM being installed in the system. |
| id | integer | 4 | NULL | The VSC associated to the EGM being removed. moved or replaced in the system. |
| id | integer | 4 | NULL | The VSC associated to the EGM replacing an EGM or the EGM being installed in the system. |
| serial_number | varchar | 32 | NOT NULL | Serial number of the EGM being removed, moved, replaced  or installed.  For a replace operation, the serial_number is expected to remain the same. |
| comm_idn | varchar | 50 | NOT NULL | Communication identifier of the EGM being removed, moved, replaced  or installed. For a replace operation, the comm_idn is expected to remain the same.
 |
| old_position_number | integer | 4 | NULL | EGM position number prior to the operation performed (REMOVE, MOVE or REPLACE). |
| new_position_number | integer | 4 | NULL | EGM position number following the operation performed (MOVE, REPLACE or INSTALL). |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_tracking_operation_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| egm_tracking_operation_fk5 | egm_tracking_operation | egm_tracking_operation_type |
| egm_tracking_operation_fk4 | egm_tracking_operation | egm |
| egm_tracking_operation_fk3 | egm_tracking_operation | egm |
| egm_tracking_operation_fk2 | egm_tracking_operation | vsc |
| egm_tracking_operation_fk1 | egm_tracking_operation | vsc |

**Table Name:** egm_tracking_operation_type

**Description**

Contains the entity statuses used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each EGM tracking operation type in the system.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_tracking_operation_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_config_h

**Description**

Contains a history of the VSC configurations used in the application for a configurable retention period.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC configuration. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| idle_session_timer | integer | 4 | NOT NULL | Number of idle seconds after which the user is logged out. |
| DESCR | varchar | 100 | NOT NULL | Description of the VSC configuration. |
| rev_number | integer | 4 | NOT NULL | Revision number used to synchronize configuration changes. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| inactivity_timer | integer | 4 | NOT NULL | Number of seconds of inactivity by the user after which the screen saver will start.  |
| no_host_comm_timer | integer | 4 | NOT NULL | Seconds since site controller communicated with host after which the site will disable. |
| reasonability_check_flag | character | 1 | NOT NULL | Y/N Indicates whether reasonability checks will be performed. |
| config_refresh_timer | integer | 4 | NOT NULL | Interval in seconds after which site controller will check for configuration changes. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the vsc configuration. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in vsc_config_domain table. |
| vsc_hardware_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each VSC hardware type. |
| vsc_function_type_key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each VSC function type. |
| download_class_id | integer | 4 | NOT NULL | Unique identifier/code assigned to each download class.
 |
| minimum_card_number | integer | 4 | NOT NULL | This minimum parameter is needed in MTSC deployments. This parameter controls how many cards will be available for selection on SCs based on the values set in their assigned config profile. Jurisdictions have changed these values in the past to accommodate hardware changes.  |
| maximum_card_number | integer | 4 | NOT NULL | This maximum parameter is needed in MTSC deployments. This parameter controls how many cards will be available for selection on SCs based on the values set in their assigned config profile. Jurisdictions have changed these values in the past to accommodate hardware changes. 
 |
| minimum_cable_number | integer | 4 | NOT NULL | This minimum parameter is needed in MTSC deployments. This parameter controls how many cables will be available for selection on SCs based on the values set in their assigned config profile. Jurisdictions have changed these values in the past to accommodate hardware changes.  |
| maximum_cable_number | integer | 4 | NOT NULL | This maximum parameter is needed in MTSC deployments. This parameter controls how many cables will be available for selection on SCs based on the values set in their assigned config profile. Jurisdictions have changed these values in the past to accommodate hardware changes.  |
| validation_prompt_flag | character | 1 | NOT NULL | When set to 'Y', VSC users must provide a confirmation when validating tickets. |
| communication_offline_program_signature_check_flag | character | 1 | NOT NULL | A cyclic redundancy check on the system that must be applied using the start and end memory addresses of the software installed on the ROM Set. The EGM is not disabled to perform the check, but gets disabled if the check fails. This check is required by some jurisdictions like PA. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| adr_enabled_flag | character | 1 | NOT NULL | When set to 'Y', ADR is enabled. |
| log_file_enabled_flag | character | 1 | NOT NULL | When set to 'Y', log file is enabled. |
| screenshot_enabled_flag | character | 1 | NOT NULL | When set to 'Y', screenshot is enabled. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_config_h_pk | id, audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** adr_dvc_cfg_profile

**Description**

Contains the parameters that are associated to the ADR device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| adr_data_life_days | integer | 4 | NOT NULL | The number of days that the Accidental Data Recorder (ADR) data must be retained on the EGM before being deleted. |
| min_adr_data_entries | integer | 4 | NOT NULL | The minimum number of ADR Data Captures to retain before deleting the oldest ADR Data Capture, regardless of whether the data has been uploaded. |
| screenshot_life_days | integer | 4 | NOT NULL | The number of days that ScreenShots must be retained on the EGM before they can be deleted. |
| min_screenshot_entries | integer | 4 | NOT NULL | The minimum number of Screenshot captures to retain before deleting the oldest Screenshot Capture, regardless of whether the Screenshot has been uploaded. |

### Indexes

| Index Name | Columns |
|------------|---------|
| adr_dvc_cfg_profile_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| adr_dvc_cfg_profile_fk1 | adr_dvc_cfg_profile | cfg_profile |

**Table Name:** adr_dvc_cfg_profile_h

**Description**

Contains a history of the parameters that are associated to the ADR device configuration profile.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| adr_data_life_days | integer | 4 | NOT NULL | The number of days that the Accidental Data Recorder (ADR) data must be retained on the EGM before being deleted. |
| min_adr_data_entries | integer | 4 | NOT NULL | The minimum number of ADR Data Captures to retain before deleting the oldest ADR Data Capture, regardless of whether the data has been uploaded. |
| screenshot_life_days | integer | 4 | NOT NULL | The number of days that ScreenShots must be retained on the EGM before they can be deleted. |
| min_screenshot_entries | integer | 4 | NOT NULL | The minimum number of Screenshot captures to retain before deleting the oldest Screenshot Capture, regardless of whether the Screenshot has been uploaded. |

### Indexes

| Index Name | Columns |
|------------|---------|
| adr_dvc_cfg_profile_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** system_news_message_h

**Description**

Table to hold a history of the system news messages and site controller messages.

### Primary Key

**Primary Key Columns:** ID, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| ID | integer | 4 | NOT NULL | Unique identifier assigned to each system news message. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| message | json | -2 | NOT NULL | The messages.   Saved in i18n json format. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in system_news_message_domain table. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the system news message. |

### Indexes

| Index Name | Columns |
|------------|---------|
| system_news_message_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_message_domain

**Description**

Identifies which domains can use which vsc messages. VSC messages can be assigned to entities that have access to the same domains if the domain_access_list_flag in the special_msg table is set to 'Y'.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated trait. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the Traits access.   |
| id | integer | 4 | NOT NULL | Message ID. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_message_domain_pk | id |
| vsc_message_domain_i1 | domain_id, vsc_message_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_message_domain_fk1 | vsc_message_domain | vsc_message |

**Table Name:** user_news_message_domain_h

**Description**

Identifies a history of which domains can use which user news messages.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated trait. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the user news message access.   |
| user_news_message_id | integer | 4 | NOT NULL | Message ID. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| user_news_message_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** system_news_message_domain_h

**Description**

Identifies a history of which domains can use which system news messages.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated trait. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the user news message access.   |
| system_news_message_id | integer | 4 | NOT NULL | Message ID. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| system_news_message_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_message_acknowledgment

**Description**

This table stores vsc message acknowledgements. Once a VSC user acknowledges a message on the VSC, an entry is made in this table so that the message no longer needs to be displayed on the VSC.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC message acknowledgment record. |
| id | integer | 4 | NOT NULL | VSC that read and acknowledged the vsc message displayed on the VSC. |
| id | integer | 4 | NOT NULL | Message ID. |
| acknowledgment_user_id | integer | 4 | NOT NULL | VSC user that read and acknowledged the vsc message displayed on the VSC. |
| acknowledgment_datetime | timestamp | 8 | NOT NULL | Date and time that the user news message was acknowledged on the VSC by a VSC User. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_message_acknowledgment_uk1 | vsc_id, vsc_message_id |
| vsc_message_acknowledgment_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_message_ack_fk2 | vsc_message_acknowledgment | vsc |
| vsc_message_ack_fk1 | vsc_message_acknowledgment | vsc_message |

**Table Name:** vsc_message_h

**Description**

This table stores a history of vsc messages created for one or more site controllers.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vsc message. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| message | text | 2048 | NOT NULL | Text of the message. |
| all_sites_flag | character | 1 | NOT NULL | Indicates if the message should be displayed on all the site controllers.  If 'N', then a defined list of sites will exist in the vsc_message_site table. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | GUI user identifier of who last updated record. |
| print_at_site_flag | character | 1 | NOT NULL | Flag that indicates if the message should be automatically printed/displayed on the Site Controller. |
| acknowledgement_required_flag | character | 1 | NOT NULL | Flag to indicate if acknowledgment must be received before further action on the VSC is taken. |
| end_datetime | timestamp | 8 | NOT NULL | The end date of the message being available for the Site Controllers. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| start_datetime | timestamp | 8 | NOT NULL | The start date of the message being available for the Site Controllers. |
| priority_flag | character | 1 | NOT NULL | Flag to indicate if the message must be displayed at the top of the message list.  Messages are sorted by START_DATETIME. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the special message. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in special_msg_domain table. |
| name | varchar | 100 | NULL | Name of the message. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| subject | varchar | 100 | NOT NULL | Subject of the message. |
| recurrence_flag | character | 1 | NOT NULL | Identifies messages that should recurr on the site controller.  If the flag is 'Y' then the recurrence time, days of the week and end datetime will be used to know when the message should be displayed. |
| recurrence_time | time | 8 | NULL | Time that the message should recurr on the site controller when a recurring message. |
| recurrence_days_of_week | varchar | 200 | NULL | Contains a comma separated list of the days of the week. |
| recurrence_week_interval | integer | 4 | NULL | Used in conjunction with the days of the week selection(s) to control how often the acknowledgment required popup will reoccur on iLinks (when ack req is enabled and recurrence is set to yes). For example: This allows a message to be active for a period of time, and show the popup only every other week (instead of every week).

 |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_message_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_message_domain_h

**Description**

A history of which domains can use which vsc messages. VSC messages can be assigned to entities that have access to the same domains if the domain_access_list_flag in the special_msg table is set to 'Y'.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_id | integer | 4 | NOT NULL | Domain which is allowed to use the associated trait. |
| deleted_flag | character | 1 | NOT NULL | Identifies if the domain has been removed from the Traits access.   |
| vsc_message_id | integer | 4 | NOT NULL | Message ID. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_message_domain_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_message_site_h

**Description**

This table stores a history of vsc messages assignments for the sites.

### Primary Key

**Primary Key Columns:** AUDIT_DATETIME, id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | GUI user identifier of who last updated record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Timestamp of when this record was updated. |
| vsc_message_id | integer | 4 | NOT NULL | Message ID. |
| site_id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vsc_message_site. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_message_site_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** sru

**Description**

A Self Redemption Unit is a standalone, unattended device that is used to exchange Cashout Tickets/Vouchers for currency. 

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies an Self Redemption Unit in the System. |
| descr | varchar | 100 | NOT NULL | A User entered name to uniquely identify an SRU. |
| deleted_flag | char | 5 | NOT NULL | A Y/N flag indicating whether the Self Redemption Unit has been logically deleted in the System. |
| domain_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the domain in which this SRU belongs. When it is installed at a Venue, this will be the domain of the venue, when it is in the warehouse, it will be in the domain of the warehouse. |
| serial_number | varchar | 32 | NOT NULL | A value assigned to the SRU by the manufacturer to uniquely identify it. |
| asset_ref_number | varchar | 32 | NOT NULL | A value assigned by the Lottery to the SRU to uniquely identify it. |
| purchase_amount | decimal | 16 | NULL | The amount paid to purchase the Self-Redemption Unit. |
| purchase_date | date | 4 | NULL | The date on which the Self Redemption Unit was purchased. |
| key_code | varchar | 50 | NOT NULL | A value that uniquely identifies the status of the device to indicate it is enabled or disabled. |
| install_date | date | 4 | NULL | The date on which this SRU was installed on this VSC. |
| deinstall_date | date | 4 | NULL | The date on which this SRU was removed from this VSC. |
| id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the VSC in the system to which this SRU is connected.  This in turn will identify the site in which it is installed or the Warehouse in which it currently exists. |
| revision_number | integer | 4 | NOT NULL | An incremental number used to track changes on the SRU that requires an updated message to the Site Controller to keep it in sync with the host. |
| version_number | integer | 4 | NOT NULL | A number that uniquely identifies a version of the SRUt record. This is added to support optimistic locking, a strategy whereby the version is verified on update to ensure the record has not been updated since you retrieved it. |
| audit_user_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the User that last updated this record. |
| audit_datetime | timestamp | 8 | NOT NULL | The date and time that this record was last updated. |
| key_code | varchar | 50 | NOT NULL | A value that unqiuely identifies the protocol in which this SRU communicates. |
| id | integer | 4 | NOT NULL | System generated identifier that uniquely identifies the model of the SRU. |
| comm_idn | varchar | 50 | NOT NULL | A communication identifier used by the System to identify a valid SRU in the system. This is the value that is programmed into the back office of the SRU and must match the value configured for communication to be successful. |

### Indexes

| Index Name | Columns |
|------------|---------|
| sru_pk | id |
| sru_uk1 | descr |
| sru_uk2 | comm_idn |
| sru_uk3 | serial_number |
| sru_uk4 | asset_ref_number |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| sru_fk4 | sru | entity_status_type |
| sru_fk3 | sru | vsc |
| sru_fk2 | sru | sru_protocol_type |
| sru_fk1 | sru | model |

**Table Name:** qrtz_fired_triggers

**Description**

Provides status details of all jobs that have started execution via a specific trigger & schedule.

### Primary Key

**Primary Key Columns:** SCHED_NAME, ENTRY_ID

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance that owns the trigger. |
| ENTRY_ID | varchar | 95 | NOT NULL | A quartz supplied id for this record. |
| TRIGGER_NAME | varchar | 80 | NOT NULL | A User defined name that uniquely identifies the trigger within the schedule that has been fired. |
| TRIGGER_GROUP | varchar | 80 | NOT NULL | A User defined name for a trigger group. This can be useful for grouping and categorizing triggers, by allowing you to group triggers related to "reporting jobs" separately from those related to "maintenance jobs". |
| INSTANCE_NAME | varchar | 80 | NOT NULL | The name of the scheduler instance. |
| FIRED_TIME | bigint | 8 | NOT NULL | The date and time when this job was fired. |
| SCHED_TIME | bigint | 8 | NOT NULL | The date and time for when the next triggers are scheduled to fire. |
| PRIORITY | integer | 4 | NOT NULL | When you have many triggers, you may not have enough resources to immediately fire all of the triggers that are scheduled to fire at the same time. In this case, you may want to control which of your triggers get priority.  The triggers with the highest priority will be executed first.  If you do not set a prioirty, a default priority of 5 is assumed. |
| STATE | integer | 4 | NOT NULL | The state of the job (active, paused, ...). |
| JOB_NAME | varchar | 80 | NULL | A User defined name for the job that has been fired. |
| JOB_GROUP | varchar | 80 | NULL | A user defined name for a cluster group that is used to categorize and organize jobs into different groups. This is useful for managing and scheduling jobs that belong to specific categories such as "reporting jobs" or "maintenance jobs".  Each group must have a unique name to avoid conflicts. |
| IS_NONCONCURRENT | boolean | 1 | NULL | A boolean flag indicating whether a job should be executed concurrently or not.  This is useful for preventing multiple instances of the same job from executing at the same time, which can be important for maintaining data integrity and avoiding conflicts. |
| REQUESTS_RECOVERY | boolean | 1 | NULL | A boolean flag indicating whether the job should try to be re-executed in case of a recovery situation. |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_fired_triggers_pk | sched_name, entry_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** qrtz_calendars

**Description**

Stores non-standard calendars. Used for excluding blocks of time from the triggers firing schedule.  Calendars can block out sections of time as narrow as a millisecond but is most likely used for blocking-out entire days.

### Primary Key

**Primary Key Columns:** SCHED_NAME, CALENDAR_NAME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance that owns the calendar. |
| CALENDAR_NAME | varchar | 80 | NOT NULL | A User defined name of the calendar. |
| CALENDAR | bytea | 2048 | NOT NULL | This stores the calendar information as a binary large object (BLOB).  It holds the actual calendar data used by the triggers. |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_calendars_pk | calendar_name, sched_name |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** qrtz_paused_trigger_grps

**Description**

Provides paused trigger group information.

### Primary Key

**Primary Key Columns:** SCHED_NAME, TRIGGER_GROUP

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance that owns the trigger. |
| TRIGGER_GROUP | varchar | 80 | NOT NULL | A User defined name for a trigger group. This can be useful for grouping and categorizing triggers, by allowing you to group triggers related to "reporting jobs" separately from those related to "maintenance jobs". |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_paused_trigger_grps_pk | sched_name, trigger_group |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** qrtz_scheduler_state

**Description**

This table captures the node state so that if one node goes down or fails to executea job, the other instance running in the cluster can pick up the misfired job.

### Primary Key

**Primary Key Columns:** SCHED_NAME, INSTANCE_NAME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance. |
| INSTANCE_NAME | varchar | 80 | NOT NULL | The name of the scheduler instance. |
| LAST_CHECKIN_TIME | bigint | 8 | NOT NULL | The last check-in time in milliseconds for this record. |
| CHECKIN_INTERVAL | bigint | 8 | NOT NULL | The checkin interval in milliseconds. |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_scheduler_state_pk | sched_name, instance_name |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** qrtz_locks

**Description**

This table stores the value of the instance name executing the job, to avoid the scenario of multiple nodes executing the same job.

### Primary Key

**Primary Key Columns:** SCHED_NAME, LOCK_NAME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance. |
| LOCK_NAME | varchar | 40 | NOT NULL | The functional name of the lock. |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_locks_pk | sched_name, lock_name |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** qrtz_job_details

**Description**

This table stores detailed information for every configured Quartz job.

### Primary Key

**Primary Key Columns:** SCHED_NAME, JOB_NAME, JOB_GROUP

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance. |
| JOB_NAME | varchar | 80 | NOT NULL | A user defined name that uniquely identifies a job within a specific group. |
| JOB_GROUP | varchar | 80 | NOT NULL | A user defined name for a cluster group that is used to categorize and organize jobs into different groups. This is useful for managing and scheduling jobs that belong to specific categories such as "reporting jobs" or "maintenance jobs".  Each group must have a unique name to avoid conflicts. |
| DESCRIPTION | varchar | 128 | NULL | A User provided description or additional information about the job. |
| JOB_DATA | bytea | 2048 | NULL | An optional field where you can store additional data associated with the job. |
| JOB_CLASS_NAME | varchar | 128 | NOT NULL | The full package name of the implementation class. |
| IS_DURABLE | boolean | 1 | NOT NULL | A boolean flag indicating if the job is to be persisted. |
| is_nonconcurrent | boolean | 1 | NOT NULL | A boolean flag indicating whether a job should be executed concurrently or not.  This is useful for preventing multiple instances of the same job from executing at the same time, which can be important for maintaining data integrity and avoiding conflicts. |
| IS_UPDATE_DATA | boolean | 1 | NOT NULL | A boolean flag indicating whether the job_data associated with the Quartz job can be updated or not.  When the flag is true, the job data can be modified dynamically during runtime. Conversely, when false, the job data remains static and cannot be changed once the job is scheduled. |
| REQUESTS_RECOVERY | boolean | 1 | NOT NULL | A boolean flag indicating whether the job should try to be re-executed in case of a recovery situation. |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_job_details_pk | sched_name, job_name, job_group |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** qrtz_triggers

**Description**

Defines the schedule and trigger(s) upon which a given Job will be executed.

### Primary Key

**Primary Key Columns:** SCHED_NAME, TRIGGER_NAME, TRIGGER_GROUP

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance. |
| JOB_NAME | varchar | 80 | NOT NULL | A user defined name for the job that this trigger is associated to. |
| JOB_GROUP | varchar | 80 | NOT NULL | A user defined name for a cluster group that is used to categorize and organize jobs into different groups. This is useful for managing and scheduling jobs that belong to specific categories such as "reporting jobs" or "maintenance jobs".  Each group must have a unique name to avoid conflicts. |
| TRIGGER_NAME | varchar | 80 | NOT NULL | A User defined name that uniquely identifies each trigger within a specific group. |
| TRIGGER_GROUP | varchar | 80 | NOT NULL | A User defined name for a trigger group. This can be useful for grouping and categorizing triggers, by allowing you to group triggers related to "reporting jobs" separately from those related to "maintenance jobs". |
| DESCRIPTION | varchar | 120 | NULL | An optional description that allows the User to provide a readable description of the trigger.  This can be useful for documentation or for understanding the purpose of the trigger when reviewing the database. |
| NEXT_FIRE_TIME | bigint | 8 | NULL | The next time at which the trigger will fire. |
| PREV_FIRE_TIME | bigint | 8 | NULL | The last time the job was executed by the trigger. |
| PRIORITY | integer | 4 | NULL | When you have many triggers, you may not have enough resources to immediately fire all of the triggers that are scheduled to fire at the same time. In this case, you may want to control which of your triggers get priority.  The triggers with the highest priority will be executed first.  If you do not set a prioirty, a default priority of 5 is assumed. |
| TRIGGER_STATE | varchar | 16 | NOT NULL | The current state of the trigger. Possible values are Normal, Paused, Complete, Error, Blocked, None, Waiting. |
| TRIGGER_TYPE | varchar | 8 | NOT NULL | A value that identifies the type of trigger that will be used to scehdule this job. |
| START_TIME | bigint | 8 | NOT NULL | Defines when the trigger's schedule first comes into affect.  The value is a DateTimeOffset object that defines a moment in time on a given calendar date.  For some trigger types, the trigger will actually fire at the start time, for others it marks the time the schedule should start being followed.  |
| END_TIME | bigint | 8 | NULL | Defines when the trigger's schedule should no longer be in effect. For example, a trigger with a schedule of "every 5th day of the month" and with an end time of July 1st will fire for it's last time on June 5th. |
| CALENDAR_NAME | varchar | 80 | NULL | This identifies a calendar that is used to exclude blocks of time from the triggers firing schedule. For example, you could create a trigger that fires a job every weekday at 9:30AM, but then add a calendar that excludes all the business holidays. |
| MISFIRE_INST | smallint | 2 | NULL | Misfire Instructions.  A misfire occurs if a persistent trigger "misses" its firing time because of the scheduler being shutdown, or because there are no available threads for executing the job.  Different trigger types have different misfire instructions available to them.  When the scheduler starts, it searches for any persistent triggers that have misfired, and then it updates each of them based on the misfire instructions. |
| JOB_DATA | bytea | 2048 | NULL | This column stores additional data related to a job trigger. This is typically serialized data that can be used by the job when it is executed. |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_triggers_pk | sched_name, trigger_group, trigger_name |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| qrtz_triggers_fk1 | qrtz_triggers | qrtz_job_details |

**Table Name:** qrtz_blob_triggers

**Description**

Provides BLOB type trigger allowing users to create their own customized trigger types.

### Primary Key

**Primary Key Columns:** SCHED_NAME, TRIGGER_NAME, TRIGGER_GROUP

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| BLOB_DATA | bytea | 2048 | NULL | This column stores serialized objects in a binary large object (BLOB) format, typically representing the trigger's job data map, which includes various details and configurations related to the scheduled job. |
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance. |
| TRIGGER_NAME | varchar | 80 | NOT NULL | A User defined name that uniquely identifies each trigger within a specific group. |
| TRIGGER_GROUP | varchar | 80 | NOT NULL | A User defined name for a trigger group. This can be useful for grouping and categorizing triggers, by allowing you to group triggers related to "reporting jobs" separately from those related to "maintenance jobs". |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_blob_triggers_pk | sched_name, trigger_name, trigger_group |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| qrtz_blob_triggers_fk1 | qrtz_blob_triggers | qrtz_triggers |

**Table Name:** qrtz_simple_triggers

**Description**

Simple triggers are most useful for one-time firings or firing at an exact moment in time, with N repeats with a given delay between them.

### Primary Key

**Primary Key Columns:** SCHED_NAME, TRIGGER_NAME, TRIGGER_GROUP

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| REPEAT_COUNT | bigint | 8 | NOT NULL | Defines a specific number of times for the job to be run. |
| REPEAT_INTERVAL | bigint | 8 | NOT NULL | A positive value >= zero that represents the number of milliseconds delay between running the job. |
| TIMES_TRIGGERED | bigint | 8 | NOT NULL | A value that represents the number of times a particular job has been triggered.  It is used to keep track of how many times the trigger has fired since it was created. |
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance. |
| TRIGGER_NAME | varchar | 80 | NOT NULL | A User defined name that uniquely identifies each trigger within a specific group. |
| TRIGGER_GROUP | varchar | 80 | NOT NULL | A User defined name for a trigger group. This can be useful for grouping and categorizing triggers, by allowing you to group triggers related to "reporting jobs" separately from those related to "maintenance jobs". |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_simple_triggers_pk | sched_name, trigger_name, trigger_group |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| qrtz_simple_triggers_fk1 | qrtz_simple_triggers | qrtz_triggers |

**Table Name:** qrtz_simprop_triggers

**Description**

This table is used to manage various properties of simple triggers.

### Primary Key

**Primary Key Columns:** SCHED_NAME, TRIGGER_NAME, TRIGGER_GROUP

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| STR_PROP_1 | varchar | 512 | NULL | This column is used to store a string property associated with a simple trigger. |
| STR_PROP_2 | varchar | 512 | NULL | This column is used to store a string property associated with a simple trigger. |
| STR_PROP_3 | varchar | 512 | NULL | This column is used to store a string property associated with a simple trigger. |
| INT_PROP_1 | integer | 4 | NULL | This column is used to store an integer property associated with a simple trigger. |
| INT_PROP_2 | integer | 4 | NULL | This column is used to store an integer property associated with a simple trigger. |
| LONG_PROP_1 | bigint | 8 | NULL | This column is used to store a long property associated with a simple trigger. |
| LONG_PROP_2 | bigint | 8 | NULL | This column is used to store a long property associated with a simple trigger. |
| DEC_PROP_1 | decimal | 14 | NULL | This column is used to store a decimal property associated with a simple trigger. |
| DEC_PROP_2 | decimal | 14 | NULL | This column is used to store a decimal property associated with a simple trigger. |
| BOOL_PROP_2 | varchar | 1 | NULL | This column is used to store a boolean property associated with a simple trigger. |
| BOOL_PROP_1 | varchar | 1 | NULL | This column is used to store a boolean property associated with a simple trigger. |
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance. |
| TRIGGER_NAME | varchar | 80 | NOT NULL | A User defined name that uniquely identifies each trigger within a specific group. |
| TRIGGER_GROUP | varchar | 80 | NOT NULL | A User defined name for a trigger group. This can be useful for grouping and categorizing triggers, by allowing you to group triggers related to "reporting jobs" separately from those related to "maintenance jobs". |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_simprop_triggers_pk | sched_name, trigger_name, trigger_group |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| qrtz_simprop_triggers_fk1 | qrtz_simprop_triggers | qrtz_triggers |

**Table Name:** qrtz_cron_triggers

**Description**

Provides details of cron trigger for a specific job, allows for more complex scheduling based on calendar-like expressions, like time of day, day of week, day of month, and month of year.

### Primary Key

**Primary Key Columns:** SCHED_NAME, TRIGGER_NAME, TRIGGER_GROUP

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| CRON_EXPRESSION | varchar | 120 | NOT NULL | A string made up of seven sub-expressions, that describe individual details of the schedule. |
| TIME_ZONE_ID | varchar | 80 | NULL | The time zone associated with the trigger schedule. |
| SCHED_NAME | varchar | 120 | NOT NULL | A user defined name of the schedule that is used to uniquely identify the scheduler instance. |
| TRIGGER_NAME | varchar | 80 | NOT NULL | A User defined name that uniquely identifies each trigger within a specific group. |
| TRIGGER_GROUP | varchar | 80 | NOT NULL | A User defined name for a trigger group. This can be useful for grouping and categorizing triggers, by allowing you to group triggers related to "reporting jobs" separately from those related to "maintenance jobs". |

### Indexes

| Index Name | Columns |
|------------|---------|
| qrtz_cron_triggers_pk | sched_name, trigger_name, trigger_group |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| qrtz_cron_triggers_fk1 | qrtz_cron_triggers | qrtz_triggers |

**Table Name:** sru_protocol_type

**Description**

Look-up table for the protocol types supported for Self-Redemption Unit (SRU) devices.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | A value that uniquely identifies a protocol that is supported for Self-Redemption Units (SRUs). |

### Indexes

| Index Name | Columns |
|------------|---------|
| sru_protocol_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** sru_h

**Description**

A Self Redemption Unit is a standalone, unattended device that is used to exchange Cashout Tickets/Vouchers for currency. 

### Primary Key

**Primary Key Columns:** id, audit_datetime

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies an Self Redemption Unit in the System. |
| descr | varchar | 100 | NOT NULL | A User entered name to uniquely identify an SRU. |
| deleted_flag | char | 5 | NOT NULL | A Y/N flag indicating whether the Self Redemption Unit has been logically deleted in the System. |
| domain_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the domain in which this SRU belongs. When it is installed at a Venue, this will be the domain of the venue, when it is in the warehouse, it will be in the domain of the warehouse. |
| serial_number | varchar | 32 | NOT NULL | A value assigned to the SRU by the manufacturer to uniquely identify it. |
| asset_ref_number | varchar | 32 | NOT NULL | A value assigned to theSRU by the Lottery to uniquely identify it. |
| purchase_amount | decimal | 16 | NULL | The amount paid to purchase the Self-Redemption Unit. |
| purchase_date | date | 4 | NULL | The date on which the Self Redemption Unit was purchased. |
| entity_status_type_key_code | varchar | 50 | NOT NULL | A value that uniquely identifies the status of the device to indicate it is enabled or disabled. |
| install_date | date | 4 | NULL | The date on which this SRU was installed on this VSC. |
| deinstall_date | date | 4 | NULL | The date on which this SRU was removed from this VSC. |
| vsc_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the VSC in the system to which this SRU is connected.  This in turn will identify the site in which it is installed or the Warehouse in which it currently exists. |
| revision_number | integer | 4 | NOT NULL | An incremental number used to track changes on the SRU that requires an updated message to the Site Controller to keep it in sync with the host. |
| version_number | integer | 4 | NOT NULL | A number that uniquely identifies a version of the SRUt record. This is added to support optimistic locking, a strategy whereby the version is verified on update to ensure the record has not been updated since you retrieved it. |
| audit_user_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the User that last updated this record. |
| audit_datetime | timestamp | 8 | NOT NULL | The date and time that this record was last updated. |
| sru_protocol_type_key_code | varchar | 50 | NOT NULL | A value that uniquely identifies the protocol in which this SRU communicates. |
| model_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the model of the SRU. |
| comm_idn | varchar | 50 | NOT NULL | A communication identifier used by the System to identify a valid SRU in the system. This is the value that is programmed into the back office of the SRU and must match the value configured for communication to be successful. |
| audit_operation | char | 5 | NOT NULL | A single character to identify which operation on the sru table resulted in the insert of this record for historical tracking purposes. "I"nsert, "U"pdate, or "D"elete. |

### Indexes

| Index Name | Columns |
|------------|---------|
| sru_h_pk | audit_datetime, id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** sweep_zone

**Description**

-

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | - |
| version_number | integer | 4 | NOT NULL | - |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| name | varchar | 50 | NOT NULL | - |
| sweep_period_in_days | integer | 4 | NOT NULL | - |
| next_sweep_datetime | timestamp | 8 | NOT NULL | - |
| deleted_flag | char | 5 | NOT NULL | - |
| audit_user_id | integer | 4 | NOT NULL | - |
| audit_datetime | timestamp | 8 | NOT NULL | - |

### Indexes

| Index Name | Columns |
|------------|---------|
| sweep_zone_pk | id |
| sweep_zone_uk1 | site_id, name |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
|  | sweep_zone | site |

**Table Name:** publication_list

**Description**

Holds the tables that will be replicated by Debezium to the Datalake.

### Primary Key

**Primary Key Columns:** KEY_CODE

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| KEY_CODE | varchar | 256 | NOT NULL | Contains a table name that is part of the publication list for Debezium. |

### Indexes

| Index Name | Columns |
|------------|---------|
| publication_list_pk | table_name |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** entity_status_reason

**Description**

Contains the entity reason used in the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DESCR | varchar | 100 | NOT NULL | Entity reason description. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each entity reason tyoe. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| i18n | varchar | 8192 | NOT NULL | JSON formatted document describing the internationalization for the description in the table.
JSON format:i18n : [locale : <iso639-1_language_code>,description : <localized_description_text>] |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the entity status reason. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in <ENTITY>_domain table. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| entity_status_reason_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| entity_status_reason_fk1 | entity_status_reason | entity_status_type |

**Table Name:** download_class

**Description**

Contains the download classes managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier/code assigned to each download class.
 |
| descr | varchar | 100 | NOT NULL | Download class description. |
| bytes_per_second | integer | 4 | NOT NULL | Rate limit in bytes per second. |
| active_flag | character | 1 | NOT NULL | Identifies if the download class is enabled. |
| default_flag | character | 1 | NOT NULL | Identifies if the download class is the default download class. |

### Indexes

| Index Name | Columns |
|------------|---------|
| download_class_pk | id |
| download_class_uk1 | descr |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** entity_status_reason_domain

**Description**

An association of domains to which the entity reason is available for use. IF this table is empty, the domain_restricted_access_flag should be false indicating it is available to all domains for use.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | System generated identifier that uniquely identifies a domain associated to the adjustment reason.   |
| domain_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the domain in which this adjustment reason is available for use. |
| audit_datetime | timestamp | 8 | NOT NULL | That date and time that this record was last updated. |
| audit_user_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the user that last updated this record. |
| deleted_flag | char | 5 | NOT NULL | A Y/N flag indicating if the adjustment reason domain has been deleted. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each entity reason tyoe. |

### Indexes

| Index Name | Columns |
|------------|---------|
| entity_status_reason_domain_uk1 | entity_status_reason_id, domain_id |
| entity_status_reason_domain_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| entity_status_reason_domain_fk1 | entity_status_reason_domain | entity_status_reason |

**Table Name:** entity_status_reason_h

**Description**

Contains the entity reason used in the application.

### Primary Key

**Primary Key Columns:** id, AUDIT_DATETIME

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DESCR | varchar | 100 | NOT NULL | Entity reason description. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each entity reason tyoe. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| i18n | varchar | 8192 | NOT NULL | JSON formatted document describing the internationalization for the description in the table.
JSON format:i18n : [locale : <iso639-1_language_code>,description : <localized_description_text>] |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the entity status reason. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in <ENTITY>_domain table. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| entity_status_reason_h_pk | id, audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** entity_status_reason_domain_h

**Description**

An association of domains to which the entity reason is available for use. IF this table is empty, the domain_restricted_access_flag should be false indicating it is available to all domains for use.

### Primary Key

**Primary Key Columns:** id, audit_datetime

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | System generated identifier that uniquely identifies a domain associated to the adjustment reason.   |
| domain_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the domain in which this adjustment reason is available for use. |
| audit_datetime | timestamp | 8 | NOT NULL | That date and time that this record was last updated. |
| audit_user_id | integer | 4 | NOT NULL | A system generated identifier that uniquely identifies the user that last updated this record. |
| deleted_flag | char | 5 | NOT NULL | A Y/N flag indicating if the adjustment reason domain has been deleted. |
| entity_status_reason_id | integer | 4 | NOT NULL | Unique identifier assigned to each entity reason tyoe. |
| audit_operation | character | 1 | NOT NULL | Identifies whether the record was inserted (I), updated (U) or deleted (D). |

### Indexes

| Index Name | Columns |
|------------|---------|
| entity_status_reason_domain_h_pk | id, audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** license_gaming_hours_override

**Description**

Contains the override hours associated to a license that the EGMS at the licensed site are allowed to be playable.


### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each license hours override record. |
| zip | varchar | 10 | NOT NULL | - |
| DESCR | varchar | 100 | NOT NULL | Description of override reason. |
| end_datetime | timestamp | 8 | NOT NULL | The date and time of the override period end. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each License in the system. |
| start_datetime | timestamp | 8 | NOT NULL | The date and time of the override period start. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_gaming_hours_override_pk | id |
| license_gaming_hours_override_i1 | license_id, start_datetime, end_datetime |
| license_gaming_hours_override_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| license_gaming_hours_override_fk1 | license_gaming_hours_override | license |

**Table Name:** vsc_message_site

**Description**

This table stores vsc messages assignments for the sites.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | GUI user identifier of who last updated record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Timestamp of when this record was updated. |
| id | integer | 4 | NOT NULL | Message ID. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vsc_message_site. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_message_site_pk | id |
| vsc_message_site_i1 | audit_datetime |
| vsc_message_site_i2 | site_id, vsc_message_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_message_site_fk2 | vsc_message_site | site |
| vsc_message_site_fk1 | vsc_message_site | vsc_message |

**Table Name:** license_type

**Description**

Contains the license types used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each license type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_license

**Description**

Contains the site licenses managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each license in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| id | integer | 4 | NOT NULL | - |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_license_uk1 | site_id, license_id |
| site_license_i1 | license_id |
| site_license_pk | id |
| site_license_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| site_license_fk2 | site_license | site |
| site_license_fk1 | site_license | license |

**Table Name:** entity_type

**Description**

Contains the entity types used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| entity_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** trait_generation_type

**Description**

Contains the trait generation types used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each trait generation type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_generation_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** profile_group_type

**Description**

Table holds the profile group types to create logical groupings of profiles in the GUI.


### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each group profile type.
 |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each EGM protocol.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| profile_group_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| profile_group_type_fk1 | profile_group_type | egm_protocol_type |

**Table Name:** egm_profile_group

**Description**

Contains the synchronized and unsynchronized/in progress profile groups assigned to an EGM.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | - |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Profile Group assignment. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each profile group. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| key_code | varchar | 50 | NOT NULL | Unique identifier assigned to each profile group status type.   |
| configuration_start_datetime | timestamp | 8 | NULL | Date the device configuration started. |
| configuration_complete_datetime | timestamp | 8 | NULL | Date the device configuration completed. |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_profile_group_pk | id |
| egm_profile_group_uk1 | egm_id, profile_group_id, egm_profile_group_status_typ_key_code |
| egm_profile_group_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| EGM_PROFILE_GROUP_FK2 | egm_profile_group | egm |
| egm_profile_group_fk1 | egm_profile_group | profile_group |
| egm_profile_group_fk3 | egm_profile_group | egm_profile_group_status_type |

**Table Name:** profile_group_cfg_profile

**Description**

Table holds the logical grouping of profiles to facilitate grouping the profiles on the GUI.


### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | - |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each profile group. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each record that links profile groups and profiles. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| profile_group_cfg_profile_pk | id |
| profile_group_cfg_profile_uk1 | profile_group_id, cfg_profile_id |
| profile_group_cfg_profile_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| profile_group_cfg_profile_fk1 | profile_group_cfg_profile | profile_group |
| profile_group_cfg_profile_fk2 | profile_group_cfg_profile | cfg_profile |

**Table Name:** sas_dvc_cfg_profile

**Description**

SAS device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for the record. |
| protocol_version | integer | 4 | NULL | SAS EGM protocol version. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| sas_dvc_cfg_profile_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| sas_dvc_cfg_profile_fk2 | sas_dvc_cfg_profile | egm_protocol_revision_type |
| sas_dvc_cfg_profile_fk1 | sas_dvc_cfg_profile | cfg_profile |

**Table Name:** egm_protocol_revision_type

**Description**

Contains the EGM profile revision types used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for the record. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each EGM protocol.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_protocol_revision_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| egm_protocol_revision_type_fk1 | egm_protocol_revision_type | egm_protocol_type |

**Table Name:** egm_operating_hours

**Description**

EGM operating hours stores the daily override/ weekly hours that computed based on hours in egm_gaming_hours and egm_gaming_hours_override for day and sent to the ilink.  This is calculated daily in EVO via a scheduled task and send to the iLINK if the hours have changed. It update as day at a time but sends all the 7 day data to the ilink.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each record in the table. |
| id | integer | 4 | NOT NULL | - |
| start_time | timestamp | 8 | NOT NULL | Start Time of a period of time. |
| end_time | timestamp | 8 | NOT NULL | End Time of a period of time. |
| unix_start_time | integer | 4 | NOT NULL | Start time represented by unix time (number of seconds that have elapsed since midnight Coordinated Universal Time (UTC). |
| unix_end_time | integer | 4 | NOT NULL | End time represented by unix time (number of seconds that have elapsed since midnight Coordinated Universal Time (UTC). |
| close_all_day_flag | character | 1 | NOT NULL | Flag to indicate if the vlt will not be operating all day.  The default is 'N'. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each weekday.
 |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_operating_hours_pk | id |
| egm_operating_hours_uk1 | egm_id, weekday_type_key_code, start_time |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| egm_operating_hours_fk1 | egm_operating_hours | egm |
| egm_operating_hours_fk2 | egm_operating_hours | weekday_type |

**Table Name:** printer_dvc_cfg_profile

**Description**

Contains the parameters that are associated to the note acceptor device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| printer_dvc_cfg_profile_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| printer_dvc_cfg_profile_fk1 | printer_dvc_cfg_profile | cfg_profile |

**Table Name:** note_acceptor_note

**Description**

Lookup table for note acceptor notes.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DESCR | varchar | 100 | NOT NULL | Description of the note acceptor note. |
| number_of_base_units | decimal | 16 | NOT NULL | Amount applied to the players cashable amount for each note accepted. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each note acceptor note tracked in the application. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for the record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| note_acceptor_note_pk | id |
| note_acceptor_note_uk1 | descr |
| note_acceptor_note_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| note_acceptor_note_fk1 | note_acceptor_note | currency_type |

**Table Name:** contact_addr

**Description**

Contains the contact addresses managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each address in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each contact in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each contact address. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each address type in the system. |

### Indexes

| Index Name | Columns |
|------------|---------|
| contact_addr_i1 | addr_id, addr_type_key_code |
| contact_addr_pk | id |
| contact_addr_uk1 | contact_id, addr_id, addr_type_key_code |
| contact_addr_i3 | audit_datetime |
| contact_addr_i2 | addr_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| contact_addr_fk2 | contact_addr | contact |
| contact_addr_fk3 | contact_addr | addr_type |
| contact_addr_fk1 | contact_addr | addr |

**Table Name:** g2s_host_config_profile

**Description**

G2S Host configuration profile details.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each G2S Host Config Profile record. |
| can_modify_remote_flag | character | 1 | NOT NULL | Identifies if the host is remotely modifiable before changing some params for the host.  Default is ''Y''. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| can_modify_local_flag | character | 1 | NOT NULL | Identifies if the host is locally modifiable before changing some params for the host.  Default is 'N'. |
| authorized_host_flag | character | 1 | NOT NULL | Indicates whether it is an authorized host or not.  Default is 'N'. |
| display_communication_fault_flag | character | 1 | NOT NULL | Indicates whether a communications fault message should be displayed if the communications channel is unavailable. Default is 'Y'. |
| allow_multicast_flag | character | 1 | NOT NULL | Indicates whether the host is authorized to send multicast messages. Not required if hostRegistered is set to false.  Default is 'N'. |
| no_response_timer | integer | 4 | NOT NULL | The no-response timer used to determine whether the host has lost communications with another host.  Amount of time the host will wait for a response before the timeout logic is invoked.   |
| time_to_live_timer | integer | 4 | NOT NULL | Time-to-live value for requests originated by the host. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each G2S Host. |

### Indexes

| Index Name | Columns |
|------------|---------|
| g2s_host_config_profile_pk | id |
| g2s_host_config_profile_i1 | audit_datetime |
| g2s_host_config_profile_uk1 | g2s_host_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| G2S_HOST_CONFIG_PROFILE_FK1 | g2s_host_config_profile | g2s_host_type |

**Table Name:** g2s_host_type

**Description**

Contains the G2S Hosts applicable in GSM.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each G2S Host. |

### Indexes

No indexes found.

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_config_revision

**Description**

Manages the VSC revision numbers for each VSC.  Each time a revision changes that will affect the VSC, the GLOBAL_REVISION_NUMBER will get updated.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| system_revision_number | bigint | 8 | NOT NULL | Current system configuration block revision number. The revision number changes when affective changes are made to underlying system configuration tables.  |
| config_update_datetime | timestamp | 8 | NOT NULL | Date of the last configuration update on the VSC. |
| egm_list_revision_number | bigint | 8 | NOT NULL | EGM List revision number. |
| vsc_revision_number | bigint | 8 | NOT NULL | Current VSC configuration block revision number. The revision number changes when affective changes are made to underlying VSC configuration tables.  |
| site_revision_number | bigint | 8 | NOT NULL | Current site configuration block revision number. The revision number changes when affective changes are made to underlying site configuration tables.  |
| id | integer | 4 | NOT NULL | - |
| global_revision_number | bigint | 8 | NOT NULL | The VSC global revision number associated to the VSC. Will be recalculated (by GSM) as a result of any of the REVISION_NUMBER columns changing. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC configuration revision in the system. |
| sas_device_option_list_revision_number | bigint | 8 | NULL | The SAS Device option list revision number currently configured on the VSC. |
| g2s_comm_host_list_revision_number | bigint | 8 | NULL | The G2S Comm Host list revision number currently configured on the VSC. |
| g2s_device_option_list_revision_number | bigint | 8 | NULL | The G2S Device option list revision number currently configured on the VSC. |
| vsc_message_revision_number | bigint | 8 | NULL | Current vsc message revision number. The revision number changes when affective changes are made to the vsc message tables. |
| sru_list_revision_number | bigint | 8 | NULL | The current revision number for the sru list block. An increase in this revision number indicates for the Site Controller to request the configMsg for sruList block.  The revision number will be updated whenever the list or the data for one of the srus at the site changes, by either adding a new sru to the site or removing/ending an existing sru from the site. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_config_revision_uk1 | vsc_id |
| vsc_config_revision_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_config_revision_fk1 | vsc_config_revision | vsc |

**Table Name:** site_trait

**Description**

Contains the traits assigned to Sites.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site trait combination in the system. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_trait_uk1 | site_id, trait_id |
| site_trait_pk | id |
| site_trait_i1 | trait_id |
| site_trait_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| SITE_TRAIT_FK2 | site_trait | site |
| site_trait_fk1 | site_trait | trait |

**Table Name:** entity_status_type

**Description**

Contains the entity statuses used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| entity_status_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** site_type

**Description**

Contains the site types used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each site type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc

**Description**

Contains the VSCs (VLT site controllers) managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC in the system. |
| id | integer | 4 | NOT NULL | - |
| asset_ref_number | varchar | 32 | NULL | Customer assigned asset number. |
| serial_number | varchar | 32 | NOT NULL | VSC Serial number. |
| comm_idn | varchar | 50 | NOT NULL | Network Id for Site Controller. Legacy CLIENT_ID from ESConnect. |
| comm_active_flag | character | 1 | NOT NULL | Flag to identify whether the VSC communications are active ot not.  Default is N. |
| install_date | timestamp | 8 | NULL | Date on which the VSC was installed. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | - |
| purchase_date | timestamp | 8 | NULL | Date on which the VSC was purchased. |
| REVISION_NUMBER | bigint | 8 | NOT NULL | Revision number used to synchronize configuration changes. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if the entity has been logically deleted. Default is N. |
| ip_addr | varchar | 15 | NULL | VSC IP address. |
| DESCR | varchar | 100 | NOT NULL | Description of the VSC. |
| deinstall_date | timestamp | 8 | NULL | Date on which the VSC is deinstalled.  If null then still installed. |
| domain_id | integer | 4 | NOT NULL | System generated identifier that uniquely identifies the domain that is associated to the site where this vsc is installed. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_uk1 | descr |
| vsc_i4 | serial_number |
| vsc_i2 | ip_addr |
| vsc_i3 | comm_idn |
| vsc_i1 | site_id |
| vsc_i5 | asset_ref_number |
| vsc_pk | id |
| vsc_i6 | audit_datetime |
| vsc_i7 | vsc_config_id |
| vsc_i9 | deleted_flag |
| vsc_i8 | entity_status_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_fk1 | vsc | site |
| vsc_fk2 | vsc | vsc_config |
| vsc_fk3 | vsc | entity_status_type |

**Table Name:** vendor

**Description**

Contains the vendors managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vendor. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| DESCR | varchar | 100 | NOT NULL | Vendor description. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| owner_domain_id | integer | 4 | NULL | The domain that generated or updated the vendor. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access by domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in VENDOR_DOMAIN table. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| key_code | varchar | 50 | NOT NULL | A value that uniquely identifies the entity type supplied by this vendor. Ex EGM, SRU. |
| manufacturer_code | varchar | 3 | NULL | Manfacturer code associated to the vendor. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vendor_pk | id |
| vendor_i1 | audit_datetime |
| vendor_uk1 | descr, entity_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vendor_fk1 | vendor | entity_type |

**Table Name:** egm_trait

**Description**

Contains the traits assigned to EGMs.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each egm trait combination in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM in the system. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_trait_uk1 | egm_id, trait_id |
| egm_trait_pk | id |
| egm_trait_i1 | trait_id |
| egm_trait_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| egm_trait_fk1 | egm_trait | trait |
| EGM_TRAIT_FK2 | egm_trait | egm |

**Table Name:** system_parameter

**Description**

Table that contains the system parameters.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each system parameter used in the application. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| DESCR | varchar | 100 | NOT NULL | System parameter key value description. |
| gui_editable_flag | character | 1 | NOT NULL | Flag to identify if the parameter is editable in the GUI. |
| numeric_parameter_flag | character | 1 | NOT NULL | Flag to identify if the parameter is numeric.    |
| default_value | varchar | 30 | NOT NULL | Default value for the parameter. |
| parameter_key | character | 50 | NOT NULL | System parameter key value to uniquely identify the parameter. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| system_parameter_uk1 | parameter_key |
| system_parameter_pk | id |
| system_parameter_i1 | entity_type_key_code |
| system_parameter_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| system_parameter_fk1 | system_parameter | entity_type |

**Table Name:** auto_cashout_behaviour_type

**Description**

Lookup table for Auto Cashout Behaviour codes.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code  assigned to each Auto Cashout Behaviours. |

### Indexes

| Index Name | Columns |
|------------|---------|
| auto_cashout_behaviour_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** locale_type

**Description**

Lookup table for locales.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for each locale type. |
| country_code | character | 2 | NOT NULL | Locale language code. |
| language_code | character | 2 | NOT NULL | Locale language code. |

### Indexes

| Index Name | Columns |
|------------|---------|
| locale_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** currency_type

**Description**

Lookup table for currencies used in the system.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each currency tracked in the system. |

### Indexes

| Index Name | Columns |
|------------|---------|
| currency_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_config_revision_log

**Description**

Contains a history of the VSC configuration revisions.  Records are created in this table when data is sent back from the VSC.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| system_revision_number | bigint | 8 | NOT NULL | Current system configuration block revision number. |
| global_revision_number | bigint | 8 | NOT NULL | The VSC global revision number assigned to the VSC. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC configuration revision in the system. |
| config_update_datetime | timestamp | 8 | NOT NULL | Configuration update on the VSC. |
| sas_device_option_list_revision_number | bigint | 8 | NULL | The SAS Device option list revision number currently configured on the VSC. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC in the system. |
| g2s_comm_host_list_revision_number | bigint | 8 | NULL | The G2S Comm Host list revision number currently configured on the VSC. |
| g2s_device_option_list_revision_number | bigint | 8 | NULL | The G2S Device option list revision number currently configured on the VSC. |
| egm_revision_number | bigint | 8 | NOT NULL | EGM List revision number. |
| vsc_revision_number | bigint | 8 | NOT NULL | Current VSC configuration block revision number. |
| site_revision_number | bigint | 8 | NOT NULL | Current site configuration block revision number. |
| sru_list_revision_number | bigint | 8 | NULL | The current revision number for the sru list block. An increase in this revision number indicates for the Site Controller to request the configMsg for sruList block.  The revision number will be updated whenever the list or the data for one of the srus at the site changes, by either adding a new sru to the site or removing/ending an existing sru from the site. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_config_revision_log_pk | id |
| vsc_config_revision_log_uk1 | vsc_id, config_update_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_config_revision_log_fk1 | vsc_config_revision_log | vsc |

**Table Name:** voucher_dvc_cfg_profile

**Description**

Contains the parameters that are associated to the voucher device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| validation_id_list_refresh_timer | bigint | 8 | NULL | A timer is reset to the value each time EGM receives a  validationData command.  The default is 12 hours.  If the timer expires, EGM must send getValidationData command. |
| cash_promo_expiration_period | integer | 4 | NOT NULL | Number of days before cashable promo vouchers expire. |
| min_number_validation_ids | integer | 4 | NULL | Minimum number of validation identifiers that the EGM should have at all times. |
| validation_id_list_life_timer | bigint | 8 | NULL | A timer is reset to the value each time the EGM receives a  validationData command.  The default is 24 hours.  If the timer expires, validation identifiers may not be used. |
| print_offline_flag | character | 1 | NOT NULL | Allows vouchers to be printed while the host is offline. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| max_number_validation_ids | integer | 4 | NULL | Maximum number of validation identifiers that the EGM may buffer. |
| time_to_live_timer | integer | 4 | NULL | Time-to-live value for requests originated by the device. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| voucher_dvc_cfg_profile_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| voucher_dvc_cfg_profile_fk1 | voucher_dvc_cfg_profile | cfg_profile |

**Table Name:** cfg_profile_type

**Description**

Contains the configuration profile types used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each configuration profile type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| cfg_profile_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** note_acceptor_dvc_cfg_profile

**Description**

Contains the parameters that are associated to the note acceptor device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| voucher_enabled_flag | character | 1 | NOT NULL | Indicates whether the device should accept any vouchers. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| host_authorize_notes_flag | character | 1 | NOT NULL | Indicates whether EGM must seek authorization from a host in order to redeem each note inserted. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| time_to_live_timer | integer | 4 | NULL | Time-to-live value for requests originated by the device. |
| no_response_timer | integer | 4 | NULL | Amount of time a device will wait for a response before the timeout logic is invoked. |
| note_enabled_flag | character | 1 | NOT NULL | Indicates whether the device should accept any notes. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| note_acceptor_dvc_cfg_profile_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| note_acceptor_dvc_cfg_profile_fk1 | note_acceptor_dvc_cfg_profile | cfg_profile |

**Table Name:** gaming_hours_profile

**Description**

Contains the gaming hour profiles used in the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each gaming hours profile. |
| DESCR | varchar | 100 | NOT NULL | Description of the gaming hours profile. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the gaming hours profile. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in gaming_hours_profile_domain table. |
| external_id | varchar | 16 | NULL | Captures id from legacy system during data conversion. |

### Indexes

| Index Name | Columns |
|------------|---------|
| gaming_hours_profile_uk1 | descr |
| gaming_hours_profile_pk | id |
| gaming_hours_profile_i1 | audit_datetime |
| gaming_hours_profile_uk2 | external_id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** profile_group_domain

**Description**

Identifies the domains that are accessible by which profile groups.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each configuration profile domain record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| domain_id | integer | 4 | NOT NULL | Unique identifier assigned to each domain.  The domain in this table will represent jurisdictions. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NULL | Unique identifier assigned to each profile group. |

### Indexes

| Index Name | Columns |
|------------|---------|
| profile_group_domain_pk | id |
| profile_group_domain_uk1 | profile_group_id, domain_id |
| profile_group_domain_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| profile_group_domain_fk1 | profile_group_domain | profile_group |

**Table Name:** egm

**Description**

Contains the EGMs managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DESCR | varchar | 100 | NOT NULL | Description of the EGM. |
| ip_addr | character | 15 | NULL | EGM IP Address. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM in the system. |
| REVISION_NUMBER | bigint | 8 | NOT NULL | Revision number used to synchronize configuration changes. |
| position_number | integer | 4 | NOT NULL | EGM position number. |
| comm_idn | varchar | 50 | NOT NULL | Network Id for EGM. Legacy CLIENT_ID, ie: IGT_00010010
. |
| install_date | timestamp | 8 | NOT NULL | Date on which the EGM was installled. |
| purchase_amount | decimal | 16 | NULL | Purchase amount of the EGM. |
| asset_ref_number | varchar | 32 | NOT NULL | Customer assigned asset number. |
| deinstall_date | timestamp | 8 | NULL | Date on which the EGM was uninstalled. NULL if EGM still installed. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each model. |
| serial_number | varchar | 32 | NOT NULL | EGM serial number. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| purchase_date | timestamp | 8 | NULL | Date on which the EGM was purchased. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to a VSC. |
| invoice_enabled_flag | character | 1 | NOT NULL | Flag to identify if tito is enabled on the egm. Default is Y. Site also has to be invoice enabled for the egms to be included in the invoice. |
| domain_id | integer | 4 | NOT NULL | System generated identifier that uniquely identifies the domain that is associated to the site where this egm is installed.  |
| id | integer | 4 | NULL | Unique identifier assigned to each EGM Gaming Hours Profile. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system.
 |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each EGM protocol.
 |
| id | integer | 4 | NULL | - |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_i2 | ip_addr |
| egm_i3 | comm_idn |
| egm_i4 | serial_number |
| egm_i1 | deleted_flag |
| egm_i5 | asset_ref_number |
| egm_pk | id |
| egm_i6 | audit_datetime |
| egm_i7 | vsc_id |
| egm_i8 | model_id |
| egm_i9 | entity_status_type_key_code |
| egm_i10 | egm_gaming_hours_profile_id |
| egm_i11 | egm_protocol_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
|  | egm | sweep_zone |
| egm_fk3 | egm | entity_status_type |
| egm_fk5 | egm | egm_protocol_type |
| egm_fk1 | egm | vsc |
| egm_fk4 | egm | model |
| egm_fk2 | egm | egm_gaming_hours_profile |

**Table Name:** site_addr

**Description**

Contains the addresses for each site.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to site address record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each Address. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each address type in the system. |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_addr_pk | id |
| site_addr_i1 | addr_id, addr_type_key_code |
| site_addr_uk1 | site_id, addr_id, addr_type_key_code |
| site_addr_i3 | audit_datetime |
| site_addr_i2 | addr_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| site_addr_fk1 | site_addr | site |
| site_addr_fk3 | site_addr | addr_type |
| site_addr_fk2 | site_addr | addr |

**Table Name:** DOMAIN

**Description**

Defines the different domains that exist within the system. Domains are used to isolate service instance clusters such that Users can be given different access levels per cluster.

### Primary Key

**Primary Key Columns:** ID

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| IDENTITY_PROVIDERS | varchar | 4096 | NULL | JSON-formatted document describing the Entity Providers used to authenticate users when this domain is specified.  |
| I18N | varchar | 8192 | NULL | JSON formatted document describing the internationalization for the domain.  
JSON format:

i18n : [

locale : <iso639-1_language_code>,
name : <localized_name>,
description : <localized_description>

]

 |
| LOCALES | varchar | 4096 | NULL | JSON-formatted document identifying the locales supported by this domain. |
| SERVICES | varchar | 4096 | NULL | JSON formatted document identifying the services that are unavailable tothis domain. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| ID | integer | 4 | NULL | - |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| ID | integer | 4 | NOT NULL | - |

### Indexes

| Index Name | Columns |
|------------|---------|
| DOMAIN_PK | ID |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| DOMAIN_FK1 | DOMAIN | DOMAIN |

**Table Name:** system_gaming_hours_override

**Description**

Contains the override hours that the EGMS are allowed to be playable.


### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each system gaming hours override record. |
| end_datetime | timestamp | 8 | NOT NULL | The date and time of the override period end. |
| DESCR | varchar | 100 | NOT NULL | Description of override reason. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each gaming hours profile. |
| start_datetime | timestamp | 8 | NOT NULL | The date and time of the override period start. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |

### Indexes

| Index Name | Columns |
|------------|---------|
| system_gaming_hours_override_i1 | gaming_hours_profile_id, start_datetime, end_datetime |
| system_gaming_hours_override_pk | id |
| system_gaming_hours_override_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| system_gaming_hours_override_fk1 | system_gaming_hours_override | gaming_hours_profile |

**Table Name:** weekday_type

**Description**

Contains the weekdays used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each weekday.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| weekday_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** addr_type

**Description**

Contains the address types used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each address type in the system. |

### Indexes

| Index Name | Columns |
|------------|---------|
| addr_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** time_zone_type

**Description**

Contains the time zones used by the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each time zone type. |
| offset_seconds | integer | 4 | NOT NULL | Offset for the time zone in seconds. |

### Indexes

| Index Name | Columns |
|------------|---------|
| time_zone_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** profile_group

**Description**

Table holds the logical grouping of configurations to facilitate grouping profiles on the GUI.


### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each profile group. |
| descr | varchar | 100 | NOT NULL | Description of the profile group. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in profile_group_domain table. |
| owner_domain_id | integer | 4 | NULL | The domain that generated or updated the profile group. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each group profile type.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| profile_group_pk | id |
| profile_group_uk1 | descr, profile_group_type_key_code |
| profile_group_i2 | audit_datetime |
| profile_group_i1 | profile_group_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| profile_group_fk1 | profile_group | profile_group_type |

**Table Name:** egm_sas_data

**Description**

Table holds the SAS specific data for SAS egms.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | - |
| card | smallint | 2 | NOT NULL | Card for the EGM. |
| cable | smallint | 2 | NOT NULL | Cable type for the EGM. |
| cpu_address | integer | 4 | NOT NULL | CPU Address. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_sas_data_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| egm_sas_data_fk1 | egm_sas_data | egm |

**Table Name:** contact

**Description**

Contains the contacts managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each contact in the system. |
| phone_number_backup | varchar | 24 | NULL | Contact backup phone number. |
| phone_number | varchar | 24 | NULL | Contact primary phone number. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| last_name | varchar | 50 | NOT NULL | Last name of contact. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| middle_name | varchar | 50 | NULL | Middle name of contact. |
| fax_number | varchar | 24 | NULL | Contact fax number. |
| first_name | varchar | 50 | NOT NULL | First name of contact. |
| email_addr | varchar | 100 | NULL | Contact email address. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |

### Indexes

| Index Name | Columns |
|------------|---------|
| contact_pk | id |
| contact_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** trait_category_type

**Description**

Contains the trait categories used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each trait category. |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_category_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** trait

**Description**

Contains the traits used in the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |
| DESCR | varchar | 100 | NOT NULL | Description of the trait. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| source_entity_ref | integer | 4 | NULL | ID of the entity which resulted in this trait being generated; NULL for user generated traits.
 |
| id | integer | 4 | NULL | Parent trait id. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait type. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the trait. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in trait_domain table. |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_pk | id |
| trait_i1 | trait_type_id |
| trait_i2 | parent_trait_id |
| trait_i3 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| trait_fk2 | trait | trait |
| trait_fk1 | trait | trait_type |

**Table Name:** trait_type

**Description**

Contains the trait types used in the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NULL | Parent trait type. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to trait type in the system. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| descr | varchar | 100 | NOT NULL | JSON formatted document describing the internationalization for the description in the table.
JSON format:i18n : [locale : <iso639-1_language_code>,description : <localized_description_text>] |
| display_order | integer | 4 | NOT NULL | Display order of trait types. |
| i18n | varchar | 8192 | NULL | JSON formatted document describing the internationalization for the description in the table.
JSON format:i18n : [locale : <iso639-1_language_code>,description : <localized_description_text>] |
| key_code | varchar | 50 | NULL | Unique identifier/code assigned to each trait generation type. |
| key_code | varchar | 50 | NULL | Unique identifier/code assigned to each trait uniqueness type. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each trait category. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_type_pk | id |
| trait_type_i3 | parent_id |
| trait_type_i4 | audit_datetime |
| trait_type_i2 | trait_category_type_key_code |
| trait_type_i1 | entity_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| trait_type_fk1 | trait_type | entity_type |
| trait_type_fk4 | trait_type | trait_generation_type |
| trait_type_fk3 | trait_type | trait_type |
| trait_type_fk2 | trait_type | trait_category_type |
| trait_type_fk5 | trait_type | trait_uniqueness_type |

**Table Name:** system_gaming_hours

**Description**

Contains the hours that the EGMS are allowed to be playable.


### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each gaming hours profile. |
| start_time | timestamp | 8 | NOT NULL | Time that the EGMs are operational.  1900-01-01-00.00.00 represents midnight. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| end_time | timestamp | 8 | NOT NULL | Time that the EGMs end operation.  1900-01-01-00.00.00 represents midnight.
 |
| id | integer | 4 | NOT NULL | - |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each weekday.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| system_gaming_hours_uk1 | gaming_hours_profile_id, weekday_type_key_code, start_time |
| system_gaming_hours_pk | id |
| system_gaming_hours_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| system_gaming_hours_fk2 | system_gaming_hours | weekday_type |
| system_gaming_hours_fk1 | system_gaming_hours | gaming_hours_profile |

**Table Name:** vsc_function_type

**Description**

Contains the VSC functions types managed by the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each VSC function type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_function_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** accept_non_cash_amount_type

**Description**

Lookup table for what types of non cash amounts to accept.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each non cash amount. |

### Indexes

| Index Name | Columns |
|------------|---------|
| accept_non_cash_amount_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** cfg_profile

**Description**

Table holds the defined device configuration profiles used in the system.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| DESCR | varchar | 100 | NOT NULL | Description of the configuration profile. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| revision_number | bigint | 8 | NOT NULL | This revision number will hold the true revision of the configuration profile.  It will not be used for locking.  Implemented to accommodate they way in which configuration profiles are being updated. |
| allow_update_cfg_profile_flag | character | 1 | NOT NULL | Indicates whether the default profile is updateable. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each configuration profile type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| cfg_profile_uk1 | descr, cfg_profile_type_key_code |
| cfg_profile_pk | id |
| cfg_profile_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| cfg_profile_fk1 | cfg_profile | cfg_profile_type |

**Table Name:** site

**Description**

Contains the sites managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| ref_number | varchar | 6 | NOT NULL | Unique site number assigned to each site. |
| DESCR | varchar | 100 | NOT NULL | Description of the site. |
| REVISION_NUMBER | bigint | 8 | NOT NULL | Revision number used to synchronize configuration changes. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| domain_id | integer | 4 | NOT NULL | - |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| cross_valid_all_flag | character | 1 | NOT NULL | Identifies if the site can validate tickets from any other site. |
| cross_valid_chain_flag | character | 1 | NOT NULL | Identifies if the site can validate tickets from another site belonging to the same chain (aka company). |
| tito_enabled_flag | character | 1 | NOT NULL | Flag to identify if tito is enabled on the site. Default is N. |
| invoice_enabled_flag | character | 1 | NOT NULL | Flag to identify if invoicing is enabled on the site. Default is N. |
| cashout_header_use_gaming_site_name_flag | character | 1 | NOT NULL | Indicates if the cashout ticket header should use the gaming site name as the ticket header. |
| cashout_header_use_gaming_site_address_flag | character | 1 | NOT NULL | Indicates if the cashout ticket header should use the gaming site address as the ticket header. |
| activation_date | timestamp | 8 | NULL | Date on which the site was activated.  If null then site still not active. |
| deactivation_date | timestamp | 8 | NULL | Date on which the site was deactivated.  If null then site still active. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each time zone type. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each site type. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each entity status in the system.
 |
| id | integer | 4 | NULL | Unique identifier assigned to each entity reason tyoe. |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_i3 | domain_id |
| site_pk | id |
| site_uk1 | descr |
| site_i4 | audit_datetime |
| site_i1 | site_type_key_code |
| site_i2 | entity_status_type_key_code |
| site_i5 | time_zone_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| site_fk4 | site | entity_status_reason |
| site_fk1 | site | entity_status_type |
| site_fk3 | site | time_zone_type |
| site_fk2 | site | site_type |

**Table Name:** vsc_hardware_type

**Description**

Contains the VSC hardware types managed by the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for the record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_hardware_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_config

**Description**

Contains the VSC configurations used in the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC configuration. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| idle_session_timer | integer | 4 | NOT NULL | Number of idle seconds after which the user is logged out. |
| DESCR | varchar | 100 | NOT NULL | Description of the VSC configuration. |
| rev_number | integer | 4 | NOT NULL | Revision number used to synchronize configuration changes. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| inactivity_timer | integer | 4 | NOT NULL | Number of seconds of inactivity by the user after which the screen saver will start.  |
| no_host_comm_timer | integer | 4 | NOT NULL | Seconds since site controller communicated with host after which the site will disable. |
| reasonability_check_flag | character | 1 | NOT NULL | Y/N Indicates whether reasonability checks will be performed. |
| config_refresh_timer | integer | 4 | NOT NULL | Interval in seconds after which site controller will check for configuration changes. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the vsc configuration. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in vsc_config_domain table. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each VSC hardware type. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each VSC function type. |
| minimum_card_number | integer | 4 | NOT NULL | This minimum parameter is needed in MTSC deployments. This parameter controls how many cards will be available for selection on SCs based on the values set in their assigned config profile. Jurisdictions have changed these values in the past to accommodate hardware changes.  |
| maximum_card_number | integer | 4 | NOT NULL | This maximum parameter is needed in MTSC deployments. This parameter controls how many cards will be available for selection on SCs based on the values set in their assigned config profile. Jurisdictions have changed these values in the past to accommodate hardware changes. 
 |
| minimum_cable_number | integer | 4 | NOT NULL | This minimum parameter is needed in MTSC deployments. This parameter controls how many cables will be available for selection on SCs based on the values set in their assigned config profile. Jurisdictions have changed these values in the past to accommodate hardware changes.  |
| maximum_cable_number | integer | 4 | NOT NULL | This maximum parameter is needed in MTSC deployments. This parameter controls how many cables will be available for selection on SCs based on the values set in their assigned config profile. Jurisdictions have changed these values in the past to accommodate hardware changes.  |
| validation_prompt_flag | character | 1 | NOT NULL | When set to 'Y', VSC users must provide a confirmation when validating tickets. |
| communication_offline_program_signature_check_flag | character | 1 | NOT NULL | A cyclic redundancy check on the system that must be applied using the start and end memory addresses of the software installed on the ROM Set. The EGM is not disabled to perform the check, but gets disabled if the check fails. This check is required by some jurisdictions like PA. |
| adr_enabled_flag | character | 1 | NOT NULL | When set to 'Y', ADR is enabled. |
| log_file_enabled_flag | character | 1 | NOT NULL | When set to 'Y', log file is enabled. |
| screenshot_enabled_flag | character | 1 | NOT NULL | When set to 'Y', screenshot is enabled. |
| read_only_flag | character | 1 | NOT NULL | When set to 'Y', the VSC configuration data is read only and cannot be edited. |
| id | integer | 4 | NOT NULL | Unique identifier/code assigned to each download class.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_config_pk | id |
| vsc_config_uk1 | descr |
| vsc_config_i4 | audit_datetime |
| vsc_config_i2 | vsc_hardware_type_key_code |
| vsc_config_i1 | vsc_function_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_config_fk3 | vsc_config | download_class |
| vsc_config_fk1 | vsc_config | vsc_function_type |
| vsc_config_fk2 | vsc_config | vsc_hardware_type |

**Table Name:** addr

**Description**

Contains the addresses managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| zip | varchar | 25 | NOT NULL | Postal or Zip code. |
| line2 | varchar | 100 | NULL | Second Line of an Address. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| po_box | varchar | 10 | NULL | Postal office box number. |
| city | varchar | 30 | NOT NULL | City. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each Address. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| line1 | varchar | 100 | NOT NULL | First Line of an Address. |
| state | varchar | 25 | NOT NULL | State or Province. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |

### Indexes

| Index Name | Columns |
|------------|---------|
| addr_i3 | zip |
| addr_i2 | state, zip |
| addr_i1 | state, city, zip |
| addr_pk | id |
| addr_i4 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_message

**Description**

This table stores vsc messages created for one or more site controllers.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vsc message. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| message | text | 2048 | NOT NULL | Text of the message. |
| all_sites_flag | character | 1 | NOT NULL | Indicates if the message should be displayed on all the site controllers.  If 'N', then a defined list of sites will exist in the vsc_message_site table. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | GUI user identifier of who last updated record. |
| print_at_site_flag | character | 1 | NOT NULL | Flag that indicates if the message should be automatically printed/displayed on the Site Controller. |
| acknowledgement_required_flag | character | 1 | NOT NULL | Flag to indicate if acknowledgment must be received before further action on the VSC is taken. |
| end_datetime | timestamp | 8 | NOT NULL | The end date of the message being available for the Site Controllers. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| start_datetime | timestamp | 8 | NOT NULL | The start date of the message being available for the Site Controllers. |
| priority_flag | character | 1 | NOT NULL | Flag to indicate if the message must be displayed at the top of the message list.  Messages are sorted by START_DATETIME. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the special message. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in special_msg_domain table. |
| name | varchar | 100 | NULL | Name of the message. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| subject | varchar | 100 | NOT NULL | Subject of the message. |
| recurrence_flag | character | 1 | NOT NULL | Identifies messages that should recurr on the site controller.  If the flag is 'Y' then the recurrence time, days of the week and end datetime will be used to know when the message should be displayed. |
| recurrence_time | time | 8 | NULL | Time that the message should recurr on the site controller when a recurring message. |
| recurrence_days_of_week | varchar | 200 | NULL | Contains a comma separated list of the days of the week. |
| recurrence_week_interval | integer | 4 | NULL | Used in conjunction with the days of the week selection(s) to control how often the acknowledgment required popup will reoccur on iLinks (when ack req is enabled and recurrence is set to yes). For example: This allows a message to be active for a period of time, and show the popup only every other week (instead of every week).

 |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_message_pk | id |
| vsc_message_i1 | start_datetime, end_datetime |
| vsc_message_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** note_acceptor_dvc_cfg_profile_note

**Description**

Contains notes that are associated to the note acceptor device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| note_enabled_flag | character | 1 | NOT NULL | Indicates whether the device will accept the note. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each note acceptor device configuration profile note. |
| VERSION_NUMBER | integer | 4 | NOT NULL | The version number will be used on some of the tables to handle locking.  When a user selects a record for update, the version number will be used in the UPDATEs WHERE clause.  If the version number no longer matches an error will be displayed to the use |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each note acceptor note tracked in the application. |

### Indexes

| Index Name | Columns |
|------------|---------|
| note_acceptor_dvc_cfg_profile_note_pk | id |
| note_acceptor_dvc_cfg_profile_note_i2 | note_acceptor_dvc_cfg_profile_id |
| note_acceptor_dvc_cfg_profile_note_i1 | note_acceptor_note_id |
| note_acceptor_dvc_cfg_profile_note_i3 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| note_acceptor_dvc_cfg_profile_note_fk2 | note_acceptor_dvc_cfg_profile_note | note_acceptor_note |
| note_acceptor_dvc_cfg_profile_note_fk1 | note_acceptor_dvc_cfg_profile_note | note_acceptor_dvc_cfg_profile |

**Table Name:** font_type

**Description**

Lookup table for fonts.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| font_ext_ref | varchar | 100 | NOT NULL | Font external reference. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for the record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each font. |

### Indexes

| Index Name | Columns |
|------------|---------|
| font_type_pk | id |
| font_type_uk1 | key_code |
| font_type_uk2 | font_ext_ref |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** license_type_site_type

**Description**

Contains the valid site types associated to each license type.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | - |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each site type. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each license type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_type_site_type_uk1 | site_type_key_code, license_type_key_code |
| license_type_site_type_i2 | audit_datetime |
| license_type_site_type_pk | id |
| license_type_site_type_i1 | license_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| license_type_site_type_fk1 | license_type_site_type | license_type |
| license_type_site_type_fk2 | license_type_site_type | site_type |

**Table Name:** prfl_grp_type_cfg_prfl_type

**Description**

Link table contains profile group type and configuration profile type pairs.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to profile group type and configuration profile type link records. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for the record. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each group profile type.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| prfl_grp_type_cfg_prfl_type_pk | id |
| prfl_grp_type_cfg_prfl_type_uk1 | cfg_profile_type_key_code, profile_group_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| prfl_grp_type_cfg_prfl_type_fk2 | prfl_grp_type_cfg_prfl_type | cfg_profile_type |
| prfl_grp_type_cfg_prfl_type_fk1 | prfl_grp_type_cfg_prfl_type | profile_group_type |

**Table Name:** trait_uniqueness_type

**Description**

Contains the trait uniqueness type used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each trait uniqueness type. |

### Indexes

| Index Name | Columns |
|------------|---------|
| trait_uniqueness_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_trait

**Description**

Contains the traits assigned to VSCs.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | - |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each trait. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each VSC in the system. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_trait_pk | id |
| vsc_trait_uk1 | vsc_id, trait_id |
| vsc_trait_i1 | trait_id |
| vsc_trait_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| VSC_TRAIT_FK2 | vsc_trait | vsc |
| vsc_trait_fk1 | vsc_trait | trait |

**Table Name:** license_gaming_hours

**Description**

Contains the hours that the EGMS are allowed to be playable for an assigned license.  If no records exist for a license then egm, site and system hours will be used to get effective site hours.



### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each license gaming hours record. |
| end_time | timestamp | 8 | NOT NULL | Time that the EGMs end operation.  1900-01-01-00.00.00 represents midnight.
 |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| start_time | timestamp | 8 | NOT NULL | Time that the EGMs are operational.  1900-01-01-00.00.00 represents midnight. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each weekday.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_gaming_hours_pk | id |
| license_gaming_hours_uk1 | license_id, weekday_type_key_code, start_time |
| license_gaming_hours_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| license_gaming_hours_fk2 | license_gaming_hours | weekday_type |
| license_gaming_hours_fk1 | license_gaming_hours | license |

**Table Name:** contact_type

**Description**

Contains the contact types used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each contact type.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| contact_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** cabinet_dvc_cfg_profile

**Description**

Contains the parameters that are associated to the cabinet device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| large_win_limit | decimal | 16 | NOT NULL | Large win amount. |
| idle_time_period | integer | 4 | NOT NULL | Amount of time, in milliseconds, with a 0 (zero) credit meter and no player input before an EGM is considered idle. |
| report_denom_id | integer | 4 | NOT NULL | Unique identifier associated to the report denomination. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| sync_meter_to_host_flag | character | 1 | NOT NULL | Identifies if the meters should be sync to the host. |
| reel_stop_flag | character | 1 | NOT NULL | This will allow the host to enable/disable whether the EGM will allow the player to stop the reels during game play, effectively ending the game cycle. |
| time_zone_offset | varchar | 6 | NOT NULL | The offset from Universal Coordinate Time (UCT) to local time that should be used when displaying date and time to a locak user of the EGM. |
| no_response_timer | integer | 4 | NULL | Amount of time a device will wait for a response before the timeout logic is invoked. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| outcome_tax_percent | integer | 4 | NOT NULL | This is to support winner taxation parameters. Tax percentage value |
| auto_cashout_amount | decimal | 16 | NULL | Amount to cashout  if the AUTO_CASHOUT_LIMIT is reached or exceeded by the EGM.  If this amount exceeds the credit meter, only the credit meter amount is cashoed out. |
| auto_cashout_limit | decimal | 16 | NULL | When the credit meter reaches or exceeeds this value, the EGM must initiate a voucher cashout. |
| outcome_tax_threshold | integer | 4 | NOT NULL | This is to support winner taxation parameters. Tax treshold value |
| reel_duration | integer | 4 | NOT NULL | This provides a method for a host to control the duration of a game’s game-cycle, that is, the duration of the reel spin animation. |
| min_log_entries | integer | 4 | NULL | Minimum number of log entries that the EGM must maintain in persistent memory. |
| max_credit_meter | decimal | 16 | NOT NULL | Maximum value permitted on the credit meter. |
| idle_text | varchar | 500 | NULL | Text message that will be displayed on the VLT when the cabinet is idle. |
| money_input_disable_limit | decimal | 16 | NULL | When the credit meter reaches or exceeds this value, all money input devices must be disabled by the EGM. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for each locale type. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each non cash amount. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code  assigned to each Auto Cashout Behaviours. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code for the record. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| cabinet_dvc_cfg_profile_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| cabinet_dvc_cfg_profile_fk4 | cabinet_dvc_cfg_profile | currency_type |
| cabinet_dvc_cfg_profile_fk1 | cabinet_dvc_cfg_profile | cfg_profile |
| cabinet_dvc_cfg_profile_fk5 | cabinet_dvc_cfg_profile | accept_non_cash_amount_type |
| cabinet_dvc_cfg_profile_fk2 | cabinet_dvc_cfg_profile | auto_cashout_behaviour_type |
| cabinet_dvc_cfg_profile_fk3 | cabinet_dvc_cfg_profile | locale_type |

**Table Name:** coin_acceptor_dvc_cfg_profile

**Description**

Contains the parameters that are associated to the note acceptor device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to configuration profile. |
| time_to_live_timer | integer | 4 | NULL | Time-to-live value for requests originated by the device. |
| no_response_timer | integer | 4 | NULL | Amount of time a device will wait for a response before the timeout logic is invoked. |
| host_acknowledge_coin_flag | character | 1 | NOT NULL | Indicates whether the device should accept any notes. |
| REQUIRED_FOR_PLAY_FLAG | character | 1 | NOT NULL | Indicates whether the EGM MUST be disabled if the device is disabled by either the host or EGM. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| coin_acceptor_dvc_cfg_profile_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| coin_acceptor_dvc_cfg_profile_fk1 | coin_acceptor_dvc_cfg_profile | cfg_profile |

**Table Name:** egm_protocol_type

**Description**

Contains the EGM protocols managed by the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each EGM protocol.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_protocol_type_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** vsc_function

**Description**

This table stores data for the menu functions that are available on the VMT/VSC.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NULL | Internal identifier for VMT/VSC function. |
| id | integer | 4 | NOT NULL | Internal identifier for VMT/VSC function. |
| DESCR | varchar | 100 | NOT NULL | VMT/VSC function description. |

### Indexes

| Index Name | Columns |
|------------|---------|
| vsc_function_uk1 | descr |
| vsc_function_pk | id |
| vsc_function_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| vsc_function_fk1 | vsc_function | vsc_function |

**Table Name:** site_contact

**Description**

Contains the site contacts managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site contact. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each contact in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| primary_flag | character | 1 | NOT NULL | Indicates if the contact is the primary contact or not. Default is N. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each contact type.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| site_contact_uk1 | site_id, contact_id, contact_type_key_code |
| site_contact_pk | id |
| site_contact_i1 | contact_id, contact_type_key_code |
| site_contact_i3 | audit_datetime |
| site_contact_i2 | contact_type_key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| site_contact_fk3 | site_contact | contact_type |
| site_contact_fk1 | site_contact | site |
| site_contact_fk2 | site_contact | contact |

**Table Name:** license_status_type

**Description**

Contains the license statuses used in the application.

### Primary Key

**Primary Key Columns:** key_code

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each license status in the system. |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_status_pk | key_code |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| None | - | - |

**Table Name:** license

**Description**

Contains the licenses managed by the application.


### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| issue_date | timestamp | 8 | NULL | License issue date. |
| documentation_ref | varchar | 250 | NULL | License documentation reference. |
| status_change_comment | varchar | 250 | NULL | Comment to explain the status change on the the license. |
| deleted_flag | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |
| expire_date | timestamp | 8 | NULL | License expiration date. |
| comment | varchar | 250 | NULL | License comment. |
| license_type_id | integer | 4 | NOT NULL | Unique identifier assigned to each license type in the system. |
| max_egms | integer | 4 | NOT NULL | Maximum number of EGMs allowed by this license. |
| license_ref_number | varchar | 20 | NOT NULL | License reference number. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each License in the system. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | GUI user identifier of who last updated record. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the License. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in license_domain table. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each license type. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each license status in the system. |

### Indexes

| Index Name | Columns |
|------------|---------|
| license_pk | id |
| license_i2 | license_ref_number |
| license_i1 | issue_date, expire_date |
| license_i3 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| license_fk2 | license | license_type |
| license_fk1 | license | license_status_type |

**Table Name:** model

**Description**

Contains the models managed by the application.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| DESCR | varchar | 100 | NOT NULL | Model description. |
| version_number | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each vendor. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each model. |
| owner_domain_id | integer | 4 | NOT NULL | The domain that generated or updated the model. |
| domain_access_restricted_flag | character | 1 | NOT NULL | Identifies the entities access to domains.  'N' means visible to owner domain and all sub-domains and 'Y' means use domains in model_domain table. |
| DELETED_FLAG | character | 1 | NOT NULL | Flag to identify if entity has been logically deleted. Default is N. |

### Indexes

| Index Name | Columns |
|------------|---------|
| model_pk | id |
| model_i1 | vendor_id |
| model_i2 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| model_fk1 | model | vendor |

**Table Name:** egm_gaming_hours_profile

**Description**

EGM Gaming Hour Groups - allows one or more egms assigned to a a profile to override specific daily hours or regular weekly hours 

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| VERSION_NUMBER | integer | 4 | NOT NULL | Version of the record being inserted or modified. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each site in the system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Profile. |
| descr | varchar | 100 | NOT NULL | Description of the EGM Gaming Hours Profile |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| id | integer | 4 | NULL | Unique identifier assigned to each gaming hours profile. |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_gaming_hours_profile_pk | id |
| egm_gaming_hours_profile_uk1 | site_id, descr |
| egm_gaming_hours_profile_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| egm_gaming_hours_profile_fk2  | egm_gaming_hours_profile | site |
| egm_gaming_hours_profile_fk1 | egm_gaming_hours_profile | gaming_hours_profile |

**Table Name:** egm_gaming_hours

**Description**

Contains the regular opening schedule excluding the override hours for an egm_gaming_hours_profile.  Same as the weekly hours in INTELLIGEN.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Group Weekly Override. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Profile. |
| start_time | timestamp | 8 | NOT NULL | Start Time of a period of time. |
| end_time | timestamp | 8 | NOT NULL | End Time of a period of time. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| key_code | varchar | 50 | NOT NULL | Unique identifier/code assigned to each weekday.
 |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_gaming_hours_pk | id |
| egm_gaming_hours_uk1 | egm_gaming_hours_profile_id, weekday_type_key_code, start_time |
| egm_gaming_hours_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| egm_gaming_hours_fk1 | egm_gaming_hours | egm_gaming_hours_profile |
| egm_gaming_hours_fk2 | egm_gaming_hours | weekday_type |

**Table Name:** egm_gaming_hours_override

**Description**

Override hours for specific days in an EGM Gaming Hours Group. 

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |
| technical_override_flag | character | 1 | NOT NULL | Flag to indicate if the override record represents a technical override.  Technical Override available time does not change the timeline setting but keeps the system on for Technicians and suppresses log events to main system. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Group Override for a specific day and period of time. |
| id | integer | 4 | NOT NULL | Unique identifier assigned to each EGM Gaming Hours Profile. |
| start_datetime | timestamp | 8 | NOT NULL | The date and time of the override period start. |
| end_datetime | timestamp | 8 | NOT NULL | The date and time of the override period end. |
| close_all_day_flag | character | 1 | NOT NULL | Flag to indicate if the vlt will not be operating all day.  The default is 'N'. |

### Indexes

| Index Name | Columns |
|------------|---------|
| egm_gaming_hours_override_uk1 | egm_gaming_hours_profile_id, start_datetime |
| egm_gaming_hours_override_pk | id |
| egm_gaming_hours_override_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| egm_gaming_hours_override_fk1 | egm_gaming_hours_override | egm_gaming_hours_profile |

**Table Name:** gaming_hours_profile_domain

**Description**

Table holds the domains that are applicable for each valid Gaming Hours Profile. The domain in this table represents Jurisdictions in a market.  Each domain can only have one default profile.  The default profile will be used to restrict the EGM hours.  If no default profile is provided then no restrictions on hours will be assumed.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each Gaming Hours Profile Domain combination.   |
| id | integer | 4 | NOT NULL | - |
| domain_id | integer | 4 | NOT NULL | - |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| gaming_hours_profile_domain_pk | id |
| gaming_hours_profile_domain_uk1 | gaming_hours_profile_id, domain_id |
| gaming_hours_profile_domain_i1 | audit_datetime |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| gaming_hours_profile_domain_fk1 | gaming_hours_profile_domain | gaming_hours_profile |

**Table Name:** event_handler_dvc_cfg_profile

**Description**

Contains the parameters that are associated to the note acceptor device configuration profile.

### Primary Key

**Primary Key Columns:** id

### Columns

| Column | Data Type | Size | Null | Description |
|--------|-----------|------|------|-------------|
| id | integer | 4 | NOT NULL | Unique identifier assigned to each device configuration profile. |
| time_to_live_timer | integer | 4 | NULL | Time-to-live value for requests originated by the device. |
| min_log_entries | integer | 4 | NULL | Minimum number of log entries that the EGM must maintain in persistent memory. |
| AUDIT_DATETIME | timestamp | 8 | NOT NULL | Date on which the record was inserted or updated. |
| AUDIT_USER_ID | integer | 4 | NOT NULL | User that updated or inserted the current record. |

### Indexes

| Index Name | Columns |
|------------|---------|
| event_handler_dvc_cfg_profile_pk | id |

### Foreign Keys

| FK Name | Child Table | Parent Table |
|---------|-------------|--------------|
| event_handler_dvc_cfg_profile_fk1 | event_handler_dvc_cfg_profile | cfg_profile |

