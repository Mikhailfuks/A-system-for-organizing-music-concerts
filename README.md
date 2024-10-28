<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Concert Organizer</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Concert Organizer</h1>
        <form id="concertForm">
            <input type="text" id="concertTitle" placeholder="Concert Title" required>
            <input type="text" id="artist" placeholder="Artist Name" required>
            <input type="date" id="concertDate" required>
            <input type="time" id="concertTime" required>
            <textarea id="concertDescription" placeholder="Concert Description" required></textarea>
            <button type="submit">Add Concert</button>
        </form>
        <h2>Upcoming Concerts</h2>
        <div id="concertList"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1, h2 {
    text-align: center;
}

form {
    display: flex;
    flex-direction: column;
}

input, textarea {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

.concert-item {
    background: #f8f9fa;
    margin: 10px 0;
    padding: 10px;
    border-radius: 4px;
}

.concert-item button {
    background-color: #dc3545;
    border: none;
    padding: 5px 10px;
    border-radius: 4px;
}

.concert-item button:hover {
    background-color: #c82333;
}

document.getElementById("concertForm").addEventListener("submit", function(event) {
    event.preventDefault();
    addConcert();
});

let concerts = [];

function addConcert() {
    const title = document.getElementById("concertTitle").value;
    const artist = document.getElementById("artist").value;
    const date = document.getElementById("concertDate").value;
    const time = document.getElementById("concertTime").value;
    const description = document.getElementById("concertDescription").value;

    const concert = {
        title: title,
        artist: artist,
        date: date,
        time: time,
        description: description
    };

    concerts.push(concert);
    displayConcerts();
    clearForm();
}

function displayConcerts() {
    const concertList = document.getElementById("concertList");
    concertList.innerHTML = ""; // Clear current concerts

    concerts.forEach((concert, index) => {
        const concertItem = document.createElement("div");


        concertItem.className = "concert-item";
        concertItem.innerHTML = `
            <h3>${concert.title} by ${concert.artist}</h3>
            <p>${concert.date} at ${concert.time}</p>
            <p>${concert.description}</p>
            <button onclick="deleteConcert(${index})">Delete Concert</button>
        `;
        concertList.appendChild(concertItem);
    });
}

function clearForm() {
    document.getElementById("concertTitle").value = "";
    document.getElementById("artist").value = "";
    document.getElementById("concertDate").value = "";
    document.getElementById("concertTime").value = "";
    document.getElementById("concertDescription").value = "";
}

function deleteConcert(index) {
    concerts.splice(index, 1); // Remove the concert from the array
    displayConcerts(); // Re-display the concerts
}
