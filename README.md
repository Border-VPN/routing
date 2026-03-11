# RoscomVPN Routing

Готовые конфигурации маршрутизации для [Happ](https://happ.su), [INCY](https://incy.cc) и [Mihomo](https://github.com/MetaCubeX/mihomo) (Clash Meta, Clash Mi и др.)

> Быстрый и универсальный роутинг: без дыр и утечки вашего сервера, "хирургическая" фильтрация, все нужное — разблокировано, а ненужное — заблокировано

**Таргет:** Россия + Беларусь

---

## Установка для Happ

| Способ | Ссылка | Описание |
|--------|--------|----------|
| Быстрая установка | [routing.help](https://routing.help) | Редирект на диплинк, открыть на устройстве |
| DEFAULT.DEEPLINK | [Просмотр](https://raw.githubusercontent.com/hydraponique/roscomvpn-routing/refs/heads/main/HAPP/DEFAULT.DEEPLINK) | Диплинк-ссылка в текстовом формате |
| DEFAULT.JSON | [Просмотр](https://raw.githubusercontent.com/hydraponique/roscomvpn-routing/refs/heads/main/HAPP/DEFAULT.JSON) | JSON-конфиг роутинга |

## Установка для INCY

| Способ | Ссылка | Описание |
|--------|--------|----------|
| Быстрая установка | [incy.routing.help](https://incy.routing.help) | Редирект на диплинк, открыть на устройстве |
| DEFAULT.DEEPLINK | [Просмотр](https://raw.githubusercontent.com/hydraponique/roscomvpn-routing/refs/heads/main/INCY/DEFAULT.DEEPLINK) | Диплинк-ссылка в текстовом формате |
| DEFAULT.JSON | [Просмотр](https://raw.githubusercontent.com/hydraponique/roscomvpn-routing/refs/heads/main/INCY/DEFAULT.JSON) | JSON-конфиг роутинга |

## Установка для Mihomo (Clash Meta)

Готовые YAML-шаблоны в папке `MIHOMO/`:

| Файл | Описание |
|------|----------|
| `default.yaml` | DEFAULT конфиг для добавления в приложение вручную и 40+ rule-провайдерами |
| `template_remnawave.yaml` | DEFAULT конфиг для интеграции с панелью Remnawave |

Подставьте URL вашей подписки и используйте с любым Mihomo-совместимым клиентом (Clash Mi, Clash Verge и др.).

---

## Преимущества

### Кастомный GeoIP — [GitHub](https://github.com/hydraponique/roscomvpn-geoip)

Максимально уменьшенный geoip.dat — выпилено все, кроме кастомного списка `geoip:direct`, где:
- ➕ Русские/белорусские CIDR-диапазоны из трёх независимых геобаз: GeoLite2 (MaxMind), IPinfo, DB-IP
- ➕ Кастомный список IP-диапазонов "казенных" VK Company, Yandex, CDNVideo (включая их зарубежные активы)
- ➕ CIDR Apple Push-уведомлений (решение проблем с доставкой уведомлений на iOS устройствах)
- ➖ DIFF-исключение списков: [Re:filter](https://github.com/1andrevich/Re-filter-lists) + [Antifilter.Network](https://antifilter.network) (для разблокировки РКН-списков)
- ➖ DIFF-исключение Community-списков: [Re:filter](https://github.com/1andrevich/Re-filter-lists) + [Antifilter.Network](https://antifilter.network) + [Antifilter.Download](https://antifilter.download) (для проблемных/не работающих, НЕ заблокированных сервисов — 4pda, CloudFlare, аниме и др.)
- ➖ DIFF-исключение [зарубежных CDN-сервисов](https://github.com/PentiumB/CDN-RuleSet) + кастомный список Hetzner и ZeroCDN (а именно их CIDR стран нашего таргета)
- ➖ DIFF-исключение `0.0.0.0/8` из private списка (предотвращение утечки DNS на некоторых устройствах)

### Кастомный Geosite — [GitHub](https://github.com/hydraponique/roscomvpn-geosite)
- **Обновленные списки сервисов** — максимально оптимизированы под этот роутинг + дедупликация
- **Минималистичный подход** — то, чего нет в конфиге роутинга, выпилено с корнем
- **Облегченные списки** — разгружают ядро от фильтрации мусора и include-редиректов

---

## Что роутится в DEFAULT-версии

### BLOCK (блокировка)
- **Домены слежки Windows** — отключаем телеметрию и слежку за пользователями
- **BitTorrent DHT** — известные публичные DHT-серверы, для экономии трафика вашего сервера и успокоения хостера
- **Реклама VK Company** — отключаем рекламу в ВК Видео и ВК Музыке

### DIRECT (напрямую)
- **Русские/белорусские** домены и CIDR-диапазоны (за исключением РКН-списков + РФ активов зарубежных CDN-сервисов)
- **"Казенные" сервисы РФ и CDN** — VK, OK, Mail.Ru, Яндекс, CDNVideo (включая их зарубежные активы на зарубежных IP)
- **Сервера обновлений и пуш-уведомлений** — Apple, Microsoft, Android/Google Play (корректная работа устройства + экономия трафика сервера)
- **Все существующие банки РФ и их зарубежные домены** — вытащены с сайта ЦБ РФ + собрано саморезолвингом
- **Игровые платформы** — Steam, Epic Games, Riot Games, Escape from Tarkov (экономия трафика сервера + проблемы при пуске через прокси)
- **Faceit** — фикс для РФ игроков, увеличиваем количество доступных локаций серверов
- **Twitch** — экономия трафика сервера
- **Pinterest** — блокировка рекламы на сервисе

### PROXY (через VPN)
- **YouTube** — борьба с ТСПУ и банами РКН
- **Telegram** — борьба с ТСПУ и банами РКН
- **GitHub** — борьба с ТСПУ и банами РКН
- **Twitch-ads** — возвращаем полное качество (Source) стримов с блокировкой рекламы
- **Весь остальной глобальный интернет** — все, чего нет в других списках, включая все зарубежные CDN

---

## DNS

| Назначение | Сервер | Зачем |
|------------|--------|-------|
| Domestic (direct) | [Яндекс DNS](https://dns.yandex.ru/) `77.88.8.8` | Для работы ВЕЗДЕ в РФ — без вариантов в реалиях БС, шатдаунов и ТСПУ. Низкий пинг в РФ |
| Remote (proxy) | [Google Public DNS](https://developers.google.com/speed/public-dns/) `8.8.8.8` | Резолвинг-DNS для проксируемого трафика |

---

## Интеграция с панелями (ADDON_AUTOROUTING)

Готовые модули для автоматической инъекции роутинга в пользовательские подписки:

| Панель | Формат | Описание |
|--------|--------|----------|
| [3x-ui](ADDON_AUTOROUTING/3x-ui/) | Non-JSON | Кастомный форк с поддержкой роутинга |
| [Marzban](ADDON_AUTOROUTING/Marzban%20JSON/) | JSON | `subscription.py` для JSON-подписок |
| [Marzban](ADDON_AUTOROUTING/Marzban%20NON-JSON/) | Non-JSON | `subscription.py` для стандартных подписок |
| [Marzneshin](ADDON_AUTOROUTING/Marzneshin%20JSON/) | JSON | `subscription.py` для JSON-подписок |
| [Marzneshin](ADDON_AUTOROUTING/Marzneshin%20NON-JSON/) | Non-JSON | `subscription.py` для стандартных подписок |
| [Remnawave](ADDON_AUTOROUTING/Remnawave/) | API | Контейнер для автообновления роутинга через API |

Модули `subscription.py` монтируются в контейнер панели и автоматически подставляют актуальные geoip.dat/geosite.dat в подписки пользователей.

---

## Автообновление

Конфиги автоматически обновляются при выходе новых релизов [roscomvpn-geoip](https://github.com/hydraponique/roscomvpn-geoip) и [roscomvpn-geosite](https://github.com/hydraponique/roscomvpn-geosite). GitHub Actions:
- Проверяет теги апстрим-репозиториев
- Обновляет URL и таймстемпы в JSON-конфигах
- Генерирует base64-диплинки для Happ и INCY
- Коммитит изменения автоматически

## Связанные проекты

- [roscomvpn-geoip](https://github.com/hydraponique/roscomvpn-geoip) — IP-диапазоны (geoip.dat)
- [roscomvpn-geosite](https://github.com/hydraponique/roscomvpn-geosite) — доменные списки (geosite.dat)

---

> **Ставь ⭐** и не пропусти регулярные обновления для поддержания актуальности списков и оптимальной производительности

##### USDT TRC20: TMu3N2ZjK5omJ7n3WAj5MNCSM5querBXsR

##### Спасибо Всем за поддержку!
###### Сделано с ❤️ к свободному интернету!
