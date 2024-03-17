<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Application</title>
    <style>
        body{
            background: #222 ;
            background-size: cover;
            font-family: Arial, sans-serif;
            color: #fff;
            margin: 0;
            padding: 0;
        }
       
       
        .container {
            text-align: center;
            margin-top: 100px;
        }

        h1 {
            margin-bottom: 20px;
        }
        .container{
            width:90%;
            max-width: 470px;
            background:linear-gradient(135deg, #00feba,#5b548a);
            margin: auto;
            border-radius: 20px;
            padding: 40px 35px;
            text-align: center;
        }
        .search{
            width: 100%;
            display:flex;
            align-items: center;
            justify-content: space-between;
        }

        #cityInput {
            border: 0;
            outline: 0;
            background: #ebfffc;
            color:#555;
            padding: 10px 25px;
            height:60px;
            border-radius: 30px;
            flex: 1;
            margin-right: 16px;
            font-size: 18px;
        }

        #weatherInfo {
            margin-top: 20px;
            border: 1px solid #ccc;
            padding: 10px;
        }
        .icon {
            width: 150px; /* Adjust the size of the icon */
            height: 150px; /* Adjust the size of the icon */
            margin-right: 10px;
        }
        .detail {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        .col {
            display: flex;
            align-items: center;
        }
        .col img {
            width: 120px; /* Adjust the size of the icon */
            height: 120px; /* Adjust the size of the icon */
            margin-right: 10px;
        }
    </style>
</head>
<body>
    
    <h1>Weather Application</h1>
    <div class="container">
        <div class="search">
            <input type="text" id="cityInput" placeholder="Enter city name or country name">
            <button id="getWeatherBtn">Get Weather</button>
        </div>
        <div id="weatherInfo"></div>
        <div class="weather">
            <img src="th (1).jfif" class="icon">
            <h1 class="temp">22 celcius</h1>
            <h2 class="city">new york</h2>
            <div class="detail">
                <div class="col">
                    <img src="humidity-rain-drop-weather-condition-news-app-51123.webp" class="humidity-icon">
                    <div>
                        <p class="humidity">50%</p>
                        <p>humidity</p>
                    </div>
                </div>
                <div class="col">
                    <img src="th.jfif" class="wind-icon">
                    <div>
                        <p class="wind">15 km/hr</p>
                        <p>wind speed</p>
                    </div>
                </div>
            </div>
        </div>
    </div>



    <script>
        document.getElementById('getWeatherBtn').addEventListener('click', function() {
            var city = document.getElementById('cityInput').value;
            var apiKey = '6c101388096bf122d0fa0d764aa13d43';
            var apiUrl = 'https://api.openweathermap.org/data/2.5/weather?q=' + city + '&appid=' + apiKey;
            var xhr = new XMLHttpRequest();

            xhr.onreadystatechange = function() {
                if (xhr.readyState === XMLHttpRequest.DONE) {
                    if (xhr.status === 200) {
                        var data = JSON.parse(xhr.responseText);
                        var weatherInfo = 'Weather in ' + city + ': ' + data.weather[0].description;
                        weatherInfo += ', Temperature: ' + (data.main.temp - 273.15).toFixed(2) + '°C';
                        document.getElementById('weatherInfo').innerHTML = weatherInfo;
                        document.querySelector('.temp').innerText = (data.main.temp - 273.15).toFixed(2) + '°C';
                        document.querySelector('.city').innerText = city;
                        document.querySelector('.humidity').innerText = data.main.humidity + '%';
                        document.querySelector('.wind').innerText = data.wind.speed + ' km/hr';
                        var iconCode = data.weather[0].icon;
                        var iconUrl = 'http://openweathermap.org/img/wn/' + iconCode + '.png';
                        document.querySelector('.icon').setAttribute('src', iconUrl);

                        // Update humidity icon based on weather condition (example: rain)
                        // We can't directly fetch specific icons for humidity, so we'll leave it unchanged
                        // You can replace 'humidity-icon.png' with the appropriate image for humidity
                        // document.querySelector('.humidity-icon').setAttribute('src', 'humidity-icon.png');

                        // Update wind speed icon based on weather condition (example: windy)
                        if (data.wind.speed > 10) {
                            document.querySelector('.wind-icon').setAttribute('src', 'windy-icon.png');
                        } else {
                            document.querySelector('.wind-icon').setAttribute('src', 'th.jfif');
                        }
                    } else {
                        document.getElementById('weatherInfo').innerText = 'Error fetching weather information. Please try again.';
                    }
                }
            };

            xhr.open('GET', apiUrl, true);
            xhr.send();
        });
    </script>
</body>m
</html>
