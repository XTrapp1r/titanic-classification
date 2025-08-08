# Titanic Classification

**Цель проекта**
Построить классификационную модель для предсказания выживаемости пассажиров Титаника.

## Структура репозитория

titanic-classification/
├── data/
│   └── train.csv             исходный датасет
├── notebooks/
│   └── eda\_and\_modeling.ipynb  ноутбук с EDA, препроцессингом и сравнением моделей
├── model.pkl                 обученная модель (не пушится)
├── scaler.pkl                StandardScaler (не пушится)
├── predict.py                скрипт для генерации предсказаний
├── requirements.txt          список зависимостей
├── .gitignore
└── README.md

## Установка

git clone [https://github.com/XTrapp1r/titanic-classification.git](https://github.com/XTrapp1r/titanic-classification.git)
cd titanic-classification

Создать и активировать виртуальное окружение
python -m venv venv

# на Mac/Linux

source venv/bin/activate

# на Windows

venv\Scripts\activate

Установить зависимости
pip install -r requirements.txt

## Обучение модели

Если нужно переобучить модель с другими гиперпараметрами:

1. Открыть notebooks/eda\_and\_modeling.ipynb
2. Выполнить ячейки в разделах EDA, Preprocessing и Training & Evaluation
3. В конце ноутбука выполнить сохранение артефактов:
   import joblib
   best\_model = models\['XGBoost']
   best\_model.fit(X\_train, y\_train)
   joblib.dump(best\_model, '../model.pkl')
   joblib.dump(scaler,    '../scaler.pkl')

## Генерация предсказаний

python predict.py data/train.csv result.csv

* data/train.csv — входной файл (тот же формат, что исходный датасет)
* result.csv — выходной файл с колонками PassengerId,Survived, например:
  PassengerId,Survived
  1,0
  2,1
  3,1
  …

## Метрики моделей

| Модель             | cv ROC-AUC | Accuracy | Precision | Recall | ROC-AUC |
| ------------------ | ---------- | -------- | --------- | ------ | ------- |
| LogisticRegression | 0.858      | 0.804    | 0.793     | 0.667  | 0.843   |
| RandomForest       | 0.852      | 0.816    | 0.781     | 0.725  | 0.831   |
| **XGBoost (best)** | **0.862**  | 0.804    | 0.758     | 0.725  | 0.821   |

## Выводы

1. Пол: женщины выживают чаще мужчин.
2. Класс: выживаемость выше в первом классе.
3. Возраст: оптимальные шансы у пассажиров 20–30 лет и у детей.
4. Стоимость билета: более дорогие билеты коррелируют с лучшей выживаемостью.

## Лицензия

Этот проект распространяется под лицензией MIT.
