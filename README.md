const TMDB_API_KEY = "e8d924a87f0a5678c043b1683b169a2b"; // ВАЖНО: небезопасно для продакшна!
const BASE_URL = "https://api.themoviedb.org/3";
const LATEST_RELEASES_URL = `${BASE_URL}/movie/popular?api_key=${TMDB_API_KEY}&language=en-US&page=1`;
const IMAGE_BASE_URL = "https://image.tmdb.org/t/p/w500"; // Для постеров

async function fetchLatestReleases() {
    try {
        const response = await fetch(LATEST_RELEASES_URL);
        const data = await response.json();
        const movies = data.results;

        // Теперь используйте данные (movies) для динамического создания
        // элементов <li> в вашем карусели Splide с id="latest-releases"
        // (см. ваш HTML-файл).

        // ... Код для обновления DOM ...
        // Например, для "The Batman"[cite: 63], вы бы взяли название, год и постер
        // из объекта movie:
        // const posterPath = movie.poster_path;
        // const fullImageUrl = IMAGE_BASE_URL + posterPath;

    } catch (error) {
        console.error("Ошибка при получении данных TMDb:", error);
    }
}

// Вызовите функцию в main.js
// fetchLatestReleases();
