<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>InstaWAM!</title>
  <style>
    body {
      background-color: white;
      font-family: Arial, sans-serif;
      padding: 20px;
      color: #111;
      max-width: 900px;
      margin: 0 auto;
    }

    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 30px;
    }

    h1 {
      font-size: 2.5rem;
      color: #3f729b;
    }

    .button {
      background-color: #3f729b;
      color: white;
      border: none;
      padding: 8px 16px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
    }

    .search-bar {
      padding: 5px;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    .post {
      border: 1px solid #ddd;
      border-radius: 10px;
      padding: 15px;
      margin-bottom: 20px;
      background-color: #fafafa;
      cursor: pointer;
    }

    .post-title {
      font-weight: bold;
      font-size: 1.2rem;
      margin-bottom: 5px;
    }

    .post-user {
      font-size: 0.9rem;
      color: #777;
      margin-bottom: 10px;
    }

    .comments {
      display: none;
      margin-top: 10px;
      padding-top: 10px;
      border-top: 1px solid #ccc;
    }

    .comment {
      margin-bottom: 6px;
    }

    .comment strong {
      color: #3f729b;
    }

    .profile-section {
      display: none;
      margin-top: 30px;
    }

    .profile-section.active {
      display: block;
    }

    .profile-option {
      background-color: #ffcc00;
      color: white;
      padding: 10px;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 10px;
    }
  </style>
</head>
<body>

<header>
  <button class="button" onclick="postPrompt()">Post</button>
  <h1>InstaWAM!</h1>
  <input type="text" class="search-bar" id="searchInput" onkeyup="searchPosts()" placeholder="Search posts...">
  <button class="button" id="signInButton" onclick="signIn()">Sign In</button>
</header>

<div id="feed">
  <!-- Example posts -->
  <div class="post" onclick="toggleComments(this)">
    <div class="post-title">Laptop Screen Flickering</div>
    <div class="post-user">Posted by: tech_nerd</div>
    <p>My laptop screen keeps flickering, it’s driving me crazy. What should I do?</p>
    <div class="comments">
      <div class="comment"><strong>screen_help:</strong> Try updating your graphics drivers. That usually fixes flickering issues.</div>
      <div class="comment"><strong>fixer_123:</strong> It could be a hardware issue, but let's see if the drivers work first.</div>
    </div>
  </div>

  <div class="post" onclick="toggleComments(this)">
    <div class="post-title">Need Help With Hacking My Wi-Fi</div>
    <div class="post-user">Posted by: hacker_101</div>
    <p>How can I hack into a Wi-Fi network? I’ve tried everything.</p>
    <div class="comments">
      <div class="comment"><strong>helpful_guy:</strong> First, be ethical. If it’s your own, try using WPA2 to strengthen your password.</div>
      <div class="comment"><strong>network_expert:</strong> Cracking Wi-Fi can be illegal. I suggest you reset your router if you forgot the password.</div>
    </div>
  </div>

  <div class="post" onclick="toggleComments(this)">
    <div class="post-title">I’m Being Hacked!</div>
    <div class="post-user">Posted by: worried_user</div>
    <p>Someone is messing with my account! I think it’s a hacker. What can I do?</p>
    <div class="comments">
      <div class="comment"><strong>cytrix:</strong> Try changing your password to something complex, like 'securepassword22'. That should help.</div>
      <div class="comment"><strong>security_master:</strong> Definitely change all your passwords and enable two-factor authentication immediately.</div>
    </div>
  </div>

  <!-- More posts -->
  <div class="post" onclick="toggleComments(this)">
    <div class="post-title">Cannot Access My Account</div>
    <div class="post-user">Posted by: user_help</div>
    <p>I keep getting locked out of my account. Any ideas?</p>
    <div class="comments">
      <div class="comment"><strong>password_rescue:</strong> Try resetting your password using the email associated with the account.</div>
      <div class="comment"><strong>tech_solutions:</strong> Maybe your account is being compromised, make sure to secure it right away.</div>
    </div>
  </div>

</div>

<!-- Profile Section -->
<div class="profile-section" id="profileSection">
  <h2>Welcome, Cytrix!</h2>
  <div class="profile-option" onclick="hackAccount()">Hack Account</div>
  <div class="profile-option" onclick="showComments()">My Comments</div>
  <div class="profile-option" onclick="showPosts()">My Posts</div>
</div>

<script>
  let isSignedIn = false;
  let currentUsername = '';
  
  function signIn() {
    const username = prompt('Enter Username:');
    const password = prompt('Enter Password:');
    
    if (username === 'cytrix' && password === 'securepassword22') {
      isSignedIn = true;
      currentUsername = 'cytrix';
      alert('Signed in successfully!');
      document.getElementById('signInButton').style.display = 'none';
      const profileButton = document.createElement('button');
      profileButton.textContent = 'My Profile';
      profileButton.classList.add('button');
      profileButton.onclick = showProfile;
      document.querySelector('header').appendChild(profileButton);
    } else {
      alert('Invalid credentials. Try again.');
    }
  }

  function showProfile() {
    document.getElementById('profileSection').classList.add('active');
  }

  function hackAccount() {
    const password = prompt("Enter the password (Base64 encoded):");

    if (btoa("securepassword22") === password) {
      alert("You completed Level 3!");
    } else {
      alert("Incorrect password.");
    }
  }

  function showComments() {
    alert('Your comments: "Thanks ima try this" on the post titled "I’m Being Hacked!"');
  }

  function showPosts() {
    alert('You have no posts.');
  }

  function postPrompt() {
    const title = prompt("Post Title:");
    if (!title) return;
    const subtitle = prompt("Post Subtitle:");
    if (!subtitle) return;
    alert("You posted! (not really lmao)");
  }

  function searchPosts() {
    const searchValue = document.getElementById('searchInput').value.toLowerCase();
    const posts = document.querySelectorAll('.post');
    posts.forEach(post => {
      const title = post.querySelector('.post-title').textContent.toLowerCase();
      const content = post.querySelector('p').textContent.toLowerCase();
      if (title.includes(searchValue) || content.includes(searchValue)) {
        post.style.display = 'block';
      } else {
        post.style.display = 'none';
      }
    });
  }

  function toggleComments(postElement) {
    const comments = postElement.querySelector('.comments');
    comments.style.display = (comments.style.display === 'block') ? 'none' : 'block';
  }
</script>

</body>
</html>
