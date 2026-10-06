<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Solar System Sizing Calculator</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#f4f6f8;
    margin:0;
    padding:20px;
}

.container{
    max-width:1000px;
    margin:auto;
    background:white;
    padding:25px;
    border-radius:10px;
    box-shadow:0 0 15px rgba(0,0,0,0.1);
}

h1{
    text-align:center;
    color:#0b5ed7;
}

table{
    width:100%;
    border-collapse:collapse;
    margin-top:20px;
}

th, td{
    border:1px solid #ddd;
    padding:10px;
    text-align:center;
}

th{
    background:#0b5ed7;
    color:white;
}

input{
    width:80px;
    padding:5px;
}

.section{
    margin-top:25px;
}

button{
    background:#198754;
    color:white;
    border:none;
    padding:15px 25px;
    font-size:16px;
    border-radius:5px;
    cursor:pointer;
}

button:hover{
    background:#157347;
}

.results{
    margin-top:30px;
    background:#eef7ee;
    padding:20px;
    border-radius:8px;
}

.result-item{
    margin:10px 0;
    font-size:18px;
}

@media(max-width:768px){
    table{
        font-size:12px;
    }

    input{
        width:60px;
    }
}
</style>
</head>
<body>

<div class="container">

<h1>Solar System Sizing Calculator</h1>

<table>
<tr>
<th>Appliance</th>
<th>Quantity</th>
<th>Hours/Day</th>
<th>Power (W)</th>
</tr>

<tr>
<td>1 Ton AC</td>
<td><input type="number" id="ac1Qty" value="0"></td>
<td><input type="number" id="ac1Hr" value="8"></td>
<td>1200</td>
</tr>

<tr>
<td>1.5 Ton AC</td>
<td><input type="number" id="ac15Qty" value="0"></td>
<td><input type="number" id="ac15Hr" value="8"></td>
<td>1800</td>
</tr>

<tr>
<td>2 Ton AC</td>
<td><input type="number" id="ac2Qty" value="0"></td>
<td><input type="number" id="ac2Hr" value="8"></td>
<td>2500</td>
</tr>

<tr>
<td>Ceiling Fan</td>
<td><input type="number" id="fanQty" value="0"></td>
<td><input type="number" id="fanHr" value="12"></td>
<td>75</td>
</tr>

<tr>
<td>LED Light</td>
<td><input type="number" id="lightQty" value="0"></td>
<td><input type="number" id="lightHr" value="6"></td>
<td>15</td>
</tr>

<tr>
<td>Refrigerator</td>
<td><input type="number" id="fridgeQty" value="0"></td>
<td><input type="number" id="fridgeHr" value="10"></td>
<td>150</td>
</tr>

<tr>
<td>Washing Machine</td>
<td><input type="number" id="washQty" value="0"></td>
<td><input type="number" id="washHr" value="1"></td>
<td>500</td>
</tr>

<tr>
<td>Water Pump</td>
<td><input type="number" id="pumpQty" value="0"></td>
<td><input type="number" id="pumpHr" value="1"></td>
<td>750</td>
</tr>

<tr>
<td>TV</td>
<td><input type="number" id="tvQty" value="0"></td>
<td><input type="number" id="tvHr" value="5"></td>
<td>100</td>
</tr>

<tr>
<td>Laptop</td>
<td><input type="number" id="laptopQty" value="0"></td>
<td><input type="number" id="laptopHr" value="6"></td>
<td>60</td>
</tr>

</table>

<div class="section">

<h3>System Parameters</h3>

<p>
Peak Sun Hours:
<input type="number" id="sunHours" value="5.5" step="0.1">
</p>

<p>
System Efficiency:
<input type="number" id="efficiency" value="0.80" step="0.01">
</p>

<p>
Backup Hours Required:
<input type="number" id="backupHours" value="4">
</p>

</div>

<div style="text-align:center; margin-top:20px;">
<button onclick="calculateSolar()">Calculate Solar System</button>
</div>

<div class="results" id="results" style="display:none;">

<h2>Results</h2>

<div class="result-item">
Daily Energy Consumption:
<strong id="dailyEnergy"></strong>
</div>

<div class="result-item">
Connected Load:
<strong id="connectedLoad"></strong>
</div>

<div class="result-item">
Recommended Solar Size:
<strong id="solarSize"></strong>
</div>

<div class="result-item">
Recommended Inverter Size:
<strong id="inverterSize"></strong>
</div>

<div class="result-item">
Recommended Battery Capacity:
<strong id="batterySize"></strong>
</div>

<div class="result-item">
Estimated Roof Area:
<strong id="roofArea"></strong>
</div>

<div class="result-item">
Estimated Monthly Generation:
<strong id="monthlyGeneration"></strong>
</div>

</div>

</div>

<script>

function applianceEnergy(qty, hrs, watts){
    return (qty * hrs * watts) / 1000;
}

function applianceLoad(qty, watts){
    return (qty * watts);
}

function calculateSolar(){

    const appliances = [

        {q:"ac1Qty", h:"ac1Hr", w:1200},
        {q:"ac15Qty", h:"ac15Hr", w:1800},
        {q:"ac2Qty", h:"ac2Hr", w:2500},
        {q:"fanQty", h:"fanHr", w:75},
        {q:"lightQty", h:"lightHr", w:15},
        {q:"fridgeQty", h:"fridgeHr", w:150},
        {q:"washQty", h:"washHr", w:500},
        {q:"pumpQty", h:"pumpHr", w:750},
        {q:"tvQty", h:"tvHr", w:100},
        {q:"laptopQty", h:"laptopHr", w:60}

    ];

    let totalEnergy = 0;
    let connectedLoad = 0;

    appliances.forEach(item => {

        let qty = Number(document.getElementById(item.q).value);
        let hrs = Number(document.getElementById(item.h).value);

        totalEnergy += applianceEnergy(qty, hrs, item.w);
        connectedLoad += applianceLoad(qty, item.w);

    });

    let sunHours =
        Number(document.getElementById("sunHours").value);

    let efficiency =
        Number(document.getElementById("efficiency").value);

    let backupHours =
        Number(document.getElementById("backupHours").value);

    let solarSize =
        totalEnergy / (sunHours * efficiency);

    let inverterSize =
        (connectedLoad * 1.25) / 1000;

    let batterySize =
        (connectedLoad / 1000) * backupHours;

    let roofArea =
        solarSize * 55;

    let monthlyGeneration =
        totalEnergy * 30;

    document.getElementById("dailyEnergy").innerHTML =
        totalEnergy.toFixed(2) + " kWh/day";

    document.getElementById("connectedLoad").innerHTML =
        (connectedLoad/1000).toFixed(2) + " kW";

    document.getElementById("solarSize").innerHTML =
        Math.ceil(solarSize) + " kW";

    document.getElementById("inverterSize").innerHTML =
        inverterSize.toFixed(2) + " kW";

    document.getElementById("batterySize").innerHTML =
        batterySize.toFixed(2) + " kWh";

    document.getElementById("roofArea").innerHTML =
        roofArea.toFixed(0) + " sq.ft";

    document.getElementById("monthlyGeneration").innerHTML =
        monthlyGeneration.toFixed(0) + " kWh/month";

    document.getElementById("results").style.display = "block";
}

</script>

</body>
</html>
