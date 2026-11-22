# Lab 2 – DartPad Exercises (Steps 1 to 4)

## Step 1: Named Parameters and Default Values
```dart
double price({required double unit, required int quantity, double discount = 0}) {
  return unit * quantity * (1 - discount);
}

void main() {
  print('Total 1: ${price(unit: 500, quantity: 3)}');
  print('Total 2: ${price(unit: 500, quantity: 3, discount: 0.1)}');
  print('Total 3: ${price(quantity: 2, unit: 1000, discount: 0.25)}');
}
```
**Explanation:** Curly braces `{}` declare named parameters. `required` forces the caller to supply `unit` and `quantity`, while `discount = 0` provides a default value when omitted.

---

## Step 2: Null Safety with `??`
```dart
String? findTown(String code) {
  if (code == 'YDE') return 'Yaoundé';
  if (code == 'DLA') return 'Douala';
  return null;
}

void main() {
  print(findTown('YDE') ?? 'Unknown town');
  print(findTown('BFX') ?? 'Unknown town');
}
```
**Explanation:** `String?` allows the function to return `null`. The if-null operator (`??`) safely falls back to `'Unknown town'` if the result is `null`, preventing runtime crashes.

---

## Step 3: Collections (`where`, `map`, and `fold`)
```dart
void main() {
  final prices = [250.0, 600.0, 1200.0, 450.0, 800.0];

  final above500 = prices.where((p) => p > 500).toList();
  print('Above 500: $above500');

  final increased = above500.map((p) => (p * 1.10).round()).toList();
  print('Increased by 10%: $increased');

  final total = increased.fold<int>(0, (sum, p) => sum + p);
  print('Total: $total XAF');
}
```
**Explanation:** `where` filters elements matching a condition, `map` transforms each item, and `fold` combines all values into a single total starting from `0`.

---

## Step 4: Classes and `async` / `await`
```dart
class Product {
  final String name;
  final int price;

  const Product(this.name, this.price);

  bool get isFree => price == 0;

  String describe() => '$name costs $price XAF (Free: $isFree)';
}

Future<String> fetchStatus() async {
  await Future.delayed(const Duration(seconds: 1));
  return 'Server connection verified!';
}

Future<void> main() async {
  const item = Product('Textbook', 3500);
  print(item.describe());

  print('Checking server...');
  final status = await fetchStatus();
  print(status);
}
```
**Explanation:** `const` creates a compile-time constant instance, `get` defines a computed property, and `async`/`await` pauses execution until the `Future` completes without blocking the program.
