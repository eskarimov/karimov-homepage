+++
title = "Заметки о системах каталогов данных"
date = 2021-01-25
thumbnailPath = "/self/img/thumbs/catalog.jpg"
tags = ["data catalog", "big data"]
isPopular = false
+++

Каталог данных стал неотъемлемой частью современной инфраструктуры данных и управления ими.
Это позволяет иметь единую точку входа для исследования и поиска данных организации,
путем хранения метаданных о них, таких как местоположение, формат, столбцы / атрибуты и пр.
Это становится особенно важно, когда команды внутри организации переходят к современным моделям менеджмента,
таким как [Data Mesh]((https://martinfowler.com/articles/data-monolith-to-mesh.html)),
когда каждая команда может вносить свой вклад в арсенал данных организации.

В отрасли растет интерес к повышению производительности труда дата-инженеров и сайентистов  
с помощью метаданных. Следующие проекты были выпущены за последние несколько лет:
- [Dataportal von AirBnb](https://medium.com/airbnb-engineering/democratizing-data-at-airbnb-852d76c51770)
- [Databook von Uber](https://eng.uber.com/databook/)
- [Amundsen von Lyft](https://www.amundsen.io/)
- [Metacat von Netflix](https://netflixtechblog.com/metacat-making-big-data-discoverable-and-meaningful-at-netflix-56fb36a53520)
Естественно, в этой области появилось несколько стартапов, для меня одним из наиболее интересных выглядит [Tree Schema](https://treeschema.com/).

До сих пор я пытался использовать только Amundsen вместе с Apache Atlas (который помогает строить взаимосвязи между данными),
это отличная связка, однако есть аспект, которого не хватает почти в каждом продукте, - возможность задавать
и отслеживать качество данных. Однако данной темы я бы хотел бы коснуться в следующей статье.