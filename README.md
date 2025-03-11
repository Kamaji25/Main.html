<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Centring Rental App</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            text-align: center;
            background: linear-gradient(120deg, #4e54c8, #8f94fb);
            color: white;
        }

        /* Welcome Screen */
        .welcome-screen {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: rgba(0, 0, 0, 0.5);
            position: fixed;
            width: 100%;
            transition: opacity 1s ease-out;
        }

        .welcome-screen h1 {
            font-size: 2.5em;
            margin-bottom: 20px;
            animation: fadeIn 2s ease-in-out;
        }

        #startButton {
            padding: 15px 30px;
            font-size: 18px;
            border: none;
            background: #ffcc00;
            color: black;
            cursor: pointer;
            border-radius: 5px;
            animation: bounce 1s infinite alternate;
        }

        #startButton:hover {
            background: #ff9900;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes bounce {
            from { transform: translateY(0); }
            to { transform: translateY(-10px); }
        }

        /* Main Container */
        .main-container {
            display: none;
            padding: 20px;
        }

        .container {
            width: 90%;
            max-width: 800px;
            background: white;
            padding: 20px;
            margin: auto;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
            color: black;
            animation: fadeIn 1s ease-in;
        }

        form {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        input, select, button {
            padding: 10px;
            font-size: 16px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        button {
            background: green;
            color: white;
            cursor: pointer;
        }

        button:hover {
            background: darkgreen;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: center;
        }

        th {
            background: #333;
            color: white;
        }

        .delete-btn {
            background: red;
            color: white;
            border: none;
            padding: 5px 10px;
            cursor: pointer;
        }

        .delete-btn:hover {
            background: darkred;
        }
    </style>
</head>
<body>

    <div class="welcome-screen" id="welcomeScreen">
        <h1>Welcome to Centring Rental App</h1>
        <button id="startButton">Get Started</button>
    </div>

    <div class="main-container" id="mainContainer">
        <h1>Centring Rental App</h1>
        <p>Manage rental products and customer details</p>

        <div class="container">
            <h2>Customer Details</h2>
            <form id="customerForm">
                <input type="text" id="customerName" placeholder="Customer Name" required>
                <input type="number" id="customerPhone" placeholder="Phone Number" required>
                <select id="rentalProduct">
                    <option value="5 Feet Box">5 Feet Box</option>
                    <option value="10 Feet Box">10 Feet Box</option>
                    <option value="Vase">Vase</option>
                    <option value="Side Plates">Side Plates</option>
                </select>
                <input type="number" id="quantity" placeholder="Quantity" required>
                <label>Renting Date:</label>
                <input type="date" id="rentingDate" required>
                <label>Returning Date:</label>
                <input type="date" id="returningDate" required>
                <button type="submit">Add Rental</button>
            </form>

            <h2>Rented Products</h2>
            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Phone</th>
                        <th>Product</th>
                        <th>Quantity</th>
                        <th>Renting Date</th>
                        <th>Returning Date</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody id="rentalList"></tbody>
            </table>
        </div>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const welcomeScreen = document.getElementById("welcomeScreen");
            const startButton = document.getElementById("startButton");
            const mainContainer = document.getElementById("mainContainer");

            // Show main app when start button is clicked
            startButton.addEventListener("click", () => {
                welcomeScreen.style.opacity = "0";
                setTimeout(() => {
                    welcomeScreen.style.display = "none";
                    mainContainer.style.display = "block";
                }, 1000);
            });

            const form = document.getElementById("customerForm");
            const rentalList = document.getElementById("rentalList");

            form.addEventListener("submit", (e) => {
                e.preventDefault();

                const name = document.getElementById("customerName").value;
                const phone = document.getElementById("customerPhone").value;
                const product = document.getElementById("rentalProduct").value;
                const quantity = document.getElementById("quantity").value;
                const rentingDate = document.getElementById("rentingDate").value;
                const returningDate = document.getElementById("returningDate").value;

                const row = document.createElement("tr");
                row.innerHTML = `
                    <td>${name}</td>
                    <td>${phone}</td>
                    <td>${product}</td>
                    <td>${quantity}</td>
                    <td>${rentingDate}</td>
                    <td>${returningDate}</td>
                    <td><button class="delete-btn">Remove</button></td>
                `;

                row.querySelector(".delete-btn").addEventListener("click", () => {
                    rentalList.removeChild(row);
                });

                rentalList.appendChild(row);
                form.reset();
            });
        });
    </script>

</body>
</html>
