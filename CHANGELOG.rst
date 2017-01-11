Changelog
=========

Version 0.3.0
-------------

- Significant performance improvements because operations are buffered.
- BulkIndexErrors are now caught and reraised as OperationFailed.
- Support for connecting to multiple Elasticsearch hosts. See
  https://github.com/mongodb-labs/mongo-connector/wiki/Usage-with-Elasticsearch#connecting-to-multiple-elasticsearch-hosts.

Version 0.2.0
-------------

- Bug fix for namespace information saved in the mongo-connector metadata index.
- Support AWS Elasticsearch Service Request Signing.

Version 0.1.0
-------------

This was the first release of elastic-doc-manager.
