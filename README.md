# GTA Network Platform (Исходные коды) — [DEPRECATED]

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Language](https://img.shields.io/badge/C%23-87.8%25-blue)](https://github.com/Gta5Classic/platform/search?l=c%23)
[![Language](https://img.shields.io/badge/C%2B%2B-11.6%25-blue)](https://github.com/Gta5Classic/platform/search?l=c%2B%2B)
[![Status](https://img.shields.io/badge/Status-Deprecated-red)](https://github.com/Gta5Classic/platform)

## 📌 О проекте

Данный репозиторий содержит **исходные коды устаревшей (`Deprecated`) версии платформы GTA Network** — клиент-серверного решения для создания мультиплеерных модификаций к Grand Theft Auto V. Проект является предшественником более современных систем и представляет исторический интерес для изучения архитектуры GTA:MP модов.

Платформа состоит из двух ключевых компонентов:
*   **Клиентская часть (`Client`)** — внедряется в игровой процесс GTA V через модификации и DLL-инъекции.
*   **Серверная часть (`Server`)** — отвечает за бэкенд-логику, синхронизацию игроков и предоставляет API для разработки серверных скриптов.

**Важно:** Проект более не поддерживается и не рекомендован к использованию в продакшн-среде. Он оставлен в открытом доступе исключительно в образовательных и архивных целях.

## 🏗️ Архитектура и стек технологий

### Структура репозитория

platform/
├── Client/ # Клиентский модуль (C++/C#)
│ ├── GUI/ # Рендеринг графического интерфейса
│ ├── Networking/ # Сетевые протоколы и синхронизация
│ ├── Streamer/ # Управление стримингом мира и сущностей
│ └── Sync/ # Механизмы синхронизации состояния
├── Server/ # Серверный модуль (C# .NET)
│ ├── Elements/ # Базовые игровые сущности (Entity Component System)
│ ├── Managers/ # Менеджеры ресурсов, соединений и т.д.
│ └── API.cs # Публичное API для разработчиков скриптов
├── Shared/ # Общие библиотеки и утилиты
├── Shv.NET/ # Устаревший модуль SimpleHTTPVector
├── Setup/ # Инструменты для сборки и инсталляции
├── images/ & libs/ # Статические ресурсы и сторонние зависимости
├── Map2Resource/ # Конвертер карт в игровые ресурсы
└── NativeUI/ # Библиотека для нативного UI на основе масштабируемых элементов


### Используемые технологии
*   **Клиент**: C++, C#, DirectX (для GUI), Native C++ Hooks.
*   **Сервер**: C# (.NET Framework), работающий как самостоятельное консольное приложение.
*   **API**: Простые текстовые пакеты (packets), предположительно использующие `TCP` сокеты.
*   **Сборка**: `MSBuild` (C# проекты) и `Visual Studio` (решение `GrandTheftAutoNetwork.sln`).

## ⚙️ Системные требования

*   **Операционная система**: Windows 7/8/10 (x64).
*   **Игра**: Grand Theft Auto V (лицензионная версия).
*   **Среда выполнения**: .NET Framework 4.5+ (для сервера и клиента), Visual C++ Redistributable.
*   **Инструменты сборки**: Visual Studio 2017/2019 с поддержкой C++ и .NET desktop development.

## 🚀 Установка и запуск

> ⚠️ **Внимание**: Ввиду устаревшего статуса, актуальная сборка может потребовать доработок. Приведены общие принципы сборки и запуска.

### Для разработки и сборки
1.  **Клонируйте репозиторий:**
    ```bash
    git clone https://github.com/Gta5Classic/platform.git
    cd platform

    Откройте решение GrandTheftAutoNetwork.sln в Visual Studio.

Восстановите NuGet-пакеты (особенно для Server и Shv.NET проектов).

Выберите конфигурацию сборки Release / Debug и платформу x64.

Соберите решение (Build Solution). Успешная сборка создаст:

Client/bin/x64/Release/GTANetworkClient.dll (клиентский плагин).

Server/bin/Release/GTANetworkServer.exe (серверное приложение).

Для запуска сервера
Перейдите в папку Server/bin/Release/.

Запустите GTANetworkServer.exe.

При необходимости настройте параметры в App.config (порт, максимальное количество игроков и т.д.).

Для запуска клиента
Поместите скомпилированный GTANetworkClient.dll в папку с модами (например, в scripts/ или внедрите через ASI-лоадер).

Запустите GTA V.

Внутриигровой GUI (Client/GUI) позволит подключиться к серверу по IP-адресу и порту.

💻 Использование (API для разработчиков)
Сервер предоставляет простое API для создания собственных игровых режимов. Пример базового скрипта на C#:

using GTANetworkServer;

public class MyGameMode : Script
{
    public MyGameMode()
    {
        API.onPlayerConnected += OnPlayerConnected;
        API.consoleOutput("GameMode loaded!");
    }

    private void OnPlayerConnected(Client player)
    {
        API.sendChatMessageToPlayer(player, "~g~Welcome to the custom server!");
        API.setPlayerSkin(player, PedHash.FreemodeMale01);
        API.setPlayerPosition(player, new Vector3(0, 0, 72));
    }
}


Ключевые методы API находятся в Server/API.cs. Доступны возможности:

Управление игроками (телепортация, экипировка, здоровье).

Взаимодействие с транспортом и объектами мира.

Отправка сообщений и создание GUI.

Работа с базой данных и таймерами.

🤝 Внесение вклада
Проект является архивным и официально не поддерживается. Однако, если вы обнаружили критическую ошибку или хотите предложить улучшение, вы можете:

Сделать форк репозитория.

Создать ветку с вашими изменениями (git checkout -b feature/amazing-feature).

Зафиксировать изменения (git commit -m 'Add some amazing feature').

Отправить изменения в ваш форк (git push origin feature/amazing-feature).

Открыть Pull Request в оригинальный репозиторий.

Все PR будут рассмотрены, но в связи с прекращением поддержки, их слияние не гарантировано.

📜 Лицензия
Проект распространяется под лицензией MIT. Это означает, что вы можете свободно использовать, копировать, изменять, объединять, публиковать, распространять, сублицензировать и/или продавать копии программного обеспечения, при условии сохранения уведомления об авторских правах и разрешении. Подробнее см. в файле LICENSE.

Авторские права (Copyright): (c) 2017 GTA Network
