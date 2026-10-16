# C.Recipe — Recipe Calculator

**Приложение для учёта рецептов, расчёта ингредиентов и контроля питания.**

| | |
|---|---|
| **Package** | `com.artemsuharev.timbu.myapplicationnew` |
| **minSdk** | 26 (Android 8.0) |
| **targetSdk** | 34 (Android 14) |
| **compileSdk** | 36 |
| **Язык** | Kotlin + Java |
| **UI** | XML (Views) + Jetpack Compose (частично) |
| **Build flavors** | `rustoreRelease`, `rustoreBeta`, `googlePlay` |

---

## 🚀 Быстрый старт

```bash
# Сборка Debug
./gradlew assembleDebug

# Сборка RuStore Release
./gradlew assembleRustoreRelease

# Сборка Google Play Release
./gradlew assembleGooglePlayRelease

# Сборка RuStore Beta
./gradlew assembleRustoreBeta

# Юнит-тесты
./gradlew testDebugUnitTest
```

---

## ✨ Основные возможности

### 🍳 Управление рецептами
- Создание, редактирование и сохранение рецептов
- **5 режимов расчёта ингредиентов:**
  - **Простой** — базовый расчёт пропорций
  - **Форма** — расчёт по диаметру/размеру формы
  - **Порции** — расчёт по количеству порций
  - **Вес** — расчёт общего веса блюда с учётом уварки/ужарки
  - **Калории** — расчёт КБЖУ всего блюда
- Категоризация рецептов, избранное
- Поиск и сортировка по названию, дате, категории
- Добавление изображений (галерея или камера)
- Копирование, удаление, экспорт рецептов

### 📊 Контроль питания
- Расчёт суточной нормы калорий (формула Миффлина-Сан Жеора)
- Индекс массы тела (BMI)
- Учёт уровня физической активности
- Цели: похудение / поддержание / набор веса
- Трекинг приёмов пищи: Завтрак, Обед, Ужин, Перекус
- Учёт потребления воды
- Календарь прогресса с цветовой индикацией
- Графики трендов (калории, белки, жиры, углеводы, вода)
- Архив завершённых курсов (челленджей)

### 🛒 Таблица продуктов
- База из **>3000 наименований** продуктов
- Калории на 100 г — доступны всем
- БЖУ — доступны пользователям полной версии
- Поиск и сортировка по названию, калориям, БЖУ
- Добавление и редактирование продуктов (premium)
- **Сканирование штрих-кода** через OpenFoodFacts API

### 🌐 Общие рецепты
- Публикация рецептов других пользователей
- Сохранение чужих рецептов в свою коллекцию
- Избранное, жалобы, скрытие рецептов
- Модерация опубликованных рецептов

### 📷 Сканирование
- **QR-коды** — получение рецептов от других пользователей
- **Штрих-коды** — поиск продуктов в OpenFoodFacts
- Камера через CameraX + ML Kit Barcode Scanning

### 🔄 Синхронизация
- Firebase Firestore — облачная синхронизация рецептов
- Firebase Auth — авторизация через VK ID и Google
- Firebase Storage — хранение изображений
- Автоматическая синхронизация раз в сутки

### 💳 Подписка (Premium)
- **RuStore Pay** — подписка на 1/3/12 месяцев, free trial
- **Google Play Billing** — подписка через Google Play
- Восстановление покупок, миграция подписок

---

## 🏗 Архитектура

```
app/src/main/java/com/artemsuharev/timbu/myapplicationnew/
├── cr/                    # Splash, MainActivity, настройки, утилиты
├── cr_fragments/          # Фрагменты UI: навигация, рецепты, питание
├── ShareRecipeFragment.kt # Экспорт рецептов
└── Yandex.kt              # Yandex интеграция
```

### Стек технологий

| Категория | Технологии |
|-----------|-----------|
| **UI** | XML Views, Jetpack Compose (Material3), BottomNavigationView, DrawerLayout |
| **Язык** | Kotlin 2.2.10, Java 17 |
| **БД** | Room 2.8.4 (SQLite) |
| **Сеть** | Retrofit 2.9.0, OkHttp 4.12.0, Gson |
| **Firebase** | Auth, Firestore, Analytics, Crashlytics, Storage, Ads, ML Kit |
| **VK ID** | VK SDK 3.1.0, VKID 2.7.0 |
| **Биллинг** | RuStore Pay, Google Play Billing v7 |
| **Аналитика** | Yandex Metrica, MyTracker, Firebase Analytics |
| **Crash-репортинг** | Firebase Crashlytics, OK Tracer (native crashes, heap dumps, disk usage, profiler) |
| **Сканирование** | CameraX, ML Kit, ZXing, Google Vision |
| **Изображения** | Glide, PhotoView |
| **Графики** | MPAndroidChart |
| **Сервисы** | Yandex Cloud Storage, OpenFoodFacts API |

---

## 📱 Навигация

**BottomNavigationView (5 вкладок):**
1. **Простой** — базовый режим редактирования
2. **Форма** — расчёт по размеру формы
3. **Порции** — расчёт по порциям
4. **Вес** — расчёт веса + уварка
5. **Калории** — расчёт КБЖУ

**Боковое меню (Drawer):**
- Мои рецепты
- Коллекция
- Продукты
- Общие рецепты
- Питание (контроль)
- Настройки
- Синхронизация
- Авторизация
- Подписка

---

## 🔐 Разрешения

| Разрешение | Назначение |
|-----------|-----------|
| `CAMERA` | Сканирование QR/штрих-кодов |
| `READ/WRITE_EXTERNAL_STORAGE` | Галерея (API 26–32) |
| `READ_MEDIA_IMAGES` | Выбор фото (API 33+) |
| `POST_NOTIFICATIONS` | Уведомления (API 33+) |
| `INTERNET` | Сетевые запросы |
| `ACCESS_NETWORK_STATE` | Мониторинг сети |
| `VIBRATE` | Вибрация при сканировании |
| `BLUETOOTH_CONNECT` | Bluetooth |

---

## 🧪 Тестирование

```bash
# Юнит-тесты
./gradlew testDebugUnitTest

# Instrumented тесты (на устройстве)
./gradlew connectedRustoreReleaseAndroidTest

# Lint-анализ
./gradlew lintDebug
```

---

## 📦 Сборка и установка

### Debug
```bash
./gradlew assembleDebug
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

### RuStore Release
```bash
./gradlew assembleRustoreRelease
adb install -r app/build/outputs/apk/rustoreRelease/app-rustore-release.apk
```

### Google Play Release
```bash
./gradlew assembleGooglePlayRelease
```

---

## 🛠 Полезные команды

```bash
# Просмотр логов
adb logcat | grep -E "com.artemsuharev.timbu|Firebase|Room|Coroutines"

# Очистка данных приложения
adb shell pm clear com.artemsuharev.timbu.myapplicationnew

# Проверка БД на устройстве
adb shell run-as com.artemsuharev.timbu.myapplicationnew \
  ls -la /data/data/com.artemsuharev.timbu.myapplicationnew/databases/

# Мониторинг памяти
adb shell dumpsys meminfo com.artemsuharev.timbu.myapplicationnew
```

---

## 📄 Лицензия

© 2026 C.Recipe. Все права защищены.

---

## 📞 Контакты

- **Package Name:** `com.artemsuharev.timbu.myapplicationnew`
- **Build flavors:** `rustoreRelease`, `rustoreBeta`, `googlePlay`
