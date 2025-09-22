It's more of a technical note, rather than an article, so I will try to express the idea more in a condensed and clear manner.

Before getting started, if your way to see how it works, I've recently uploaded small package - [see it here](https://pub.dev/packages/is_dart_empty_or_not#).

Coming from the JS/TS world, when I first used Dart, the most fascinating thing among others was to use the **isEmpty** or **isNotEmpty** functions, and for strings, lists, maps, etc. It was amazingly simple, just not to write every time **.length == 0**.

Also, it was very useful to use **empty/zero** values like **Duration.zero, Offset.zero**, and many others that were a nice addition to this pattern.

Over time, I developed a habit to use the same principle for different cases and came to think, what if we use zero values for most cases, eliminating the need for null for most cases (not all, but nonetheless)? I searched and found that a similar pattern is used in Go, so I've started thinking:

# Problem

imagine situation:

```dart
String? value;

// do something

value = "new value”;
```

What checks should we make to ensure the value exists to assign some value to a new variable?

```dart
final String newValue;
if(value != null && value.isEmpty){
  // do something
  newValue = “defaultValue”;
}  else {
  newValue = value;
}
```

What is the difference between null and isEmpty check in this situation?
What if we write

```dart
String value = “”;
final String newValue;

if(value.isEmpty){
  // do something
  newValue = “defaultValue”;
} else {
  newValue = value;
}

// use newValue
```

Nice but still verbose.
Would that be nice to use it inline? Let's try to rewrite it with a new extension:

```dart
extension StringX on String {
  String whenEmptyUse(String value) => isEmpty ? value : this;
}

final newValue = value.whenEmptyUse("defaultValue");
```

What if we try to apply it to lists, maps, values, and numbers?

```dart
extension ListX on List<T> {
  List<T> whenEmptyUse(List<T> values) => isEmpty ? values : this;
}

final newValues = values.whenEmptyUse(['defaultValue']);

extension DoubleX on double {
  bool isZero => this == 0;
  double whenZeroUse(final double value) => isZero ? value : this;
}

final opacity = 0;

final newOpacity = opacity.whenZeroUse(0.5);
```

This pattern is extremely useful with zero/empty values for objects too. For example:

```dart
class Person {
  const Person({this.name=''});
  final String name;

  static const empty = Person();

  bool get isEmpty => name.isEmpty;
  bool get isNotEmpty => name.isNotEmpty;
  // or use different names for to read nicer
  bool get isInitialized => name.isNotEmpty;
  bool get isNotInitialized => name.isEmpty;
}

extension PersonX on Person {
 Person whenEmptyUse(Person value) => isEmpty ? value : this;
}

```

Then we could use it everywhere the same simple way as checking a string:

```dart
var person = Person.empty;

// do something dangerous

final newPerson = person.whenEmptyUse(Person(name:'Frodo'));
```

We could do same for IDs, Lists with types, etc. etc..
This way we use simpler API, always know for sure that we have some value and we know how to identify default (empty, zero) value.

Hopefully it helps:)

Please don't forget to share your thoughts in comments:) it really helps the algorithms give this article to others to read, and it would be great support from you:)

Have a nice day!
