# Better Lyrics — установка (сборка 3.0.2.4)

Версия: 3.0.2.4

## Прямые ссылки для скачивания

- Chrome / Edge / Brave / Opera:
  <https://raw.githubusercontent.com/MERAD-dsg/better-lyrics/arena/5257e29b-better-lyrics/release/better-lyrics-3.0.2.4-chrome.zip>
- Firefox:
  <https://raw.githubusercontent.com/MERAD-dsg/better-lyrics/arena/5257e29b-better-lyrics/release/better-lyrics-3.0.2.4-firefox.zip>

На странице репозитория: ветка `arena/5257e29b-better-lyrics` → папка `release` → файл →
кнопка **Download raw file**.

## Что нового в 3.0.2.4

### Диагностика перезапуска видео (эта сборка)

Раз «High resolution video» выключен, а видео всё равно перезапускается — причина в другом месте,
и чтобы её не угадывать, в сборку встроен трассировщик. Он включается тумблером
**Show logs** (Настройки → General) и пишет в консоль:

- каждый вызов методов плеера, способных перезапустить видео
  (`updateVideoData`, `loadVideoByPlayerVars`, `cueVideoByPlayerVars`, `loadVideoById`,
  `nextVideo`, `playVideo`, `seekTo`, …) — с аргументами и **стеком вызова**, то есть видно,
  кто именно инициировал перезапуск: сама страница YouTube Music или расширение;
- события видео: `emptied`, `loadstart`, `loadedmetadata`, `seeking`, `seeked`, `waiting`, `ended`
  — с текущей позицией;
- сообщение `video quality settings received in the page world`, если настройки качества вообще
  доходят до скрипта в мире страницы (их отсутствие означает, что весь модуль качества не работает).

### Как собрать лог (2 минуты)

1. Установите эту сборку (см. ниже) и откройте [music.youtube.com](https://music.youtube.com).
2. В настройках расширения: **General → Show logs** — включите.
3. Перезагрузите вкладку YouTube Music (F5).
4. Откройте консоль вкладки: **F12 → вкладка Console**.
5. Включите трек с видео и дождитесь 2–3 циклов перезапуска.
6. Скопируйте все строки, начинающиеся с `[BetterLyrics]` (или `player.` / `video:`), и пришлите их.

По стеку вызова будет точно видно, что перезапускает плеер.

### Что уже исправлено ранее

- **3.0.2.3** — перезагрузка плеера для разблокировки качеств выше 1080p больше не зацикливается
  (было: 43 перезагрузки за 6 секунд) и возвращает позицию воспроизведения;
- **3.0.2.2** — «Чистый полноэкранный режим»: убирает футер под текстом, плавающую панель
  управления и кнопки громкости/«⋮» у названия песни (Display → Fullscreen).

## Установка

### Chrome / Edge / Brave / Opera

1. Распакуйте `better-lyrics-3.0.2.4-chrome.zip` в любую папку
   (или возьмите уже распакованную папку `chrome` из релиза).
2. Откройте `chrome://extensions` (в Edge — `edge://extensions`).
3. Включите **«Режим разработчика»** (переключатель справа сверху).
4. Нажмите **«Загрузить распакованное расширение»** и выберите распакованную папку
   (ту, где лежит `manifest.json`).
5. Откройте [music.youtube.com](https://music.youtube.com) и обновите вкладку.

> Папку, которую вы выбрали, удалять нельзя — браузер читает расширение прямо из неё.

### Firefox

1. Распакуйте `better-lyrics-3.0.2.4-firefox.zip` (или возьмите папку `firefox`).
2. Откройте `about:debugging#/runtime/this-firefox`.
3. Нажмите **«Загрузить временное дополнение»** и выберите `manifest.json` внутри папки.
4. Откройте [music.youtube.com](https://music.youtube.com).

> Временные дополнения в Firefox удаляются при закрытии браузера. Для постоянной установки
> используйте подписанную версию с [Firefox Add-ons](https://addons.mozilla.org/en-US/firefox/addon/better-lyrics/).

## Что можно проверить сразу

- **Выключите расширение** (тумблер на `chrome://extensions`) и включите тот же трек.
  Если видео всё равно перезапускается — это поведение самого YouTube Music, а не расширения.
- Попробуйте тот же трек **не в полноэкранном режиме** и **на вкладке «Текст песни» / «Далее»**.
- Выключите по очереди: Display → Fullscreen → **Karaoke**, Display → **Blurred album art background**,
  Display → **Controls dock** — и проверьте, что изменится.
