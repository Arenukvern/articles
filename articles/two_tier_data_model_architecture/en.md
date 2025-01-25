Making data flow management simple, testable and controllable with DTO’s and Runtime Models structure.

This article are thoughts and reflection of my current view to that problem, which combines multiply project experience and maybe reinvention of the wheel:) But in the same time, I would like to share this view — maybe it will inspire you to reimagine your data structures.
The idea uses some Entities functionality described by Robert C. Martin (Uncle Bob) in the Clean Architecture — and also Model-Driven engineering along with concepts of immutability.

This article:

- divided to theory and example parts to make the theory is language agnostic so it would be easy to understand for other developers as well.
- mostly focus on client-side (frontend, app, server-side rendering) developers, but can be used anywhere I think.
- will try to explain this concept using a simple finance app and using Dart language to create code examples.
- uses not native English spelling and grammar (but I’ve tried my best to spellcheck it, sorry).

# Theoretical principles and concepts foundation

1. Separation of Concerns:

Let’s define two data types:

Data Transfer Objects (DTOs) are responsible for:
— matching the exact structure of external data sources (e.g., API responses)
— data serialization (converting data to a format that can be easily stored or transmitted) and deserialization (data transfer, converting it back).
— carrying data between different parts of your system

Runtime Models:

- always created from DTO’s
- can include computed properties and additional fields
- defines data structures which treat business logic as static data for specific to app and UI-specific representation.

2. Immutability (inability to change an object’s state after it has been created):

Both DTOs and Runtime Models are designed to be immutable.
This theory is controversial since for some edge cases it can lead to higher memory usage (literally It would create more instances which will occupy more memory), but if you like to use it — it can leading to more predictable and easier-to-reason-about code. 3. Type Safety:

- In DTOs — you can add additional transformers and rules how exactly DTO’s fields should be serialized / deserialized. This approach helps to handle potential errors during development rather in production (for example — boolean parameter can be represented as “1” 1 (as integer) “TRUE” or native to language true).
  Personally, I like to treat any serialization with Murphy’s law — Anything (any value) that can go wrong will go wrong.

- In Runtime Models you can wrap, create specific fields of computed or static data, to create strong typing, for example ID’s (for example in dart — extension types can be used for IDs (e.g., ExpenseId)).

3. Flexibility:

- DTO’s — field changed name in REST, protocol changed in GRPC — that’s all should go there — DTO’s should be flexible but only to adjust its serialization / deserialization purpose, nothing more.
- Runtime Models are designed to be more flexible than DTOs (you can treat it as Entity in Clean Architecture but without business logic). They can include additional fields or computed properties not present in DTOs, allowing them to adjust to specific needs of the certain part of application or even break down to completely different models.

For example if you feel that your business logic needs two different models which filled from DTO’s — break it, needs enum — add it. In the same time I think it’s important to do what makes sense — for example if Runtime Model is the same as DTO — it makes no sense to create it just because “it is written in guidelines”. In my opinion it is better to redefine guidelines if they are inconvenient and not adaptable for specific project.

5. Testability

- since all data is immutable write tests. Treat data parsing for DTO’s and business logic in Runtime Models separately.

6. Data Transformation

- use Factory methods (methods which decide which class to instantiate) to instantiate Runtime Models (e.g., Expense.fromDto, Expense.toDto) by handle the conversion from DTO to Runtime Model. This will create one-way or two-way (if needed) data flow. I found it useful in games, various saves etc — i.e. when you have complex data structured for runtime (Runtime Models represented as States, classes), but completely inefficient to save.

7. Global and Local

- I found often, that making all models application wide just don’t work, since if you want to isolate part of application to shared (between apps or business logic) or Open Source library, it would be very hard to refactor the code. Therefore sometimes, applying two-tier data model architecture to business domain (even the domain is just UI element) can be far efficient, but it really depends from the App Architecture and business goal.

To make absolutely abstract and short, this concept can be reimagined as Layers:

- External Layer (DTOs): Responsible for matching the exact structure of data sources (e.g., API responses (not only network calls, but any API which needs to be isolated)).
- Internal Layer (Runtime Models): Tailored for any part of application specific needs, including computed properties and business logic.
- Conversion Layer (other names: transformers, mapping, adapters): handles how External Layer will be converted to Internal Layer and vice versa.

# Applying theory to practice

Imagine you’re building a finance app with dart language that tracks expenses and investments. You need to handle data from various sources and present it in a user-friendly way. Let’s try to apply the two-tier model architecture there.

Notice: in real life app you will use freezed or json_serializable or built_value, but for all examples below I will use just raw dart for simplicity.
Defining Data Transfer Objects (DTOs)

Since DTOs are like couriers for your data, we use them to convert json-like structures.
In our finance app, a simple ExpenseDTO might look like this:

```dart
class ExpenseDTO {
  final String id;
  final String description;
  final double amount;
  final String date;

  const ExpenseDTO({
    required this.id,
    required this.description,
    required this.amount,
    required this.date,
  });

  factory ExpenseDTO.fromJson(Map<String, dynamic> json) {
    return ExpenseDTO(
      id: json['id'],
      description: json['description'],
      amount: json['amount'],
      date: json['date'],
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'description': description,
      'amount': amount,
      'date': date,
    };
  }
}
```

## Defining Runtime Models

Continuing with our finance app example, an Expense runtime model might look like this (I omit toDTO method, but if you will need it — add it:)):

```dart
extension type ExpenseId(String value){
  factory ExpenseId.fromJson(final value) => ExpenseId(value);
  String toJson() => value;
}

class Expense {
  final ExpenseId id;
  final String description;
  final double amount;
  final DateTime date;

  const Expense({
    required this.description,
    required this.id,
    required this.amount,
    required this.date,
  });

  factory Expense.fromDTO(ExpenseDTO dto) {
    return Expense(
      id: ExpenseId.fromJson(dto.id),
      description: dto.description,
      amount: dto.amount,
      date: DateTime.parse(dto.date),
    );
  }

  String get formattedAmount => '\$${amount.toStringAsFixed(2)}';
  bool get isRecentExpense => DateTime.now().difference(date).inDays < 7;
}
```

Use Runtime Models as clay to make it simple to adapt for business needs.
Combining models

```dart
void main() {
  // Simulating data from an API
  final jsonData = {
    'id': '123',
    'description': 'Groceries',
    'amount': 50.99,
    'date': '2023-05-15',
  };

  // Create a DTO from the JSON data
  final expenseDTO = ExpenseDTO.fromJson(jsonData);

  // Convert DTO to runtime model
  final expense = Expense.fromDTO(expenseDTO);

  // Use the runtime model in your app
  print('Recent expense: ${expense.formattedAmount}');
  print('Is recent? ${expense.isRecentExpense}');
}
```

## Breaking a piece

Imagine if now API has address, but in the app we will need more comprehensive address fields?
Notice: in real life app, you would probably use some API for it, but as for example it should be fine:)

Let’s apply first to ExpenseDTO

```dart
class ExpenseDTO {
  // …. rest of fields
  final String address; // <— added line

  const ExpenseDTO({
    //…. rest of fields
    required this.address, // <— added line
  });

  factory ExpenseDTO.fromJson(Map<String, dynamic> json) {
    return ExpenseDTO(
      //…. rest of fields
      address: json['address'], // <— added line
    );
  }

  Map<String, dynamic> toJson() {
    return {
      //…. rest of fields
      'address': address, // <— added line
    };
  }
}
```

Now let’s think about Models.
Since we need more advanced AddressDTO, let’s create one (for simplicity, let’s assume we don’t need Runtime Model):

```dart
class AddressDTO {
  final String region;
  final String country;
  final String rawAddress;
  final String houseNumber;

  const AddressDTO({
    required this.region,
    required this.country,
    required this.rawAddress,
    required this.houseNumber,
  });

  factory AddressDTO.fromJson(String json) {
    final (:region, :country, :houseNumber) = parseAddressFromString(json);
    return AddressDTO(
      country: region,
      region: country,
      houseNumber: houseNumber,
      rawAddress: json,
    );
  }
  ({String region, String country, String houseNumber}) parseAddressFromString(
  String json) {
  /// will omit implementation for simplicity
  }
}
```

Now we can add it to Expense if needed, or treat it completely independently:

```dart
class Expense {
  //…. rest of fields
  final AddressDTO address

  const Expense({
    //…. rest of fields
    required this.address,
    });

  factory Expense.fromDTO(ExpenseDTO dto) {
    return Expense(
      //…. rest of fields
      address: AddressDTO.from(dto.address)
    );
  }
}
```

Or just use separately:

```dart
void main() {
  // Simulating data from an API
  final jsonData = {
    'id': '123',
    'description': 'Groceries',
    'amount': 50.99,
    'date': '2023-05-15',
    'address': 'USA, Mary Ave, Sunnyvale, CA 94085'
  };
  final addressDTO = AddressDTO.from(jsonData.address);

  // Create a DTO from the JSON data
  final expenseDTO = ExpenseDTO.fromJson(jsonData);

  // Convert DTO to runtime model
  final expense = Expense.fromDTO(expenseDTO);

  // Use the runtime model in your app
  print('Recent expense: ${expense.formattedAmount}');
  print('Is recent? ${expense.isRecentExpense}');
}
```

In the same time, if the AddressDTO would need to have additional fields — we can create Address Runtime Model.

```dart
final addressDTO = AddressDTO.from(jsonData.address);
final address = Address.fromDTO(addressDTO);
```

## Applying to UI

With usual data flow has been covered, it is time to move to UI part. What was frustrating for me years ago is working with UI layer, because many examples from theory usually written around about business data, but not about UI/UX data which defines how particular UI element would look like, so I will start from here:)

### Defining a problem — Styled Button example

Let’s imagine a simple button. We have to design 15–20 visually different variants of button, which will be reused inside the app. For simplicity we will omit semantics & feedback logic. What we can do? (note: I’m biased, and will write down thoughts more from Developer perspective, then Designer’s).

One option is to create multiply buttons, to represent each style (with its variations) and take inspiration from Material You guidelines — for example to have Outlined, Filled etc.

Thinking from developer perspective, using similar naming convention makes easier to switch and reuse same components between projects —it reduces onboarding time + shares logic + this option allows Designers to iterate easier and faster while keeping sync with Developers.
In the same time, it ties design to specific, non project and non business naming conventions.
Other option is to create styled variation of one button. Let’s call it Styled Decorations (it can be called differently, it’s just an example, also note: from designer perspective and from developer perspective this button can and realistically will be separated to different components, we will omit this inner hierarchy).
Of course it's not all options, but let’s stick to these two as it is far from topic of article.
Flutter implementation
I will use an app, developed with Flutter as an example to implement here-above Styled Decorators idea.

Since we need to define style, which actually are properties of button, we can think of it as DTO or Runtime Model. To make example more comprehensive, let’s treat StyledButtonDecoration as Runtime Model. For properties we will add only backgroundColor, border properties to emphasize how it can be used.

```dart
class StyledButtonDecoration {
  final Color backgroundColor;
  final Border? border;
  const StyledButtonDecoration({
    this.backgroundColor = Colors.white,
    this.border,
  });
  factory StyledButtonDecoration.copyWith({
    Color? backgroundColor,
    Border? border
  })=> StyledButtonDecoration(
    backgroundColor: backgroundColor ?? this.backgroundColor,
    border: border ?? this.border,
  );
  bool get hasBorder => border != null;
}
```

Since we agreed that it’s Runtime Model, we can define a getter hasBorder as an example.
Now we have at least two options how styles can be initialized:

1. We can define factories or static variables for specific styles.

```dart
class StyledButtonDecoration {
  // ... rest of decoration
  static const \_baseOutlined = StyledButtonDecoration(
    color: Colors.transparent,
    border: Border.all(),
  );
  static const primaryOutlined = \_baseOutlined.copyWith(
   border: Border.all(color: Colors.red),
   );
  static const primaryFilled= StyledButtonDecoration(
   color: Colors.red,
  );
   // ... or
  static const \_outlinedBase = StyledButtonDecoration(
   color: Colors.transparent,
   border: Border.all(),
  );
  static const outlinedPrimary = \_outlinedBase.copyWith(
   border: Border.all(color: Colors.red),
  );
  static const filledPrimary= StyledButtonDecoration(
   color: Colors.red,
  );
}
```

The difference in naming is semantics and design decision — how it would convenient for Developer and Designer to use. Either way, by defining it inside class as variable, Developer (and AI) can use these defined static with code-completion in IDE, without a need to remember names.

2. We can define data to populate these styles via constructor. It’s extreme case, but since we treat it as Runtime Model, we can safely create DTO and use it if needed. From my little experience — I find it useful while creating editors-like apps (like game level editor, admin panel).

```dart
/// Styles example raw data
const buttonStyles = [
  {
    'backgroundColor': 'FFF',
    'borderColor': 'FFF',
    //...etc
  },
];

class StyledButtonDecorationDTO {
  /// We can parse it to Color if needed, or keep it String,
  /// to have access to original value - it would depend on
  /// business task
  final Color backgroundColor;
  final Color borderColor;
  /// ... rest of parameters which can be used for Border
  const StyledButtonDecorationDTO({
    required this.backgroundColor,
    required this.borderColor,
  });
  factory StyledButtonDecorationDTO.fromJson(final Map<String, dynamic> map){
    return StyledButtonDecorationDTO(
      backgroundColor: parseColorFromHex(map['backgroundColor']),
      borderColor: parseColorFromHex(map['borderColor']),
    );
  }
  Map<String, dynamic> toJson() => {
    'backgroundColor': backgroundColor,
    'borderColor': borderColor,
  };
}
```

Then we can add fromDto method to the StyledButtonDecoration:

```dart
class StyledButtonDecoration {
  ///... rest of class
  factory StyledButtonDecoration.fromDTO(StyledButtonDecorationDTO dto)=>
    StyledButtonDecoration(
      backgroundColor: dto.backgroundColor,
      border: Border.all(StyledButtonDecoration.borderColor),
    );
}
```

This way we now can define the data flow:

```dart
final stylesDtos = styles.map(StyledButtonDecorationDTO.fromJson);
final styles = stylesDtos.map(StyledButtonDecoration.fromDTO);
```

What we got here is dynamic styling, which is not very useful if using it directly, but can be very useful if you need to give for example App User more flexibility to define how UI look. Again, it may be uneccessary for most of the apps, but you can imagine a game or app (like Figma) where it can be extremely useful.
Note: this approach can be easily adjusted for React, Vue, Kotlin compose and other great frameworks or use it without framework at all — since I think it’s more a theory, rather than implementation.

# Conclusion

Finding the right balance between making too much code, unnecessary models and in the same time applying them as patterns, using right tools for code generation (for example in dart you will use freezed with json_serializable, or built_value) is hard thing, and in my opinion it should completely depend from business and developer goals combined.
For one app — you will generate only DTO’s and it would be completely fine. For another — you may end up with complex runtime models structures and complex conversion to / from DTO’s.
So for me, this journey gave me lesson to start thinking that highly important to treat developer as user in the same way we treat users as users of the app (even if developer is AI)…
Hope that this concept will be useful for you too:)
Thank you for your time.
