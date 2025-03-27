# S3
aws s3

S3 Basics (End-to-End)
├── 1. What is S3?
│   ├── Definition
│   │   ├── Simple Storage Service: AWS cloud-based object storage
│   │   └── Purpose: Store and retrieve any amount of data anytime
│   ├── Key Features
│   │   ├── Scalable: From 1 KB to terabytes, no limits
│   │   ├── Durable: 99.999999999% (11 nines) durability
│   │   ├── Accessible: Via web, CLI, SDK (e.g., Python Boto3)
│   │   └── Object Storage: Stores data as objects (not files/folders)
│   ├── Components
│   │   ├── Buckets: Containers for objects
│   │   ├── Objects: Files with key, value, metadata
│   │   └── Regions: Geographic locations (e.g., us-east-1)
│   ├── Use Cases
│   │   ├── Data Storage: CSVs, JSONs, images for pipelines
│   │   ├── Backups: Long-term data archiving
│   │   ├── ML Datasets: Feed into SageMaker, Databricks
│   │   └── Static Websites: Host HTML files
│   └── Why It Matters
│       ├── Foundation for AWS Stack: Links to Glue, Redshift, Kafka
│       └── Scalability for Future: Supports your MLOps/Lakehouse goals
├── 2. Buckets
│   ├── Definition
│   │   ├── Containers: Hold objects (like folders but flat structure)
│   │   └── Scope: Belong to an AWS account, region-specific
│   ├── Creating Buckets
│   │   ├── Tools: AWS Console, CLI, SDK
│   │   ├── Naming Rules
│   │   │   ├── Globally Unique: No duplicates worldwide
│   │   │   ├── Lowercase: a-z, 0-9, hyphens only
│   │   │   ├── Length: 3-63 characters
│   │   │   └── Example: "my-s3-bucket-2025-mar20"
│   │   ├── Region Selection: e.g., us-east-1 (affects latency, cost)
│   │   └── Defaults: Public access blocked (security)
│   ├── Managing Buckets
│   │   ├── List: View all buckets in Console
│   │   ├── Configure: Later topics (e.g., events)
│   │   ├── Delete: Remove empty buckets
│   │   └── Example: "my-practice-bucket-2025" for testing
│   └── Why It Matters
│       ├── Organization: Groups data for pipelines
│       └── Integration: Connects to Glue, Databricks in your stack
├── 3. Objects
│   ├── Definition
│   │   ├── Files: Data stored in buckets (e.g., CSVs, JSONs)
│   │   └── Structure: Key (name), Value (content), Metadata (info)
│   ├── Key Concepts
│   │   ├── Key: Unique identifier in bucket (e.g., "data/sales.csv")
│   │   ├── Value: Actual file content (e.g., CSV rows)
│   │   ├── Metadata: System (size, date) or custom (e.g., "owner: me")
│   │   └── Size Limit: 0 bytes to 5 TB per object
│   ├── Actions
│   │   ├── Uploading
│   │   │   ├── Methods: Console, CLI, SDK (e.g., Boto3)
│   │   │   ├── Process: Select file, upload to bucket
│   │   │   └── Example: Upload "test-data.csv"
│   │   ├── Downloading
│   │   │   ├── Methods: Console (click "Download"), CLI, SDK
│   │   │   ├── Process: Retrieve file to local system
│   │   │   └── Example: Download "test-data.csv"
│   │   ├── Deleting
│   │   │   ├── Methods: Console (select, delete), CLI, SDK
│   │   │   ├── Process: Remove file from bucket
│   │   │   └── Example: Delete "test-data.csv"
│   │   └── Practice Example: Upload, download, delete a CSV
│   └── Why It Matters
│       ├── Data Source: Feeds into Databricks, DBT, SageMaker
│       └── Pipeline Start: Raw data for processing
├── 4. Storage Classes
│   ├── Definition
│   │   ├── Types: Options for storing objects based on access needs
│   │   └── Purpose: Optimize cost and performance
│   ├── Main Storage Classes
│   │   ├── Standard
│   │   │   ├── Use: Frequently accessed data (e.g., active datasets)
│   │   │   ├── Cost: Higher storage, low access cost
│   │   │   └── Example: "sales.csv" for daily analytics
│   │   ├── Intelligent-Tiering
│   │   │   ├── Use: Data with changing access patterns
│   │   │   ├── Feature: Auto-moves between frequent/infrequent tiers
│   │   │   └── Example: ML datasets with variable use
│   │   ├── Standard-IA (Infrequent Access)
│   │   │   ├── Use: Less accessed data (e.g., monthly reports)
│   │   │   ├── Cost: Lower storage, higher retrieval cost
│   │   │   └── Example: "old-reports.csv"
│   │   ├── Glacier
│   │   │   ├── Use: Archival, rarely accessed data
│   │   │   ├── Cost: Very low storage, high retrieval cost/time
│   │   │   └── Example: Backups from 2 years ago
│   │   └── Glacier Deep Archive
│   │       ├── Use: Ultra-rare access (e.g., compliance data)
│   │       ├── Cost: Cheapest storage, longest retrieval (hours)
│   │       └── Example: Legal docs from 5+ years
│   ├── Managing Storage Classes
│   │   ├── Set During Upload: Choose class in Console/CLI
│   │   ├── Change Later: Move objects manually or via lifecycle rules
│   │   └── Practice: Upload "sample.csv" to Standard, move to Glacier
│   └── Why It Matters
│       ├── Cost Efficiency: Saves money in pipelines
│       └── Flexibility: Matches data usage in Databricks, MLOps
├── 5. Access Permissions (Basics)
│   ├── Definition
│   │   ├── Control: Who can access buckets and objects
│   │   └── Purpose: Secure data, enable integrations
│   ├── Key Concepts
│   │   ├── Public Access
│   │   │   ├── Default: Blocked (secure)
│   │   │   ├── Enable: Make bucket public (e.g., for websites)
│   │   │   └── Risk: Only for non-sensitive data
│   │   ├── Bucket Policies
│   │   │   ├── JSON-based: Rules for access
│   │   │   ├── Example: Allow Glue to read from bucket
│   │   │   └── Use: Fine-grained control
│   │   ├── IAM Roles
│   │   │   ├── Assign: To AWS services (e.g., Lambda, Databricks)
│   │   │   ├── Purpose: Secure service access
│   │   │   └── Example: Grant S3 read/write to Glue
│   ├── Managing Permissions
│   │   ├── Console: Edit "Block Public Access" or "Bucket Policy"
│   │   ├── Practice: Check default permissions, make a file public briefly
│   │   └── Revert: Ensure bucket stays private after testing
│   └── Why It Matters
│       ├── Security: Protects data in pipelines
│       └── Integration: Enables Glue, Databricks to access S3
