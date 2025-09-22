[LocalStorage: IsarDb @isar]

[Task: TransactionsLocalApi implementation]
Create a [TransactionsLocalApi] implementation that:

1. Data Model:

- Use JSON serialization for complex objects
- Keep collection schema minimal with essential indexed fields
- Store full transaction data as JSON string
- Add @Index annotations for frequently queried fields

2. File Structure:

- Create part files for each collection
- Use common_imports.dart for shared imports
- Export all APIs through data_local_api.dart
- Follow existing error handling pattern with local_api_exceptions.dart

3. Implementation Requirements:

- Implement CRUD operations
- Use IsarDb for persistence
- Follow LastWriteWins strategy
- Support future migrations
- Add proper error handling using LocalApiException

4. Integration:

- Register in dependency injection
- Add to HasLocalApis mixin
- Ensure IsarDb is properly initialized

[Code Organization]

- /data_local_api/
  - isar/
    - isar.dart (main configuration)
    - isar_transaction.dart (collection)
  - transactions_local_api.dart (implementation)
  - data_local_api.dart (exports)

[Example Usage]

```dart
final api = TransactionsLocalApi();
await api.upsertTransaction(transaction);
final result = await api.getTransaction(id);
```

[Output Requirements]

- Follow existing code style
- Add comprehensive documentation
- Include error handling
- Support model versioning
