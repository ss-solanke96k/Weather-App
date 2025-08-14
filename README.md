<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<!--     <link rel="stylesheet" href="style.css"> -->
    <style>
        *{
    margin: 0;
    padding: 0;
    font-family: 'poppins', sans-serif;
    box-sizing: border-box;
}
body{
    background: #aacfd4;
    color: #333;
}

.card{
    width: 90%;
    max-width: 470px;
    /* height: 300px; */
    background: linear-gradient(135deg, #00feba, #5b548a);
    color: #fff;
    margin: 100px auto 0;
    border-radius: 10px;
    padding: 40px 35px;
    text-align: center;
}

.search{
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.search input{
    border: none;
    outline: none;
    background: #ebfffc;
    color: #555;
    padding: 10px 25px;
    height: 50px;
    border-radius: 30px;
    flex: 1;
    margin-right: 16px;
    font-size: 18px;
}

.search button{
    border: none;
    outline: none;
    background: #ebfffc;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    cursor: pointer;
    align-content: center;
}

.search button img{
    width: 30px;
    height: 30px;
}

.weather-icon{
    width: 170px;
    margin-top: 30px;
}

.weather h1{
    font-size: 80px;
    font-weight: 500;;
}

.weather h2{
    font-size: 45px;
    font-weight: 400;
    margin-top: -10px;
}
.details{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 20px;
    margin-top: 50px;
}
.col{
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.col img{
    width: 40px;
   margin-left: 10px;
}

.humidity, .wind{
    font-size: 28px;
    margin-top: -6px;
}
    </style>
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
