# High Availability & Disaster Recovery (DR) Strategy

This directory documents the data redundancy architecture implemented to comply with corporate data retention policies and cross-region disaster recovery mandates.

## Architecture Overview

* **Primary Production Region:** Europe (Stockholm) `eu-north-1`
* **Disaster Recovery Region:** Europe (Ireland) `eu-west-1`
* **Mechanism:** Automated, asynchronous Amazon S3 Cross-Region Replication (CRR).
* **Data Integrity:** Bucket Versioning is strictly enabled across both buckets to protect against accidental deletions or ransomware overwrites.

## Replication Status Monitoring Steps

To verify that the backup infrastructure is operating properly, the security and ops teams follow these monitoring procedures:
1. **Object-Level Validation:** Upload a test object to the primary production bucket and check the object's metadata properties under `Replication status`. It should shift from `PENDING` to `COMPLETED`.
2. **Destination Audit:** Confirm the identical object, along with its unique version ID, appears automatically in the `internee-dr-backup-bucket`.
3. **CloudWatch Metrics (Optional):** Monitor `ReplicationLatency` and `BytesPendingReplication` via Amazon CloudWatch to detect unexpected sync delays across geographic boundaries.
