##  What is Bloc?
**BLoC (Business Logic Component)** is a design pattern that helps to manage state and separate UI from business logic. It is highly used in Flutter for scalable and testable architecture.
There are two main components provided by the `flutter_bloc` package:
- **Cubit** – Simpler way to manage state.
- **Bloc** – More powerful and event-driven approach.

---

##  Cubit
### What is Cubit?
- A **Cubit** is a lightweight class that extends `Cubit<State>`.
- It exposes methods to emit new states.
- No event classes are required (unlike Bloc).

---

### Creating a Cubit

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

class CounterCubit extends Cubit<int> {
  CounterCubit() : super(0);

  void increment() => emit(state + 1);
  void decrement() => emit(state - 1);
}
```

- `state` holds the current state (in this case, an integer).
- `emit()` updates the state and notifies listeners.

---

###  Using Cubit in Flutter

```dart
final counterCubit = CounterCubit();
counterCubit.increment();
print(counterCubit.state); // Output: 1
```

This **won't update the UI** unless you use **BlocBuilder**.

---

###  UI Integration with `BlocBuilder`

```dart
BlocBuilder<CounterCubit, int>(
  builder: (context, counter) {
    return Text('$counter');
  },
);
```

- `BlocBuilder` rebuilds the widget when `state` changes.
- You can wrap it around only the part you want to rebuild (not the whole scaffold).

---

###  Providing Cubit to the App (Shared Across Widgets)
To use the same instance of a Cubit across multiple pages:
```dart
void main() {
  runApp(
    BlocProvider(
      create: (_) => CounterCubit(),
      child: MyApp(),
    ),
  );
}
```

Now in any widget:

```dart
final counterCubit = context.read<CounterCubit>();
```

> Prefer `read<T>()` for one-time access and `watch<T>()` for automatic rebuilds.

---

##  Bloc (More Structured Approach)

### What is Bloc?
- Bloc uses `Events` to trigger logic.
- States are emitted based on Events.
- More powerful and testable.

---

###  Defining Events and State

#### Event:

```dart
abstract class CounterEvent {}

class CounterIncrement extends CounterEvent {}

class CounterDecrement extends CounterEvent {}
```

#### Bloc:

```dart
class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<CounterIncrement>((event, emit) => emit(state + 1));
    on<CounterDecrement>((event, emit) => emit(state - 1));
  }
}
```

---

###  Using Bloc in UI

Provide Bloc:

```dart
BlocProvider(
  create: (_) => CounterBloc(),
  child: MyApp(),
)
```

Trigger event:

```dart
context.read<CounterBloc>().add(CounterIncrement());
```

Listen state:

```dart
BlocBuilder<CounterBloc, int>(
  builder: (context, count) {
    return Text('$count');
  },
);
```

---

##  MultiBlocProvider

To provide multiple Cubits/Blocs:

```dart
MultiBlocProvider(
  providers: [
    BlocProvider(create: (_) => CounterCubit()),
    BlocProvider(create: (_) => CounterBloc()),
  ],
  child: MyApp(),
);
```

---

##  Bloc vs Cubit

| Feature         | Cubit                     | Bloc                             |
| --------------- | ------------------------- | -------------------------------- |
| Input Mechanism | Direct method call        | Events                           |
| Simplicity      | Easier & less boilerplate | More structured                  |
| Flexibility     | Less                      | More (e.g. multiple event types) |
| Use Case        | Simple UI logic           | Complex workflows                |

---

##  Debugging Cubit/Bloc

Override lifecycle methods for logging:

```dart
@override
void onChange(Change change) {
  print(change);
  super.onChange(change);
}

@override
void onError(Object error, StackTrace stackTrace) {
  print(error);
  super.onError(error, stackTrace);
}
```

---

##  Login Form Using Bloc with Validation

---

###  1. Define Login Events

```dart
abstract class LoginEvent {}

class EmailChanged extends LoginEvent {
  final String email;
  EmailChanged(this.email);
}

class PasswordChanged extends LoginEvent {
  final String password;
  PasswordChanged(this.password);
}

class LoginSubmitted extends LoginEvent {}
```

---

###  2. Define Login State

```dart
class LoginState {
  final String email;
  final String password;
  final bool isValid;
  final bool isSubmitting;
  final String? errorMessage;

  LoginState({
    this.email = '',
    this.password = '',
    this.isValid = false,
    this.isSubmitting = false,
    this.errorMessage,
  });

  LoginState copyWith({
    String? email,
    String? password,
    bool? isValid,
    bool? isSubmitting,
    String? errorMessage,
  }) {
    return LoginState(
      email: email ?? this.email,
      password: password ?? this.password,
      isValid: isValid ?? this.isValid,
      isSubmitting: isSubmitting ?? this.isSubmitting,
      errorMessage: errorMessage,
    );
  }
}
```

---

###  3. Implement LoginBloc

```dart
class LoginBloc extends Bloc<LoginEvent, LoginState> {
  LoginBloc() : super(LoginState()) {
    on<EmailChanged>((event, emit) {
      final isValid = event.email.contains('@') && state.password.length > 5;
      emit(state.copyWith(email: event.email, isValid: isValid));
    });

    on<PasswordChanged>((event, emit) {
      final isValid = state.email.contains('@') && event.password.length > 5;
      emit(state.copyWith(password: event.password, isValid: isValid));
    });

    on<LoginSubmitted>((event, emit) async {
      emit(state.copyWith(isSubmitting: true));
      await Future.delayed(Duration(seconds: 2)); // Simulate login
      if (state.email == 'test@example.com' && state.password == '123456') {
        emit(state.copyWith(isSubmitting: false));
      } else {
        emit(state.copyWith(
          isSubmitting: false,
          errorMessage: 'Invalid credentials',
        ));
      }
    });
  }
}
```

---

###  4. UI Integration for Login

```dart
BlocProvider(
  create: (_) => LoginBloc(),
  child: LoginForm(),
);
```

#### In `LoginForm`:

```dart
BlocBuilder<LoginBloc, LoginState>(
  builder: (context, state) {
    return Column(
      children: [
        TextField(
          onChanged: (value) =>
              context.read<LoginBloc>().add(EmailChanged(value)),
          decoration: InputDecoration(
            labelText: 'Email',
            errorText: state.email.contains('@') ? null : 'Invalid Email',
          ),
        ),
        TextField(
          onChanged: (value) =>
              context.read<LoginBloc>().add(PasswordChanged(value)),
          obscureText: true,
          decoration: InputDecoration(
            labelText: 'Password',
            errorText: state.password.length > 5 ? null : 'Too short',
          ),
        ),
        if (state.isSubmitting) CircularProgressIndicator(),
        ElevatedButton(
          onPressed: state.isValid
              ? () => context.read<LoginBloc>().add(LoginSubmitted())
              : null,
          child: Text('Login'),
        ),
        if (state.errorMessage != null)
          Text(state.errorMessage!, style: TextStyle(color: Colors.red)),
      ],
    );
  },
);
```

---

##  Summary

- Use **Cubit** for simple state changes (increment counter, toggle switch).
- Use **Bloc** when you need:
    - Multiple inputs (events)
    - Complex workflows
    - Validation and error handling
- Use **BlocBuilder** to rebuild UI on state changes.
- Use **BlocProvider** or **MultiBlocProvider** to inject state objects.
- Use `context.read<T>()` for accessing Cubit/Bloc.
- Separate concerns: UI ⬌ Events ⬌ State

---