# Семантическое распознавание кассовых чеков на основе Vision-Encoder-Decoder

Репозиторий содержит материалы магистерской диссертации по теме 
«Разработка и исследование end-to-end системы семантического распознавания 
кассовых чеков на основе Vision-Encoder-Decoder моделей».

**Автор:** Станкевич Светлана Олеговна  
**Университет:** УрФУ, ИРИТ-РТФ, группа РИМ-240931к  
**Год:** 2026

---

## Описание

Разработана система семантического распознавания русскоязычных кассовых чеков 
на основе архитектуры Donut (Document Understanding Transformer). 
Система выполняет прямое преобразование изображения чека в структурированный 
JSON без использования традиционных OCR-систем.

**Извлекаемые поля:**
- `seller` — наименование продавца
- `inn` — ИНН организации
- `date` — дата операции
- `total` — итоговая сумма покупки
- `items` — перечень товаров

---

## Результаты

| Поле | Donut F1 | Tesseract F1 |
|------|----------|--------------|
| inn | 0.533 | 0.097 |
| date | 0.726 | 0.255 |
| total | 0.784 | 0.016 |
| среднее | 0.511 | 0.099 |

Прирост среднего F1-score по сравнению с Tesseract OCR — в 5 раз.

---

## Датасет

Специализированный датасет русскоязычных кассовых чеков размещен на HuggingFace:

[![Dataset](https://img.shields.io/badge/HuggingFace-Dataset-yellow)](https://huggingface.co/datasets/cdek-ocr/receipt-ocr-ru)

- 999 изображений, полученных в реальных условиях съемки
- Разметка 5 семантических полей в формате JSONL
- Первый публичный датасет с реквизитами российского документооборота (ИНН, фискальный накопитель)

---

## Запуск

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/14C-7vZd8NQAzaFyKHs0xPtTEJVBt4jGo#scrollTo=-mHHC3u1wIvZ)

### Зависимости
```bash
pip install transformers torch pillow gradio
```

---

## Структура репозитория
├── notebook.ipynb        # Обучение и оценка модели, а также сравнение с baseline Tesseract OCR + регулярные
├── README.md

---

## Стек

- Модель: [Donut](https://huggingface.co/naver-clova-ix/donut-base)
- Фреймворк: HuggingFace Transformers
- Среда обучения: Google Colab (NVIDIA L4)
- Интерфейс: Gradio
