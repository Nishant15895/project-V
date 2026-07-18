``` html 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="todo.css">
</head>
<body>
    <div class="content">
        <h1>Know Your City Weather</h1>
        <div class="input-container">
            <input type = "text" id = "input" placeholder = "enter city name">
            <button id="submit">Submit</button>
        </div>
        <div class="result">
            
        </div>
    </div>
    <script src="todo.js"></script>
</body>
</html>
```
``` css

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html, body{
  height: 100%;
  width: 100%;
  font-family: 'Poppins', sans-serif;
}
.content{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 100%;
    gap: 20px;
}
.input-container{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
    height: 70px;
    width: 400px;
    border-radius: 5px;
    border: 1px solid #ccc;
    box-shadow: inset 0 0 10px #ccc;
  }
  #input{

    width: 70%;
    height: 40px;
    border-radius: 5px;
    border: 1px solid #ccc;
    padding: 0 10px;
    box-shadow: inset 0 0 5px #ccc;
}
#input:focus{
    outline: none;
    border: 1px solid #4CAF50;
}
#submit{
    width: 20%;
    height: 40px;
    border-radius: 5px;
    border: 1px solid #ccc;
    background-color: #4CAF50;
    color: white;
    cursor: pointer;
}
#submit:hover{
    background-color: #45a049;
}
.result{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 10px;
    width: 400px;
    height: 300px;
    border-radius: 5px;
    border: 1px solid #ccc;
    box-shadow: inset 0 0 10px #ccc;
}
```
``` JS 
let city_name = document.querySelector("#input");
let button = document.querySelector("#submit");
const apiKey = "39f0b6323c9519fcc08fbc545cd540a8";
button.addEventListener("click", async ()=>{
    const city = city_name.value.trim();
    if(city === ""){
         alert("please enter any city name to fetch weather");
         return;
    }
    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

    try{
        const response = await fetch(url);
        const data = await response.json();
        if(!response.ok){
            alert(data.message);
            return;
        }
        displayWeather(data);
        console.log(data);
        city_name.value = "";
    } catch(error){
        console.log(error);
        alert("unable to fetch");
    }
    
})
function displayWeather(data){
    let result = document.querySelector(".result");
    result.innerHTML = `
        <h2>${data.name}</h2>
        <p><strong>Temperature:</strong> ${data.main.temp} °C</p>
        <p><strong>Feels Like:</strong> ${data.main.feels_like} °C</p>
        <p><strong>Humidity:</strong> ${data.main.humidity}%</p>
        <p><strong>Pressure:</strong> ${data.main.pressure} hPa</p>
        <p><strong>Weather:</strong> ${data.weather[0].main}</p>
        <p><strong>Description:</strong> ${data.weather[0].description}</p>
        <p><strong>Wind Speed:</strong> ${data.wind.speed} m/s</p>`;
}
```
