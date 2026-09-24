# Стандарт кодирования AeroCore (MISRA C++ Subset)

Этот документ определяет правила написания кода для бортового вычислительного комплекса AeroCore[span_6](start_span)[span_6](end_span)[span_7](start_span)[span_7](end_span). 

---

## 1. Область применения (Scope)
* **Ядро (core/)**: Код ядра пишется на C++17/C++2строго подчиняетсяся** настоящему стандарту[span_8](start_span)[span_8](end_span).
* **Графический слой (hmi/)**: Код Qt 6 / QML исключен из области действия MISRA, так как GUI-слой не является flight-critical частью системы[span_9](start_span)[span_9](end_span).

---

## 2. Категории правил (Rule CategorMandatory (Обязательно)ельно)** — отступления строго запрещены[span_10](start_span)[span_10](end_spRequired (Требуется)уется)** — допускаются отступления только с оформлением записи об отклонении (*Deviation Record*)[span_11](start_span)[span_11](end_spAdvisory (Рекомендуется)уется)** — базовые рекомендации по стилю и чистке кода[span_12](start_span)[span_12](end_span).

---

## 3. Критические правила MISRA C++:2023 для AeroCore

| Правило / Раздел | Описание | Зачем нужно в AeroCore |
| :--- | :--- | :11.6.211.6.2** | Запрет чтения объектов до их инициализации[span_13](start_span)[span_13](end_span) | Гарантия предсказуемости данных телеметрии и физики[span_14](start_span)[span_14](end_spa7.0.5 / 7.0.6 7.0.6** | Контроль неявных приведений типов | Исключение ошибок точности при расчете 6DoF физики[span_15](start_span)[span_15](end_spa8.18.28.18.2** | Запрет использования присваивания в качестве условия if (x = y)[span_16](start_span)[span_16](end_span) | Предотвращение случайных логических багов[span_17](start_span)[span_17](end_spaMemory PolicyPolЗапрет динамической аллокации (heap)(heap)** после инициализации[span_18](start_span)[span_18](end_span) | Жесткие требования Real-Time: zero-allocation буферы[span_19](start_span)[span_19](end_span)[span_20](start_span)[span_20](end_spa15.0.1 / 15.1.315.1.3** | Соблюдение *Rule of Zero* для спец-функций классов[span_21](start_span)[span_21](end_span)[span_22](start_span)[span_22](end_span) | Корректное управление кадрами данных и кольцевыми буферами[span_23](start_span)[span_23](end_spaConcurrencyrrency** | Строгий контроль разделяемых данных и потоков | Безопасный обмен между SITL-генератором и ядром[span_24](start_span)[span_24](end_span)[span_25](start_span)[span_25](end_spaExceptions/RTTIs/RTTI** | Ограничение или полный отказ от C++ исключений | Гарантированное детерминированное время выполнения циклов[span_26](start_span)[span_26](end_span)[span_27](start_span)[span_27](end_span). |

---

## 4. Обработка ошибок в RT-цикле (Data Core)
* Ошибки датчиков или пакетов не должны прерывать реальный цикл вычислений[span_28](start_span)[span_28](end_span).
* Все ошибки переводятся в явные статус-коды кадра: OK, DEGRADED, CRITICAL[span_29](start_span)[span_29](end_span).

---

## 5. Статический анализ и флаги компилятора
Проверки обеспечиваются автоматически при каждой сборке[span_30](start_span)[span_30](end_span)[span_31](start_span)[span_31](end_sФлаги компиляторалятора**: -Wall -Wextra -Werror -Wconversion -Wsign-conversion[span_32](start_span)[span_32](end_Инструменты CIнты CI**: clang-tidy (с наборами bugprone-*, cert-*, cppcoreguidelines-*)[span_33](start_span)[span_33](end_span)[span_34](start_span)[span_34](end_span).
