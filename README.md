
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dinesh Taxi Booking</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 80%;
            margin: 20px auto;
            padding: 20px;
            background: white;
            box-shadow: 0px 0px 10px gray;
            border-radius: 10px;
        }
        input, button {
            padding: 10px;
            margin: 10px;
            width: 80%;
            font-size: 16px;
        }
        button {
            background-color: #28a745;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        #map {
            width: 100%;
            height: 300px;
            margin-top: 10px;
        }
        #rideHistory {
            text-align: left;
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>🚖 Dinesh Taxi Booking</h2>
        <p>Book your taxi with real-time tracking</p>
        
        <form>
            <input type="text" id="pickup" placeholder="Enter Pickup Location" required><br>
            <input type="text" id="drop" placeholder="Enter Drop Location" required><br>
            <label>Select Travel Date:</label>
            <input type="date" id="travelDate" required><br>
            <button type="button" onclick="calculateFare()">Calculate Fare</button>
            <p id="fare"></p>
            <button type="button" onclick="bookTaxi()">Book Now</button>
        </form>

        <h3 id="status"></h3>
        <div id="map"></div>

        <h3>📜 Ride History</h3>
        <ul id="rideHistory"></ul>

        <h3>💳 Make Payment</h3>
        <button onclick="makePayment()">Pay with Razorpay</button>
    </div>

    <script>
        function calculateFare() {
            let pickup = document.getElementById('pickup').value;
            let drop = document.getElementById('drop').value;

            if (pickup && drop) {
                let distance = Math.floor(Math.random() * 20) + 5; // Random distance between 5-25 km
                let fare = distance * 10; // ₹10 per km
                document.getElementById('fare').innerHTML = "Estimated Fare: ₹" + fare;
                return fare;
            } else {
                alert("Please enter both pickup and drop locations.");
                return 0;
            }
        }

        function bookTaxi() {
            let pickup = document.getElementById('pickup').value;
            let drop = document.getElementById('drop').value;
            let travelDate = document.getElementById('travelDate').value;
            let fare = calculateFare();

            if (pickup && drop && travelDate) {
                let rideDetails = `🚖 ${pickup} ➡ ${drop} | Date: ${travelDate} | Fare: ₹${fare}`;
                document.getElementById('status').innerHTML = "✅ Taxi booked! " + rideDetails;

                // Save to ride history
                let history = localStorage.getItem('rideHistory') ? JSON.parse(localStorage.getItem('rideHistory')) : [];
                history.push(rideDetails);
                localStorage.setItem('rideHistory', JSON.stringify(history));

                updateRideHistory();

                // Send Email Confirmation (Opens email client)
                window.location.href = `mailto:avidinesh99@gmail.com?subject=Taxi Booking Confirmation&body=${rideDetails}`;

                alert("Taxi booking confirmed! 🚖");
            } else {
                alert("Please fill in all details.");
            }
        }

        function updateRideHistory() {
            let history = localStorage.getItem('rideHistory') ? JSON.parse(localStorage.getItem('rideHistory')) : [];
            let rideHistoryList = document.getElementById('rideHistory');
            rideHistoryList.innerHTML = "";
            history.forEach(ride => {
                let li = document.createElement('li');
                li.textContent = ride;
                rideHistoryList.appendChild(li);
            });
        }

        function makePayment() {
            alert("Redirecting to Razorpay Payment Gateway...");
            window.open("https://razorpay.com/", "_blank");
        }

        function initMap() {
            let map = new google.maps.Map(document.getElementById('map'), {
                center: { lat: 12.9716, lng: 77.5946 }, // Default location (Chennai)
                zoom: 12
            });
        }

        // Load ride history on page load
        window.onload = updateRideHistory;
    </script>
    
    <!-- Google Maps API -->
    <script async defer src=https://console.cloud.google.com/

</body>
</html>
