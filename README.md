# Sophiphi-s-shop
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sophiphi's Shop</title>
    <style>
        :root {
            --primary: #ff6b6b;
            --primary-hover: #ff5252;
            --bg: #f8f9fa;
            --card-bg: #ffffff;
            --text: #2d3436;
            --border: #dfe6e9;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            background: var(--card-bg);
            padding: 2.5rem;
            border-radius: 12px;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.05);
            width: 100%;
            max-width: 400px;
            text-align: center;
            box-sizing: border-box;
        }

        h1 {
            color: var(--primary);
            margin-bottom: 1.5rem;
            font-size: 2rem;
        }

        h2 {
            margin-bottom: 1.5rem;
            font-size: 1.5rem;
            color: #4a4a4a;
        }

        .form-group {
            margin-bottom: 1.25rem;
            text-align: left;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            font-size: 0.9rem;
        }

        input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--border);
            border-radius: 6px;
            font-size: 1rem;
            box-sizing: border-box;
            transition: border-color 0.2s;
        }

        input:focus {
            outline: none;
            border-color: var(--primary);
        }

        button {
            width: 100%;
            padding: 0.75rem;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s;
            margin-top: 0.5rem;
        }

        button:hover {
            background-color: var(--primary-hover);
        }

        .toggle-text {
            margin-top: 1.5rem;
            font-size: 0.9rem;
            color: #747d8c;
        }

        .toggle-text span {
            color: var(--primary);
            cursor: pointer;
            font-weight: 600;
        }

        .hidden {
            display: none !important;
        }

        .admin-dashboard, .shop-dashboard {
            max-width: 800px;
            width: 90%;
            text-align: left;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-top: 1.5rem;
        }

        .card {
            background: #f1f2f6;
            padding: 1rem;
            border-radius: 8px;
            border-left: 4px solid var(--primary);
        }

        .error-msg {
            color: #ff4757;
            font-size: 0.85rem;
            margin-top: 0.5rem;
            min-height: 18px;
        }
    </style>
</head>
<body>

    <!-- Landing / Welcome Entry Page -->
    <div id="landing-page" class="container">
        <h1>sophiphi’s shop</h1>
        <p>Welcome to the ultimate shopping experience.</p>
        <button onclick="showAuthPage()">Enter Shop</button>
    </div>

    <!-- Auth Page (Login / Sign Up) -->
    <div id="auth-page" class="container hidden">
        <h1 id="auth-title">Log In</h1>
        
        <!-- Step 1: Username Input -->
        <div id="username-stage">
            <div class="form-group">
                <label for="username">Username</label>
                <input type="text" id="username" placeholder="Enter username">
                <div id="username-error" class="error-msg"></div>
            </div>
            <button onclick="handleUsernameSubmit()">Continue</button>
        </div>

        <!-- Step 2: Password Input (Hidden initially) -->
        <div id="password-stage" class="hidden">
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" id="password" placeholder="Enter password">
                <div id="password-error" class="error-msg"></div>
            </div>
            <button onclick="handlePasswordSubmit()">Sign In</button>
        </div>

        <p class="toggle-text" id="toggle-container">
            Don't have an account? <span onclick="toggleAuthMode()">Create an account</span>
        </p>
    </div>

    <!-- Admin Page Dashboard -->
    <div id="admin-page" class="container admin-dashboard hidden">
        <h1>Admin Control Panel</h1>
        <h2>Welcome back, Sophiphi2016</h2>
        
        <div class="grid">
            <div class="card">
                <h3>Website Settings</h3>
                <p>Edit layout, themes, and global store inventory configurations.</p>
                <button style="width: auto; padding: 0.5rem 1rem;">Edit Website</button>
            </div>
            <div class="card">
                <h3>User Notifications</h3>
                <p><strong>🔔 3 New Notifications</strong></p>
                <p style="font-size: 0.85rem; color: #57606f;">User 'Alex99' requested a password reset.</p>
            </div>
            <div class="card">
                <h3>Store Information</h3>
                <p>Total Users: 1,240<br>Active Sessions: 14</p>
            </div>
        </div>
        <button onclick="logout()" style="margin-top: 2rem; width: auto; padding: 0.5rem 1.5rem; background: #747d8c;">Log Out</button>
    </div>

    <!-- Standard Shop Welcome Page -->
    <div id="shop-page" class="container shop-dashboard hidden">
        <h1>Welcome to my shop</h1>
        <p>You have successfully logged into your account. Explore our products and exclusive deals below!</p>
        <div class="grid">
            <div class="card" style="border-left-color: #2ed573;">
                <h3>New Arrivals</h3>
                <p>Check out the fresh inventory curated just for you.</p>
            </div>
            <div class="card" style="border-left-color: #2ed573;">
                <h3>Your Cart</h3>
                <p>Your shopping cart is currently empty.</p>
            </div>
        </div>
        <button onclick="logout()" style="margin-top: 2rem; width: auto; padding: 0.5rem 1.5rem; background: #747d8c;">Log Out</button>
    </div>

    <script>
        // Track the current mode ('login' or 'signup') and target user state
        let authMode = 'login'; 
        let currentUsername = '';

        // Temporary user database mock for client-side evaluation
        const existingUsers = {
            'Sophiphi2016': '2016',
            'user1': 'password123'
        };

        function showAuthPage() {
            document.getElementById('landing-page').classList.add('hidden');
            document.getElementById('auth-page').classList.remove('hidden');
        }

        function toggleAuthMode() {
            const title = document.getElementById('auth-title');
            const toggleContainer = document.getElementById('toggle-container');
            resetForm();

            if (authMode === 'login') {
                authMode = 'signup';
                title.innerText = 'Create Account';
                toggleContainer.innerHTML = 'Already have an account? <span onclick="toggleAuthMode()">Log In</span>';
            } else {
                authMode = 'login';
                title.innerText = 'Log In';
                toggleContainer.innerHTML = 'Don\'t have an account? <span onclick="toggleAuthMode()">Create an account</span>';
            }
        }

        function handleUsernameSubmit() {
            const usernameInput = document.getElementById('username').value.trim();
            const errorDiv = document.getElementById('username-error');
            errorDiv.innerText = '';

            if (!usernameInput) {
                errorDiv.innerText = 'Username cannot be empty.';
                return;
            }

            currentUsername = usernameInput;

            if (authMode === 'login') {
                // Routing logic condition based on account type
                if (currentUsername === 'Sophiphi2016') {
                    // Redirects directly to admin verification step
                    showPasswordStage();
                } else if (existingUsers[currentUsername]) {
                    // Standard user credentials found
                    showPasswordStage();
                } else {
                    errorDiv.innerText = 'Username not found. Try creating an account.';
                }
            } else {
                // Sign Up execution path
                if (existingUsers[currentUsername]) {
                    errorDiv.innerText = 'Username is already taken.';
                } else {
                    showPasswordStage();
                }
            }
        }

        function showPasswordStage() {
            document.getElementById('username-stage').classList.add('hidden');
            document.getElementById('password-stage').classList.remove('hidden');
            document.getElementById('toggle-container').classList.add('hidden');
        }

        function handlePasswordSubmit() {
            const passwordInput = document.getElementById('password').value;
            const errorDiv = document.getElementById('password-error');
            errorDiv.innerText = '';

            if (authMode === 'login') {
                // Verify password against criteria matching user routing profile
