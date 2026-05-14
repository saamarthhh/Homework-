<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>ระบบส่งการบ้าน</title>
  <script src="https://apis.google.com/js/platform.js" async defer></script>
  <meta name="google-signin-client_id" content="YOUR_CLIENT_ID.apps.googleusercontent.com">
  <style>
    body { font-family: 'TH SarabunPSK', sans-serif; background: #f0f8ff; text-align: center; }
    .login-box { margin-top: 100px; }
  </style>
</head>
<body>
  <div class="login-box">
    <h2>เข้าสู่ระบบส่งการบ้าน</h2>
    <div class="g-signin2" data-onsuccess="onSignIn"></div>
  </div>

  <script>
    function onSignIn(googleUser) {
      var profile = googleUser.getBasicProfile();
      console.log("Logged in: " + profile.getEmail());
      // ส่ง token ไป backend เพื่อตรวจสอบสิทธิ์
    }
  </script>
</body>
<div class="classroom-container">
  <h2>เลือกห้องเรียน</h2>
  <div class="room-card">ห้อง 2/1 <img src="qr_21.png"></div>
  <div class="room-card">ห้อง 2/2 <img src="qr_22.png"></div>
  <div class="room-card">ห้อง 2/3 <img src="qr_22.png"></div>
  <div class="room-card">ห้อง 2/4 <img src="qr_22.png"></div>
  <div class="room-card">ห้อง 2/5 <img src="qr_22.png"></div>
  <div class="room-card">ห้อง 2/6 <img src="qr_22.png"></div>
  <div class="room-card">ห้อง 2/7 <img src="qr_22.png"></div>
  <div class="room-card">ห้อง 2/8 <img src="qr_22.png"></div>
  <div class="room-card">ห้อง 2/9 <img src="qr_22.png"></div>
</div>

<style>
  .classroom-container { display: flex; flex-wrap: wrap; justify-content: center; }
  .room-card { background: #ffe4f0; margin: 10px; padding: 20px; border-radius: 10px; }
  .room-card img { width: 100px; }
</style>
<form action="upload.php" method="post" enctype="multipart/form-data">
  <label>เลือกไฟล์งาน:</label>
  <input type="file" name="assignment" accept=".pdf,.doc,.docx,.ppt,.jpg,.png">
  <button type="submit">ส่งงาน</button>
</form>
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    role ENUM('student','teacher') NOT NULL,
    profile_pic VARCHAR(255), -- เก็บ path หรือ URL ของรูปโปรไฟล์
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE classrooms (
    classroom_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL, -- เช่น "2/1", "2/2"
    created_by INT, -- ครูผู้สร้างห้อง
    FOREIGN KEY (created_by) REFERENCES users(user_id)
);
CREATE TABLE classrooms (
    classroom_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL, -- เช่น "2/1", "2/2"
    created_by INT, -- ครูผู้สร้างห้อง
    FOREIGN KEY (created_by) REFERENCES users(user_id)
);
CREATE TABLE assignments (
    assignment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT NOT NULL,
    classroom_id INT NOT NULL,
    file_name VARCHAR(255) NOT NULL,
    file_path VARCHAR(255) NOT NULL, -- เก็บ URL หรือ path ของไฟล์
    submitted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (student_id) REFERENCES users(user_id),
    FOREIGN KEY (classroom_id) REFERENCES classrooms(classroom_id)
);
CREATE TABLE grades (
    grade_id INT AUTO_INCREMENT PRIMARY KEY,
    assignment_id INT NOT NULL,
    teacher_id INT NOT NULL,
    score DECIMAL(5,2), -- เช่น 95.50
    feedback TEXT,
    graded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (assignment_id) REFERENCES assignments(assignment_id),
    FOREIGN KEY (teacher_id) REFERENCES users(user_id)
);
CREATE TABLE notifications (
    notification_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    message TEXT NOT NULL,
    status ENUM('unread','read') DEFAULT 'unread',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);
</html>
