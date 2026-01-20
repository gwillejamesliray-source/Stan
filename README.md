<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tote Bag Store</title>
    <style>
        body { 
            font-family: 'Arial', sans-serif; 
            text-align: center; 
            margin: 0; 
            padding: 0; 
            background-color: #f5e1c8;
        }
        header { 
            background: #d2b48c; 
            color: white; 
            padding: 20px; 
            font-size: 24px;
        }
        .container { 
            padding: 40px; 
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
        }
        .product { 
            background: #fdf3e7;
            border-radius: 10px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
            display: inline-block; 
            margin: 20px; 
            padding: 20px; 
            border: 1px solid #ddd;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .product:hover {
            transform: scale(1.05);
            box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.3);
        }
        .product img {
            width: 300px;
            height: auto;
            max-width: 100%;
            border-radius: 5px;
        }
        button { 
            background: #007bff; 
            color: white; 
            border: none; 
            padding: 10px 15px; 
            cursor: pointer; 
            font-size: 16px;
            border-radius: 5px;
            transition: background 0.3s;
        }
        button:hover { 
            background: #0056b3; 
        }
        #cart {
            background: #fdf3e7;
            padding: 20px;
            margin: 20px auto;
            width: 50%;
            border-radius: 10px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
        }
        ul {
            list-style: none;
            padding: 0;
        }
        ul li {
            font-size: 18px;
            padding: 5px;
        }
        #feedback {
            background: #fdf3e7;
            padding: 20px;
            margin: 20px auto;
            width: 50%;
            border-radius: 10px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
            text-align: left;
        }
        textarea {
            width: 100%;
            height: 80px;
            padding: 10px;
            margin-top: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            resize: none;
        }
    </style>
</head>
<body>
    <header>
        <h1>👜 Welcome to Tote Bag Store</h1>
    </header>
    <div class="container">
        <div class="product">
            <img src="https://cdn.thewirecutter.com/wp-content/media/2023/11/totebags-2048px-cuyanabagexterior.jpg?auto=webp&quality=75&width=1024" alt="Stylish Tote Bag">
            <h2>Stylish Tote Bag</h2>
            <p><strong>$15.00</strong></p>
            <button onclick="addToCart('Stylish Tote Bag', 15)">Add to Cart</button>
        </div>
        <div class="product">
            <img src="https://www.ecobags.com/cdn/shop/products/ECOBAGS-CAN-501d-Edit.jpg?v=1670871835" alt="Eco-friendly Tote">
            <h2>Eco-friendly Tote</h2>
            <p><strong>$18.00</strong></p>
            <button onclick="addToCart('Eco-friendly Tote', 18)">Add to Cart</button>
        </div>
    </div>
    
    <div id="cart">
        <h2>🛒 Shopping Cart</h2>
        <ul id="cart-items"></ul>
        <p><strong>Total: $<span id="total-price">0.00</span></strong></p>
        <button onclick="purchase()">Purchase</button>
    </div>

    <div id="feedback">
        <h2>💬 Leave Your Feedback</h2>
        <textarea id="feedback-text" placeholder="Write your feedback here..."></textarea>
        <button onclick="submitFeedback()">Submit</button>
        <ul id="feedback-list"></ul>
    </div>

    <script>
        let cart = [];
        function addToCart(name, price) {
            cart.push({ name, price });
            updateCart();
        }
        function updateCart() {
            const cartItems = document.getElementById('cart-items');
            const totalPrice = document.getElementById('total-price');
            cartItems.innerHTML = '';
            let total = 0;
            cart.forEach(item => {
                const li = document.createElement('li');
                li.textContent = `${item.name} - $${item.price.toFixed(2)}`;
                cartItems.appendChild(li);
                total += item.price;
            });
            totalPrice.textContent = total.toFixed(2);
        }
        function purchase() {
            if (cart.length === 0) {
                alert('Your cart is empty!');
                return;
            }
            alert('🎉 Thank you for your purchase!');
            cart = [];
            updateCart();
        }
        function submitFeedback() {
    const feedbackText = document.getElementById('feedback-text').value;
    if (feedbackText.trim() === '') {
        alert('Please enter your feedback before submitting.');
        return;
    }
    const feedbackList = document.getElementById('feedback-list');
    const li = document.createElement('li');
    li.textContent = feedbackText;
    feedbackList.appendChild(li);
    document.getElementById('feedback-text').value = '';
    
    // Store feedback in local storage to persist across page reloads
    let feedbackArray = JSON.parse(localStorage.getItem('feedbacks')) || [];
    feedbackArray.push(feedbackText);
    localStorage.setItem('feedbacks', JSON.stringify(feedbackArray));
}

// Load stored feedback on page load
window.onload = function() {
    let feedbackArray = JSON.parse(localStorage.getItem('feedbacks')) || [];
    const feedbackList = document.getElementById('feedback-list');
    feedbackArray.forEach(feedback => {
        const li = document.createElement('li');
        li.textContent = feedback;
        feedbackList.appendChild(li);
    });
}
            const feedbackList = document.getElementById('feedback-list');
            const li = document.createElement('li');
            li.textContent = feedbackText;
            feedbackList.appendChild(li);
            document.getElementById('feedback-text').value = '';
        
    </script>
</body>
</html>
