# CONV Data Dictionary

**Model:** GSM

**Generated:** 2026-11-06 1:52:36 PM

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
