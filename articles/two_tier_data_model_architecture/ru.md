Краткая цель статьи — сделать потоки данных проще, более тестируемыми и управляемыми с DTO и Runtime Model структурой.
Эта статья — набор мыслей и экспрессии опыта моего текущего видения этой проблемы, как комбинации опыта от работы над проектами и может быть, переизобретение колеса:) Но, в то же время, я хотел бы поделиться этими мыслями — и, надеюсь, вдохновить и посмотреть на структуры данных.
Концепт использует немного функционала Entities, описанных Robert C. Martin (Uncle Bob) в Clean Architecture, также Model‑Driven engineering вместе с концептом immutability.

Эта статья:
— разделена на секцию теории и применения, чтобы статью можно было понять разработчикам не знающим язык используемый в примерах (Dart).
— в основном фокусируется на client‑side (frontend, app, server‑side рендеринг) разработчиках, но думаю что может быть интересна и другим разработчикам..
— для примеров используется абстрактное финансовое приложение и язык Dart.
Теоретические принципы и концепты в качестве основы

1. Separation of Concerns (разделение ответственности):

Определим два типа:

- Data Transfer Objects (DTOs) отвественные за:

  — точное описание структуры данных источников данных (например, API)
  — сериализацию (конвертирование данных в формат, который легко сохранить или передать) и десериализацию (конвертация обратно) данных.
  — перенос данных между между частями системы.

- Runtime Models: всегда создаваемые из DTO

  — могут включать вычисляемые (computed — рассчитываемые в ходе выполнения программы (runtime)) параметры и дополнительные поля
  — определяют такую структуру данных, которая относится к бизнес логике как к статическим данным, специально разработанных под конкретную часть приложения или UI элементов.

2. Immutability (невозможность изменения состояния обьекта после его создания):
   Оба типа моделей — DTO и Runtime Model должны быть immutable.
   Эта теория может быть противоречивой из‑за крайних случаев (например может вести к повышению использования памяти — так как буквально объектов будет больше), но если вы используете её ‑ она может привести к более предсказуемому и понятному коду.
3. Type Safety (безопасность типов):
   — В DTO — можно добавить дополнительные преобразователи и правила, как именно поля DTO должны сериализоваться/десериализоваться. Этот подход помогает обрабатывать потенциальные ошибки на этапе разработки, а не в продакшене (например, булево значение может быть представлено как «1», 1 (как целое число), «TRUE» или нативное для языка true). Лично я предпочитаю относиться к любой сериализации с законом Мерфи — всё, что может пойти не так (со значениями), пойдет не так.
   — В Runtime Model можно обернуть, создать специфичные поля вычисляемых или статических данных, чтобы поддержать строгую типизацию, например, для ID (в Dart для ID можно использовать типы‑расширения (например, ExpenseId пример ниже)).
4. Гибкость:

— DTO — изменилось имя поля в REST, изменился протокол в gRPC — всё это должно быть отображено там. DTO должны быть гибкими, но только для настройки сериализации/десериализации, не более.

— Runtime Models разработаны более гибкими, чем DTO (можно рассматривать их как Entity в Clean Architecture, но без бизнес‑логики). Они могут включать дополнительные поля или вычисляемые свойства, отсутствующие в DTO, позволяя адаптироваться к специфическим нуждам определенной части приложения или даже разбиваться на совершенно разные модели.
Например, если вы чувствуете, что вашей бизнес‑логике нужны две разные модели, заполняемые из DTO — разделите их, нужен enum — добавьте его. В то же время важно делать то, что имеет смысл — например, если Runtime Model такая же, как DTO, нет смысла создавать её только потому, что «так написано в теории». По моему мнению, иногда лучше переопределить теорию, если она неудобна и не адаптируема для конкретного проекта.

5. Тестируемость

- поскольку все данные immutable, пишите тесты. Разделяйте тесты для парсинг данных для DTO и бизнес‑логику в Runtime Model.

6. Преобразование данных
   используйте Factory методы (методы, которые решают, какой класс инстанцировать) для создания RuntimeModel instances (например, Expense.fromDto, Expense.toDto в примерах ниже), обрабатывая преобразование из DTO в Runtime Model. Это создаст односторонний или двусторонний (если нужно) поток данных. Мне понравилось применять это в играх для различных сохранений и т. д. — т. е. когда у вас есть сложные структуры данных, описанные как Runtime Model (states, и т. д.), но очень сложные для сохранения и загрузки.
7. Global and Local (Глобальное и локальное)
   часто замечал, что иногда не работает принцип, при котором все модели создаются общими для всего приложения. Так как, если вы хотите изолировать часть приложения в общую библиотеку (чтобы делиться между приложениями или бизнес‑логикой) или выйти в Open Source, будет очень сложно рефакторить код. Поэтому иногда применение two tier архитектуры к бизнес‑домену (даже если домен — это просто элемент UI) может быть гораздо эффективнее, но в то же время это очень часто зависит от архитектуры приложения и бизнес‑целей.

Чтобы сделать максимально абстрактно и кратко, переосмыслим концепцию как слои (Layers):

- Внешний слой (External Layer — DTO): отвечает за точное соответствие структуре источников данных (например, ответы API (не только сетевые вызовы, но любой API, который нужно изолировать)).
- Внутренний слой (Internal Layer — Runtime Model): адаптирован под специфические нужды любой части приложения, включая вычисляемые свойства и бизнес‑логику.
- Слой преобразования (другие названия: трансформеры, маппинг, адаптеры): обрабатывает преобразование внешнего слоя во внутренний слой и наоборот.

# Применение теории на практике

Представьте, что вы разрабатываете финансовое приложение на языке Dart, которое отслеживает расходы и инвестиции. Вам нужно обрабатывать данные из различных источников и представлять их в удобном для пользования виде. Давайте попробуем применить к нему описанную выше two‑tier архитектуру.

Примечание: в реальном приложении на dart для генерации вы будете использовать freezed, json_serializable или built_value, но для простоты, для всех примеров ниже, я буду использовать просто чистый Dart.

## Определяя Data Transfer Object (DTO)

Так как DTOs являются переносчиками данных, мы используем их для конвертации json подобных структур.
В нашем финансовом приложении, простой ExpenseDTO может выглядеть так:

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

## Определяя Runtime Model

Продолжая пример финансовго приложения, Expense Runtime Model может выглядеть так (опущу toDTO метод, но при необходимости его можно добавить):

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
    required this.id,
    required this.description,
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

Таким образом, мы используем Runtime Models как глину, подстраивая их под требования бизнеса.

## Соберем модели:

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

## Отломим кусок

Теперь представим, что API имеет строковое поле адрес, но в приложении нам нужны больше полей адреса.
Примечание: в реальном приложении, вероятно, вы будете использовать какой‑то API для парсинга.
Давайте применим поле сначала к ExpenseDTO:

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
      address: json[‘address’], // <— added line
    );
  }

  Map<String, dynamic> toJson() {
    return {
      //…. rest of fields
      ‘address’: address, // <— added line
    };
  }
}
```

Теперь подумаем о моделях
Так как нам нужна более сложная модель AddressDTO, создадим такую (для простоты, представим что нам не нужна Runtime Model):

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

Теперь мым можем добавить модель к Expense если нужно:

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
      //… rest of fields
       address: AddressDTO.from(dto.address)
     );
  }
}
```

Или использовать отдельно:

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

В то же время, если нам нужно будет добавить новые поля в AddressDTO — мы можем создать Address Runtime Model.

```dart
final addressDTO = AddressDTO.from(jsonData.address);
final address = Address.fromDTO(addressDTO);
```

# Применяя к UI

Рассмотрев обычный поток данных, перейдем к UI. Несколько лет назад, меня вводила в путаницу работа с UI-слоем, так как примеры в теории обычно касались бизнес-данных, а не UI/UX-данных, определяющих внешний вид элемента UI. Поэтому начнем с этого:)

Определение проблемы— пример Styled Button (стилизованной кнопки)
Представим простую кнопку. Нужно разработать 15–20 визуально разных вариантов стилей, которые будут переиспользоваться в приложении. Для простоты опустим семантику и логику feedback. Что можно сделать?
Примечание: так как мое отношение субъективно, опишу мысли больше с точки зрения разработчика, чем дизайнера.

Первый вариант создать несколько кнопок для каждого стиля (с вариациями), вдохновляясь Material You — например, Outlined, Filled и т. д.
С точки зрения разработчика, использование известного гайда по наименованиям упрощают переключение и переиспользование компонентов между проектами + сокращает время онбординга в команде + общая логика + дизайнерам легче итерировать, сохраняя синхронизацию с разработчиками.
В то же время, это привязывает дизайн к специфическим, непроектным и небизнесовым гайдам.

Второй вариант создать стилизованные вариации одной кнопки. Назовем это Styled Decorations (название условное: с точки зрения дизайнера и разработчика эта кнопка в реальной жизни скорее всего будет разделена на разные компоненты, но для примера мы пропустим эту иерархию).
Конечно, есть и другие варианты, но остановимся на этих двух, так как это не основная тема статьи.

## Flutter имплементация

Я буду использовать Flutter как пример имплементации идеи Styled Decorators.
Так как нам нужно опредить стиль (а фактически — настройки кнопки), мы можем представить его как DTO или Runtime Model. Чтобы пример был интереснее договримся что StyledButtonDecoration будет Runtime Model. В качестве полей класса используем backgroundColor, border и ничего больше, чтобы сделать акцент на том, как именно их можно использовать.

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

Так как мы договорились что это Runtime Model, добавим для примера getter hasBorder.
Теперь у нас есть два варианта инициализации модели:

1. Можно определить factories или static переменные для нужных стилей.

```dart
class StyledButtonDecoration {
  // ... rest of decoration
  static const _baseOutlined = StyledButtonDecoration(
    color: Colors.transparent,
    border: Border.all(),
  );
  static const primaryOutlined = _baseOutlined.copyWith(
    border: Border.all(color: Colors.red),
  );
  static const primaryFilled= StyledButtonDecoration(
    color: Colors.red,
  );
  // ... or
  static const _outlinedBase = StyledButtonDecoration(
    color: Colors.transparent,
    border: Border.all(),
  );
  static const outlinedPrimary = _outlinedBase.copyWith(
    border: Border.all(color: Colors.red),
  );
  static const filledPrimary= StyledButtonDecoration(
    color: Colors.red,
  );
}
```

Разница в наименовании — это семантика и дизайнерский выбор — то есть то, как будет удобно использовать Разработчику и Дизайнеру. Определяя переменную внутри класса, Разработчик (и AI) может использовать автодополнение кода в IDE, без необходимости запоминать названия, например StyledButtonDecoration.primaryOutlined и модифицировать в месте применения при необходимости, используя copyWith.
Можно заполнить стили через конструктор. Это экстремальный случай, но так как мы договорились рассматривать модель как Runtime Model, мы можем безопасно создать DTO. Из моего небольшого опыта — мне этот метод пригодился при создании например редактора уровней игры и админок.

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

Теперь добавим fromDto метод для StyledButtonDecoration:

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

Таким образом, у нас получится следующий поток данных (data flow):

```dart
final stylesDtos = styles.map(StyledButtonDecorationDTO.fromJson);
final styles = stylesDtos.map(StyledButtonDecoration.fromDTO);
```

Так мы получили динамические стили, которые, возможно, не очень полезны если использовать их напрямую (через индексы), но могут быть очень полезными, если вам нужно, например, дать пользователю приложения больше гибкости в настройках UI .
Важно, что несмотря на то, что такие стили могут быть излишними для большинства приложений, такую логику можно легко представить в игре или приложении (как Figma).
Примечание: этот подход можно легко адаптировать для React, Vue, Kotlin Compose и других фреймворков или использовать его вообще без фреймворка — так как думаю, что это скорее теория, чем реализация.

# Заключение

Найти правильный баланс между созданием слишком большого количества кода, ненужных моделей и в то же время применением их как паттернов, используя правильные инструменты для генерации кода (например, в Dart вы будете использовать freezed с json_serializable или built_value) — сложная задача, и, по моему мнению, это должно полностью зависеть от комбинации бизнес‑целей и целей разработчика.
Для одного приложения вы будете генерировать только DTO, и это будет вполне нормально. Для другого — можно получить очень сложные структуры Runtime Model со сложным преобразованием в/из DTO.
Лично для меня этот путь дал урок, что важно относиться к разработчику как к пользователю так же, как мы относимся к пользователям приложения (даже если разработчик — это AI)...
Надеюсь, что этот концепт окажется полезным для вас :)

Спасибо за ваше время.

Антон
