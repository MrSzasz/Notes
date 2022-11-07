# Fav Movies App (Redux)

Este proyecto tiene como fin el poder armar una aplicación que nos deje guardar películas favoritas de base, a la cual se le agregarán más funcionalidades, como el hecho de poder agregar películas a una lista de pendientes o vistas, además de poder guardar estos datos en una base de datos, pero hay que ir de a poco, es por eso que empezaremos guardando las películas favoritas en local. La base de esto está hecho en el apartado de [Redux](../Redux.md).

## Cambios

Para empezar haremos unos cambios en cuanto a lo antes armado, por lo que cambiaremos la forma de tener las películas, utilizando la API [TMDB](https://www.themoviedb.org/).  
En el home agregaremos un cuadro de búsqueda que enviará las queries a la API para buscar las películas, luego mostrará los resultados en diferentes cards, las cual debemos crear. Para ello crearemos el componente `MainCard` de la siguiente manera.

```jsx
const MainCard = ({ movie }) => {       // Le pasamos el resultado que obtuvimos de la búsqueda
    return (
        <div className="bg-slate-600 relative w-fit h-fit group overflow-hidden border-4 border-black">
            <img
                className="max-w-[200px] h-[20em] object-cover"
                src={
                    movie.poster_path === null
                        ? "https://miro.medium.com/max/800/1*hFwwQAW45673VGKrMPE2qQ.png"        // Si no tiene poster le pasamos una imagen genérica
                        : `https://image.tmdb.org/t/p/w200${movie.poster_path}`         // Sino le pasamos el poster
                }
                alt={movie.original_title + "poster"}
            />
            <div className="absolute w-full h-[20em] top-full group-hover:top-0 transition-all flex flex-col gap-4 py-4 px-2 bg-clip-padding backdrop-filter backdrop-blur-xl bg-opacity-60 bg-black">      // Creamos el div que contendrá toda la info
                <h2 className="text-2xl">{movie.original_title}</h2>
                <p className="overflow-y-scroll w-auto h-full scrollbar-hide">
                    {movie.overview}
                </p>
                <button className="w-full bg-green-700 hover:bg-green-800 transition-all border-2 border-black py-1 rounded-lg uppercase">add</button>      // Y el botón que usaremos para añadirlo a la lista
            </div>
        </div>
    );
};

export default MainCard;
```

> Para quitar el scrollbar se utilizó el plugin `tailwind-scrollbar-hide`

Ahora podemos pasarlo al Home, quedándonos de la siguiente manera.

```jsx
import $ from "jquery";
import { AiOutlineSearch } from "react-icons/ai";
import { useState } from "react";
import MainCard from "../../components/MainCard/MainCard";

const Home = () => {
    const [moviesArray, setMoviesArray] = useState([]);

    const handleSearch = async (e) => {
        e.preventDefault();
        let query = $("#movieQuery").val();
        if (query !== "") {
            try {
                const url = `https://api.themoviedb.org/3/search/movie?api_key=${
                    import.meta.env.VITE_APIKEY
                }&page=1&query=${$("#movieQuery").val()}`;
                await fetch(url)
                .then((res) => res.json())
                .then((data) => setMoviesArray(data.results));
            } catch (err) {
                console.error(err);
            }
        }
    };

    return (
        <div className="bg-zinc-900 text-white min-h-screen h-fit text-center flex flex-col gap-8 p-4">
            <div className="flex mx-auto justify-center items-center bg-white rounded-lg overflow-hidden">
                <input
                    type="text"
                    placeholder="Search a movie"
                    id="movieQuery"
                    className="text-black p-2 focus-visible:outline-none"
                />
                <button
                    className="bg-white h-full p-2 text-black"
                    onClick={handleSearch}
                >
                    <AiOutlineSearch />
                </button>
            </div>
            <div>
                {moviesArray?.length !== 0 && (
                    <section className="flex flex-wrap justify-evenly gap-y-4">
                        <h2 className="w-full">Results</h2>
                            {moviesArray?.map((movie) => (
                                <MainCard key={movie.id} movie={movie} />
                            ))}
                    </section>
                )}
            </div>
        </div>
    );
};

export default Home;
```

Con esto hecho podemos agregar el handler para agregar las películas al store en nuestra `mainCard.jsx`

```jsx
import { useDispatch } from "react-redux";
import { addMovie } from "../../features/movies/favMovieListSlice";

const MainCard = ({ movie }) => {
    const dispatch = useDispatch();

    const handleAdd = (name, id, poster) => {
        dispatch(addMovie({ name, id, poster }));
    };

    return (
        <div className="bg-slate-600 relative w-fit h-fit group overflow-hidden border-4 border-black">
            <img
                className="max-w-[200px] h-[20em] object-cover"
                src={
                    movie.poster_path === null
                        ? "https://miro.medium.com/max/800/1*hFwwQAW45673VGKrMPE2qQ.png"
                        : `https://image.tmdb.org/t/p/w200${movie.poster_path}`
                }
                alt={movie.original_title + "poster"}
            />
            <div className="absolute w-full h-[20em] top-full group-hover:top-0 transition-all flex flex-col gap-4 py-4 px-2 bg-clip-padding backdrop-filter backdrop-blur-xl bg-opacity-60 bg-black">
                <h2 className="text-2xl">{movie.original_title}</h2>
                <p className="overflow-y-scroll w-auto h-full scrollbar-hide">
                    {movie.overview}
                </p>
                <button
                    onClick={() =>
                        handleAdd(
                        movie.original_title,           // Le pasamos el titulo
                        movie.id,           // Le pasamos el id de la película de la API
                        movie.poster_path === null
                            ? "https://miro.medium.com/max/800/1*hFwwQAW45673VGKrMPE2qQ.png"
                            : `https://image.tmdb.org/t/p/w200${movie.poster_path}`
                        )            // Y el poster si lo tiene
                    }
                    className="w-full bg-green-700 hover:bg-green-800 transition-all border-2 border-black py-1 rounded-lg uppercase"
                    >
                        Favorite
                </button>
            </div>
        </div>
    );
};

export default MainCard;
```
