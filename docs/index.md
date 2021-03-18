---
marp: true
title: Мониторинг производительности JVM
description: Мониторинг производительности JVM
theme: vtb
template: giala
paginate: true
_paginate: false

---

<!-- _class: lead2-->

# Мониторинг производительности JVM
## __Смирнов Вячеслав, 2021__

---

# Исследователь артефактов НТ

![bg cover](img/omsk.jpg)


---

# Много JVM в Kubernetes Pod, Kafka, Elastic Search
![bg right h:700px](img/monitoring-4.svg)

---


# 100 JVM работающих друг с другом и базой
![bg right h:700px](img/monitoring-5.svg)

---


# Сопоставляем входные сигналы метрикам
![bg w:100% ](img/monitoring-7.png)

---

![bg w:100% ](img/monitoring-7.png)

---

![bg w:100% ](img/monitoring-8.png)

---

![bg h:100% ](img/monitoring-9.png)

---

![bg h:100% ](img/monitoring-10.png)

---

![bg h:100% ](img/monitoring-11.png)

---

# Метрики JVM — часть метрик
![bg h:100% ](img/monitoring-11.png)

---

# Метрики JVM — утилизация и сборка мусора
![bg h:100% ](img/plastic-5527525_1920.jpg)

---

# Утилизация влияет на стабильность

![bg h:100% ](img/plastic-5527525_1920.jpg)

![bg h:100% ](img/cairn-4247395_1920.jpg)

---

# Утилизация влияет на стабильность

![bg h:100% ](img/plastic-5527525_1920.jpg)

![bg h:100% ](img/Logins.png)

---

![bg h:100% ](img/Logins.png)

---

![bg h:100% ](img/cpu.png)

---

# Проблемы стабильности сервисов

![bg h:100% right ](img/problems.svg)

---

# Несоотвествие заданных опций фактическим

![bg w:100% right ](img/problems.reconfig.svg)

---

# Несоотвествие заданных опций фактическим

![bg h:100% right ](img/problems.reconfig.2.png)

---

# Потребление памяти больше, чем настроено (утечка?)

![bg w:100% right ](img/problems.memory.1.svg)

---

# Настроено памяти больше, чем есть

![bg w:100% right ](img/problems.memory.2.svg)

---

# Настроено подключений к БД больше, чем есть

![bg w:100% right ](img/problems.db.pool.svg)

---

# Настроено подключений к БД меньше, чем нужно

![bg w:100% right ](img/problems.db.pool.svg)

---

# Утечка файловых ресурсов, подключений, ...

![bg w:100% right ](img/problems.file.leak.svg)

---

# Это покажет мониторинг JVM

![bg h:100% right ](img/problems.svg)

---

# Используемые JVM

![bg w:100%](img/java-version.svg)

---

![bg w:100%](img/java-version.svg)

---

# Поддерживают JMX и JavaAgent от Jolokia и Prometheus

![bg w:90% right](img/openjdk.svg)

---

# Поддерживает JMX, не поддерживает популярные Agent-ы

![bg w:90% right](img/openj9.svg)

---

# Популярные JavaAgent-ы

![bg ](img/hub.docker.com-u-fabric8.png)

---

![bg ](img/hub.docker.com-u-fabric8.png)

---

![bg ](img/hub.docker.com-u-fabric8-images.png)

---

![bg ](img/hub.docker.com-u-fabric8-images-hl.png)

---

![bg w:140%](img/hub.docker.com-u-fabric8-images-hl.png)

---

![bg](img/java-centos-openjdk8-jre.png)

---

![bg ](img/java-centos-openjdk8-jre-hl.png)

---

# Варианты сбора метрик JVM

![bg w:90% right](img/jvm-agent-jmx.png)

---

![bg w:90%](img/jvm-agent-jmx.png)

---

![h:50% bg](img/jvm-jolokia-telegraf.png)

---

![w:95% bg](img/jvm-jolokia-telegraf-influxdb.png)

---

![w:95% bg](img/jvm-prometheus.png)

---

![w:95% bg](img/jvm-telegraf-prometheus.png)

---

![w:95% bg](img/jvm-jmx-jmx_exporter_server.png)

---

![w:95% bg](img/jvm-jmx-jmx_exporter_server-prometheus.png)

---

![w:95% bg](img/jvm-jmx-telegraf.png)

---

![w:95% bg](img/jvm-jmx-jmxtrans.png)

---

![w:95% bg](img/jvm-jmxtrans.png)

---

<!-- _class: head -->

# Утилита JMC - простой просмотр MBean

![w:95% bg ](img/jvm-jmx-jmc.png)

---

![w:95% bg ](img/jvm-jmx-jmc.png)

---

![bg ](img/jmc_path.png)

---

![bg w:100%](img/jmc-version.png)

---

![bg w:100%](img/jmc_view2.png)

---

![bg h:100%](img/jmc-select-MBean-path.png)


---

<!-- _class: head -->

#  Из jolokia через telegraf (jolokia2) в InfluxDB 

![w:95% bg](img/jvm-jolokia-telegraf-influxdb.png)

---

<!-- _class: head -->

# Для каждого MBean нужно правило jolokia2 🙁

![w:95% bg](img/telegraf-jolokia2.png)

---

<!-- _class: head -->

# Для каждого MBean нужно правило jolokia2 🙁

![w:95% bg](img/telegraf-jolokia2-hl.png)

---

<!-- _class: head -->

# 1. Выбираем MBean в JMC

![w:95% bg](img/jmc-select-MBean.png)

---

<!-- _class: head -->

# MBean "Runtime", а точнее java.lang:type=Runtime

![w:95% bg](img/jmc-select-MBean.png)

---


![w:155% bg](img/jmc-select-MBean.png)



---


<!-- _class: head -->

# 2. Выбираем аттрибут(ы) MBean в JMC

![w:95% bg](img/jmc-select-MBean-path.png)

---

<!-- _class: head -->

# Обращаем внимание на тип аттрибутов

![w:100% bg](img/mbean-attribute-type.png)

---


![w:100% bg](img/mbean-attribute-type-hl.png)

---

<!-- _class: head -->

# Выбрали аттрибут "Uptime"

![w:100% bg](img/mbean-attribute-type-hl.png)


---

<!-- _class: head -->

# 3. Формируем правило jolokia2_agent  (Telegraf)

![w:95% bg](img/telegraf-jolokia2-hl.png)

---

<!-- _class: head -->

# 1. Выбираем несколько MBean в JMC

![w:95% bg](img/jmc-select-MBean-2.png)

---

<!-- _class: head -->

# java.lang:type=MemoryPool,name=G1 Survivor ...

![w:155% bg](img/jmc-select-MBean-2.png)

---

<!-- _class: head -->

# java.lang:type=MemoryPool,name=*: маска в name

![w:155% bg](img/jmc-select-MBean-2.png)


---


<!-- _class: head -->

# 2. Выбираем аттрибут(ы) MBean в JMC

![w:95% bg](img/jmc-select-MBean-path2.png)

---


![w:155% bg](img/jmc-select-MBean-path2.png)

---


![w:155% bg](img/jmc-select-MBean-path2-hl.png)

---

<!-- _class: head -->

# Выбрали CollectionUsage, PeakUsage, Usage

![w:95% bg](img/jmc-select-MBean-path2-hl.png)

---

<!-- _class: head -->

# 3. Формируем правило jolokia2_agent (Telegraf)

![w:95% bg](img/telegraf_jolokia2_agent_ast.png)

---

<!-- _class: head -->

# Для разных сервисов есть готовые конфиги 🙂

![bg](img/jolokia2-sample.png)

---

<!-- _class: head -->

# И готовые доски Grafana для Jolokia

![bg](img/grafana-jolokia.png)

---

<!-- _class: head -->

# Из jmx_exporter в Prometheus

![bg w:95%](img/jvm-prometheus-only.png)

---

<!-- _class: head -->

# Настройка jmx_exporter для Prometheus  проще

![bg h:100%](img/jmx_exporter.yaml.png)

---

<!-- _class: head -->

# Но гораздо сложнее 🙂 из-за RegExp-ов

![bg h:100%](img/jmx_exporter.yaml.2.png)

---

![bg w:95%](img/jvm-prometheus-only.png)

---

<!-- _class: head -->

# Накладные расходы на сбор метрик JVM

![bg h:60%](img/jolokia_cache.png)

![bg h:60%](img/jmx_exporter_no_cache.png)

---

![bg h:100%](img/jolokia_cache.png)

---

![bg h:100%](img/jmx_exporter_no_cache.png)


---

<!-- _class: head -->

# Jolokia реже ищет MBean-ы

![bg h:60%](img/jolokia_cache.png)

![bg h:60%](img/jmx_exporter_no_cache.png)

---

<!-- _class: head -->

# Визуализация метрик в Grafana

![bg w:95%](img/all.png)

---

![bg w:95%](img/grafana_ds.svg)

---

<!-- _class: head -->

# Берегите зрение

![bg ](img/grafana-line-width.png)


---


![bg ](img/grafana-line-width-hl.png)

---

<!-- _class: head -->

# Сортируйте данные по убыванию

![bg ](img/grafana-sort-order.PNG)

---


<!-- _class: head -->

# Так проще читать подсказки

![bg ](img/grafana-sort-order-2.PNG)

---

<!-- _class: head -->

# Лучше собирать пореже, но хранить подольше 

![bg ](img/grafana-stability.png)


---

# 1. Мониторим не только JVM

![bg w:100% right ](img/monitoring-11.png)

---

# 2. Способ зависит от JVM и хранилища

![bg w:100% right vertical](img/java-version.svg)

![bg w:100% right](img/jvm-jmx-jmx_exporter_server-prometheus.png)

---

# 3. Важно мониторить утечки

![bg w:100% right](img/telegraf_jolokia2_agent_ast.png)

---

# 4. Метрики достаточно собирать раз в 30 сек

![bg w:100% right ](img/grafana-stability.png)

---


<!-- _class: lead2-->

# Мониторинг производительности JVM
## owasp@ya.ru, t.me/qa_load