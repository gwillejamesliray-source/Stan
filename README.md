<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Medical Awareness Hub</title>
    <style>
        body { 
            font-family: 'Arial', sans-serif; 
            text-align: center; 
            margin: 0; 
            padding: 0; 
            background-color: #e8f4f8;
        }
        header { 
            background: #2a9d8f; 
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
            background: #ffffff;
            border-radius: 10px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
            display: inline-block; 
            margin: 20px; 
            padding: 20px; 
            width: 320px;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .product:hover {
            transform: scale(1.05);
            box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.3);
        }
        .product img {
            width: 100%;
            border-radius: 5px;
        }
        button { 
            background: #264653; 
            color: white; 
            border: none; 
            padding: 10px 15px; 
            cursor: pointer; 
            font-size: 16px;
            border-radius: 5px;
            transition: background 0.3s;
        }
        button:hover { 
            background: #1b3330; 
        }
        #support {
            background: #ffffff;
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
            background: #ffffff;
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
    <h1>🩺 Medical Awareness Hub</h1>
    <p>Educate • Prevent • Protect</p>
</header>

<div class="container">
    <div class="product">
        <img src="https://images.unsplash.com/photo-1588776814546-1ffcf47267a5" alt="Heart Health">
        <h2>Heart Health Awareness</h2>
        <p>Learn how to prevent heart disease through healthy lifestyle choices.</p>
        <button onclick="addSupport('Heart Health Awareness')">Support This Cause</button>
    </div>

    <div class="product">
        <img src="https://images.unsplash.com/photo-1587502537745-84d5e70c8b86" alt="Mental Health">
        <h2>Mental Health Awareness</h2>
        <p>Break the stigma and understand the importance of mental well-being.</p>
        <button onclick="addSupport('Mental Health Awareness')">Support This Cause</button>
    </div>

    <div class="product">
        <img src="https://images.unsplash.com/photo-1584467735871-bc1a0a35fdd8" alt="Hygiene Awareness">
        <h2>Hygiene & Disease Prevention</h2>
        <p>Simple hygiene practices can save lives and prevent infections.</p>
        <button onclick="addSupport('Hygiene Awareness')">Support This Cause</button>
    </div>
</div>

<div id="support">
    <h2>🤝 Supported Awareness Topics</h2>
    <ul id="support-items"></ul>
    <button onclick="pledge()">Make a Pledge</button>
</div>

<div id="feedback">
    <h2>💬 Share Your Health Message</h2>
    <textarea id="feedback-text" placeholder="Share your thoughts or awareness message..."></textarea>
    <button onclick="submitFeedback()">Submit</button>
    <ul id="feedback-list"></ul>
</div>

<script>
    let supportList = [];

    function addSupport(topic) {
        supportList.push(topic);
        updateSupport();
    }

    function updateSupport() {
        const list = document.getElementById('support-items');
        list.innerHTML = '';
        supportList.forEach(item => {
            const li = document.createElement('li');
            li.textContent = item;
            list.appendChild(li);
        });
    }

    function pledge() {
        if (supportList.length === 0) {
            alert('Please support at least one awareness topic.');
            return;
        }
        alert('🙏 Thank you for supporting medical awareness!');
        supportList = [];
        updateSupport();
    }

    function submitFeedback() {
        const feedbackText = document.getElementById('feedback-text').value;
        if (feedbackText.trim() === '') {
            alert('Please enter a message before submitting.');
            return;
        }
        const feedbackList = document.getElementById('feedback-list');
        const li = document.createElement('li');
        li.textContent = feedbackText;
        feedbackList.appendChild(li);

        let feedbackArray = JSON.parse(localStorage.getItem('healthFeedback')) || [];
        feedbackArray.push(feedbackText);
        localStorage.setItem('healthFeedback', JSON.stringify(feedbackArray));

        document.getElementById('feedback-text').value = '';
    }

    window.onload = function() {
        let feedbackArray = JSON.parse(localStorage.getItem('healthFeedback')) || [];
        const feedbackList = document.getElementById('feedback-list');
        feedbackArray.forEach(feedback => {
            const li = document.createElement('li');
            li.textContent = feedback;
            feedbackList.appendChild(li);
        });
    }
</script>

</body>
</html>
