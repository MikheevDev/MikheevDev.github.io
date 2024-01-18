---
title: Смайлики для Jekyll
category:
 - Jekyll
---

В этой шпаргалке перечислены некоторые доступные и работающие в настоящее время смайлы , которые можно использовать в
документах Markdown для веб-сайтов, созданных Jekyll . Emoji включаются с помощью плагина Jekyll Jemoji ꜛ , 
который работает как в ваших локальных запусках Jekyll, так и на GitHub Pagesꜛ.

### Включение Jemoji на вашем сайте
Добавьте следующую запись в свой Gemlile:
```
gem 'jemoji'
```
Примечание . Поместите эту запись в отдельную строку. Не указывайте это в group :jekyll_plugins do.

Кроме того, добавьте следующую запись в список плагинов в вашем файле _config.yml:
```
plugins:
  - jemoji
```
При необходимости обновите пакет для вашей локальной сборки с помощью следующей команды терминала:
```
bundle update
```
#### Доступные смайлы

Face Smiling

|     emoji     |     code      |
| ------------- | ------------- |
| 	:grinning:   | 	`:grinning:` |
|   :smiley:    |  `:smiley:`   |
| 	:smile:   | 	`:smile:` |
|   :laughing:    |  `:laughing:`   |
| 	:rofl:   | 	`:rofl:` |
|   :slightly_smiling_face:    |  `:slightly_smiling_face:`   |
| 	:wink:   | 	`:wink:` |
|   :innocent:    |  `:innocent:`   |
| 	:grin:   | 	`:grin:` |
|   :joy:    |  `:joy:`   |
|   :sweat_smile:    |  `:sweat_smile:`   |
| 	:upside_down_face:   | 	`:upside_down_face:` |
|   :blush:    |  `:blush:`   |
