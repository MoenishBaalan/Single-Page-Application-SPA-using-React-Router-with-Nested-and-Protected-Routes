# Single Page Application (SPA) using React Router with Nested and Protected Routes

## Aim:
To develop a Single Page Application in React that includes Home and Login pages, and a Dashboard section with nested pages (Profile, Settings, Notifications).

## Procedure:
Step 1: Create separate JSX files for all pages:
Home.jsx
Login.jsx
Profile.jsx
Settings.jsx
Notifications.jsx

Step 2: Create a ProtectedRoute component to check whether the user is logged in using localStorage.

Step 3: Configure routes inside App.jsx:

Public routes → Home, Login

Protected routes → Profile, Settings, Notifications inside Dashboard

Add navigation using <Link> or custom buttons.

Step 4: Test the SPA:

Try accessing dashboard pages without login → should redirect to Login

After login, dashboard pages should open normally

Verify that routing happens without page reload, confirming SPA behavior.

## Program:
```
App.jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { useState } from "react";
import Home from "./testqs/home";
import Login from "./testqs/login";
import Dashboard from "./testqs/dashboard";
import Profile from "./testqs/profile";
import Settings from "./testqs/setting";
import Notifications from "./testqs/notis";
import ProtectedRoute from "./testqs/protectedRoutes";

function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  return (
    <BrowserRouter>
      <Routes>

        <Route path="/" element={<Home />} />

        <Route
          path="/login"
          element={<Login setIsLoggedIn={setIsLoggedIn} />}
        />

        {}
        <Route
          path="/dashboard"
          element={
            <ProtectedRoute isLoggedIn={isLoggedIn}>
              <Dashboard />
            </ProtectedRoute>
          }
        >
          {}
          <Route path="profile" element={<Profile />} />
          <Route path="settings" element={<Settings />} />
          <Route path="notifications" element={<Notifications />} />
        </Route>

      </Routes>
    </BrowserRouter>
  );
}

export default App;
```
```
protectedRoutes.jsx
import { Navigate } from "react-router-dom";

function ProtectedRoute({ isLoggedIn, children }) {
  if (!isLoggedIn) {
    return <Navigate to="/login" replace />;
  }
  return children;
}

export default ProtectedRoute;
```
```
home.jsx
import { Link } from "react-router-dom";

function Home() {
  return (
    <div>
      <h1>Home Page</h1>
      <Link to="/login">Go to Login</Link>
    </div>
  );
}

export default Home;
```
```
login.jsx
import { useNavigate } from "react-router-dom";

function Login({ setIsLoggedIn }) {
  const navigate = useNavigate();

  function handleLogin() {
    setIsLoggedIn(true);
    navigate("/dashboard");
  }

  return (
    <div>
      <h1>Login</h1>
      <button onClick={handleLogin}>Login</button>
    </div>
  );
}

export default Login;
```
```
dashboard.jsx
import { Link, Outlet } from "react-router-dom";

function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>

      <nav>
        <Link to="profile">Profile</Link> |{" "}
        <Link to="settings">Settings</Link> |{" "}
        <Link to="notifications">Notifications</Link>
      </nav>

      <hr />

      <Outlet /> {}
    </div>
  );
}

export default Dashboard;
```
```
profile.jsx
function Profile() {
  return <h2>Profile Page</h2>;
}

export default Profile;
```
```
setting.jsx
function Settings() {
  return <h2>Settings Page</h2>;
}

export default Settings;
```
```
notis.jsx
function Notifications() {
  return <h2>Notifications Page</h2>;
}

export default Notifications;
```

## Output:

<img width="1192" height="902" alt="image" src="https://github.com/user-attachments/assets/6c465a1f-6d4d-41d4-a581-34c89252a5f2" />

<img width="1165" height="876" alt="image" src="https://github.com/user-attachments/assets/78f846d3-0e06-4312-90fd-f57f38dfa2bb" />

<img width="836" height="805" alt="image" src="https://github.com/user-attachments/assets/12d2fcd9-fadc-4bfb-88ac-4b1133c45f52" />

<img width="722" height="522" alt="image" src="https://github.com/user-attachments/assets/8b31ff08-8d6b-4d76-aec8-7e4aef723da4" />

<img width="755" height="712" alt="image" src="https://github.com/user-attachments/assets/ed0332f2-4c32-4e6a-b47d-8abd11a7079b" />

<img width="958" height="607" alt="image" src="https://github.com/user-attachments/assets/69c5abb2-c120-49ae-ac60-02d12e8ca6e4" />

## Result:
A Single Page Application (SPA) was successfully developed using React Router.




