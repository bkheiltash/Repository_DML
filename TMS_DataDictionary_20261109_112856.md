# TMS Data Dictionary

**Model:** GSM

**Generated:** 2026-11-09 11:28:56 AM

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
