<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="card">
        <div class="search">
            <input type="text" placeholder="Enter city name" spellcheck="false">
        <button><img src="images\search.png" alt="Search"width="100px" height="100px">
            <br><br>
        </button>
        </div>
        <div class="weather">
            <img src="images\weatherbg.png" height="170px" width="170px" alt="Weather Icon">
            <h1 class="temp">22°C</h1>
            <h2 class="city">Amravati</h2>
            <div class="details">
                <div class="col">
                    <img src="images\humidity.png">
                    <div>
                        <p class="humidity">50%</p>
                    <p>Humidity</p>
                    </div>
                </div>
                <div class="col">
                    <img src="images\wind.png">
                    <div>
                    <p class="wind">15 km/h</p>
                    <p>Wind Speed</p>
            </div>
        </div>
    </div>
</div>
    
<script>
const apiKey = "c55ce1f8fa937e4dedee1c273e9896ed";

async function checkwhethere(city) {
    const apiUrl = `https://api.openweathermap.org/data/2.5/weather?units=metric&q=${city}&appid=${apiKey}`;
    try {
        const response = await fetch(apiUrl);
        const data = await response.json();
        console.log(data);
        if (data.cod !== 200) {
            document.querySelector(".city").innerHTML = "City not found";
            document.querySelector(".temp").innerHTML = "--";
            document.querySelector(".humidity").innerHTML = "--";
            document.querySelector(".wind").innerHTML = "--";
            return;
        }
        document.querySelector(".city").innerHTML = data.name;
        document.querySelector(".temp").innerHTML = `${Math.round(data.main.temp)}°C`;
        document.querySelector(".humidity").innerHTML = `${data.main.humidity}%`;
        document.querySelector(".wind").innerHTML = `${data.wind.speed} km/h`;
    } catch (error) {
        console.error("Error fetching weather:", error);
    }
}

// Enable search button to fetch weather for entered city
document.querySelector("button").addEventListener("click", function() {
    const city = document.querySelector("input").value.trim();
    if (city) {
        checkwhethere(city);
    }
});

// Optionally, show default city on load
</script>

</body>
</html>
