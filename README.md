# Кейс: Влияние загрязнений на количество инфицированных в агентной модели распространения инфекционных заболеваний
Репозиторий проекта "Проектная практика", группа M25-525.

## Формулировка проблемы
Учащение эпидемий и пандемий в XXI веке (например, COVID-19) остро ставит вопрос о необходимости эффективных 
инструментов для прогнозирования нагрузки на системы здравоохранения. 

![1651618612-pandemic-timeline-4.png](docs%2Fimg%2F1651618612-pandemic-timeline-4.png)
*Иллюстрация: [Pandemic Readiness](https://www.safer.me/virus-features/pandemic-readiness/)*

Традиционные дифференциальные уравнения, описывающие [компартментальные модели](https://en.wikipedia.org/wiki/Compartmental_models_(epidemiology)), 
зачастую не учитывают гетерогенность популяции и пространственную структуру контактов. 
Агентное моделирование позволяет преодолеть эти ограничения, 
явно описывая поведение и взаимодействие отдельных индивидуумов (агентов) в популяции, что делает его перспективным 
для анализа сложных, нелинейных эффектов распространения заболеваний, включая влияние загрязнений окружающей среды, 
использование индивидуальных средств защиты, сезонной вариативности иммунитета и эволюции патогена.

Полный цикл исследования распространения инфекционных заболеваний включает моделирование агентов, их взаимодействие,
параметры патогенов, проведение симуляций, сбор данных и, немаловажно, исследование результатов.

Данный проект является попыткой приблизить общий функционал программного комплекса, разработанного в рамках 
проекта "Моделирование распространения инфекционных заболеваний с использованием агентного подхода"
для Зимней научной сессии Студенческого Научного Общества НИЯУ МИФИ 2025г. к уровню, обеспечивающему полный цикл 
исследований, на котором можно предлагать рекомендации ЛПР системы здравоохранения для достижения заданных показателей
эффективности. 

В проекте будет исследоваться один из возможных сценариев оценки последствий изменения входных параметров рассчитываемой 
модели распространения инфекционных заболеваний с использованием агентного подхода (аналитическая методология "What if?").

### Какое отношение данное исследование имеет к экологии?
Известно, что загрязнение воздуха снижает иммунитет и способствует развитию респираторных заболеваний:
- [Effects of atmospheric suspended particulate matter on the immune system](https://romj.org/2024-0103) by Elena V. Kondratyeva, Tatyana I. Vitkina
- [Particulate matter impairs immune system function by up-regulating inflammatory pathways and decreasing pathogen response gene expression](https://www.nature.com/articles/s41598-023-39921-w) by Marín-Palma, D. et al
- [Association of short-term PM2.5 exposure with airway innate immune response, microbiota and metabolism alterations in human airways](https://www.sciencedirect.com/science/article/abs/pii/S0269749124001490) by Shuaiqi Zhao et al
- [Fine particulate matter manipulates immune response to exacerbate microbial pathogenesis in the respiratory tract](https://pmc.ncbi.nlm.nih.gov/articles/PMC11372469/) by Jason Ma et al

Для проекта был смоделирован сценарий экспозиции части агентов повышенному уровню загрязнителя, снижающего иммунитет.

Было проведено 2000 симуляций, в которых варьировались следующие параметры:
- инфективность патогена;
- коэффициент снижения иммунитета у агентов, подверженных загрязнению;
- количество изначально заражённых агентов;
- минимально возможный иммунитет агента;
- максимально возможный иммунитет агента;
- коэффициент снижения инфективности при применении маски.

Количество агентов, находящихся в загрязнённой области, и [остальные параметры](https://github.com/AlekseiAgarkov/AgenticInfectiousDiseaseTransmissionModels/blob/main/configs/project_practice/seir_neighbors_project_practice.toml) 
оставались зафиксированы.

![sim_generation.png](docs%2Fimg%2Fsim_generation.png)
*2000 симуляций*

Нам предстоит выяснить насколько качественно можно спрогнозировать суммарное количество инфицированных спустя 
90 дней от даты первичного инфицирования, зная:
- количество изначально заражённых агентов;
- минимально возможный иммунитет агента;
- максимально возможный иммунитет агента;
- коэффициент снижения иммунитета у агентов, подверженных загрязнению;
- коэффициент снижение инфективности при применении маски.

## Проект "Agent-based Implementations for Infectious Disease Transmission Models"
Проект [Agent-based Implementations for Infectious Disease Transmission Models](https://github.com/AlekseiAgarkov/AgenticInfectiousDiseaseTransmissionModels/) 
представляет собой программный комплекс для моделирования распространения инфекционных заболеваний 
путём имитационного моделирования взаимодействия агентов, представляющих собой стохастические конечные автоматы.
Базовые состояния агентов определяются классическими компартментальными моделями (SIR, SEIR). Проект расширяет 
классические модели, добавляя индивидуальные характеристики агентам 
(возраст, иммунитет, дисциплина использования средств индивидуальной защиты), патогенам (изменение инфективности) и
среде (загрязнения части пространства взаимодействия агентов).

## Данные
### Обучающая выборка
Обучающие данные для модели сгенерированы при помощи симулятора 
[Agent-based Implementations for Infectious Disease Transmission Models](https://github.com/AlekseiAgarkov/AgenticInfectiousDiseaseTransmissionModels/), разработанного в рамках 
проекта "Моделирование распространения инфекционных заболеваний с использованием агентного подхода"
для Зимней научной сессии Студенческого Научного Общества НИЯУ МИФИ 2025г.

Параметры, использованные для генерации данных:
- `beta` - коэффициент инфективности патогена в диапазоне `[0.01, 0.09, 0.17, 0.25]`;
- `pollutant_immunity_reduction` - коэффициент снижения иммунитета у агентов, подверженных загрязнению, в диапазоне `[0, 0.1, 0.2, 0.3]`;
- `initially_infected` - количество изначально заражённых агентов в диапазоне `[4, 6, 8, 10]`;
- `lowest_immunity` - минимально возможный иммунитет агента `[0.1, 0.2, 0.3]`;
- `highest_immunity` - максимально возможный иммунитет агента `[0.6 , 0.75, 0.9]`;
- `mask_beta_penalty` - снижение инфективности при применении маски `[0.25, 0.5]`;
- `seed` - random seed значение симуляции. 

Всего для обучающей выборки было сгенерировано 2000 симуляций.

Данные доступны по ссылке [sim_data_metrics_20251214.csv](https://github.com/AlekseiAgarkov/MIFIML-2-Sem1-M25-525-Project-Practice/tree/main/data/sim_data_metrics_20251214.csv).

## Моделирование воздействия загрязнителя

### Что из себя представляет агент в рамках симуляции?
Агент - стохастический конечный автомат, смоделированный классом [SEIRNeighborsFSMExtended](https://github.com/AlekseiAgarkov/AgenticInfectiousDiseaseTransmissionModels/blob/main/src/models/seir.py#L168) 
с использованием библиотек [simpy](https://simpy.readthedocs.io/en/latest/) и [transitions](https://github.com/pytransitions/transitions).

Состояния агента определены моделью [SEIR](https://web.pdx.edu/~gjay/teaching/mth271_2020/html/09_SEIR_model.html):
* S — восприимчивые к болезни (могут заразиться);
* E — подвергшиеся воздействию (заражены, но ещё не заразны; эта стадия учитывает инкубационный период);
* I — инфицированные (заразны и распространяют болезнь);
* R — выздоровели.

Переходы между состояниями описываются вероятностной логикой взаимодействия с другими агентами.
![SEIRNeighborsFSMExtended.png](docs%2Fimg%2FSEIRNeighborsFSMExtended.png)

С деталями реализации можно ознакомиться в репозтории проекта [SEIRNeighborsFSMExtended](https://github.com/AlekseiAgarkov/AgenticInfectiousDiseaseTransmissionModels/blob/main/src/models/seir.py#L168).

В рамках одной симуляции происходят взаимодействия агентов в разных состояниях. 
"Инфицированные" агенты могут "заражать" других агентов.

![one_sim_vizualized.png](docs%2Fimg%2Fone_sim_vizualized.png)
*Визуализация одной симуляции*

![Agentic Model 4 simulations 90d.gif](docs%2Fimg%2FAgentic%20Model%204%20simulations%2090d.gif)
*Визуализация четырёх симуляций в течение 90 дней*


### Как моделируется взаимодействие агентов
Взаимодействие агентов моделируется следующим образом:
- сгенерированные агенты размещены на плоскости;
- каждый агент имеет N соседей;
- на каждом шаге симуляции каждый агент может заразиться от своих соседей с некоторой вероятностью.

![neighbors_map.png](docs%2Fimg%2Fneighbors_map.png)
*Агент на плоскости (красным цветом) и его соседи (синим цветов)*

### Как моделируется эффект от загрязнителя

На вероятность заражения влияет множество факторов:
  - инфективность патогена, 
  - иммунитет агента (определяется возрастом и сезоном), 
  - воздействие загрязнителя на агента (снижает иммунитет агента),
  - ношение масок соседними заражёнными агентами при контакте.

Часть агентов находится в загрязнённом районе на плоскости взаимодействия.
![exposed_area.png](docs%2Fimg%2Fexposed_area.png)
*Пространство моделирования и область загрязнения*

## Модели
- [20251214-agentic_disease_spread_catboost_pollutant-infected_90d](https://huggingface.co/agarkov-aleksei1/20251214-agentic_disease_spread_catboost_pollutant-infected_90d)
- [20251214-agentic_disease_spread_catboost_pollutant_with_beta-infected_90d](https://huggingface.co/agarkov-aleksei1/20251214-agentic_disease_spread_catboost_pollutant_with_beta-infected_90d)

## Датасеты
- [20251214-20251214-agentic_disease_spread_catboost_pollutant_with_beta-infected_90d-dataset](https://huggingface.co/datasets/agarkov-aleksei1/20251214-agentic_disease_spread_catboost_pollutant_with_beta-infected_90d-dataset)
- [20251214-agentic_disease_spread_catboost_pollutant-infected_90d-dataset](https://huggingface.co/datasets/agarkov-aleksei1/20251214-agentic_disease_spread_catboost_pollutant-infected_90d-dataset)

## Выборка для прогнозирования и валидации
Для прогнозирования и валидации подготовлена выборка с использованием параметров:
- `beta` - коэффициент инфективности патогена в диапазоне `[0.01, 0.09, 0.17, 0.25]`;
- `pollutant_immunity_reduction` - коэффициент снижения иммунитета у агентов, подверженных загрязнению, в диапазоне `[0, 0.1, 0.2, 0.3]`;
- `initially_infected` - количество изначально заражённых агентов в диапазоне `[4, 6, 8, 10]`;
- `lowest_immunity` - минимально возможный иммунитет агента `[0.1, 0.2, 0.3]`;
- `highest_immunity` - максимально возможный иммунитет агента `[0.6 , 0.75, 0.9]`;
- `mask_beta_penalty` - снижение инфективности при применении маски `[0.25, 0.5]`;
- `seed` - random seed значение симуляции. 

Всего для выборки прогнозирования и валидации было сгенерировано 50 симуляций. Выборка доступна по адресу:
https://github.com/AlekseiAgarkov/MIFIML-2-Sem1-M25-525-Project-Practice/blob/main/data/project_practice_20251214.csv

## Материалы
- Ноутбук "20251214 - Train and upload model
  - [Colab версия](https://colab.research.google.com/drive/1vsM7LGdpeMFpMvkMexOowuMjgGZ51ihD)
  - [.ipynb версия](https://github.com/AlekseiAgarkov/MIFIML-2-Sem1-M25-525-Project-Practice/blob/main/notebooks/20251214_Train_and_upload_model.ipynb)
- Ноутбук "20251214 - Model Usage"
  - [Colab версия](https://colab.research.google.com/drive/1RhfjL2WVjdpBdHr2fB1-s5X0zWAU-xnv?usp=sharing)
  - [.ipynb версия](https://github.com/AlekseiAgarkov/MIFIML-2-Sem1-M25-525-Project-Practice/blob/main/notebooks/20251214_Model_Usage.ipynb)
