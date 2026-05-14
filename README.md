<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบส่งการบ้าน - Classroom Hub</title>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500&display=swap" rel="stylesheet">

    <style>
        :root {
            --bg-color: #f0f7ff;      /* พื้นหลังน้ำเงินสว่างมาก */
            --card-bg: #ffffff;      /* สีขาวสะอาด */
            --accent-pink: #ffc1cc;  /* ชมพูพาสเทล */
            --accent-blue: #a2c2e1;  /* น้ำเงินพาสเทล */
            --text-main: #5a5a5a;
            --nav-bg: rgba(255, 255, 255, 0.8);
        }

        body {
            font-family: 'Kanit', sans-serif;
            background-color: var(--bg-color);
            margin: 0;
            color: var(--text-main);
            /* พื้นหลังไล่เฉดเบาๆ ให้ดูมีมิติแบบในรูป */
            background: linear-gradient(135deg, #fdfcfb 0%, #e2ebf0 100%);
            min-height: 100vh;
        }

        /* Navbar แบบใสๆ สบายตา */
        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 8%;
            background: var(--nav-bg);
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 15px rgba(0,0,0,0.03);
        }

        .logo {
            font-size: 1.2rem;
            font-weight: 500;
            color: #777;
            letter-spacing: 1px;
        }

        /* ส่วนโปรไฟล์ */
        .user-controls {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .profile-btn {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            border: 2px solid var(--accent-pink);
            cursor: pointer;
            object-fit: cover;
            transition: 0.3s;
        }

        .profile-btn:hover { transform: scale(1.1); }

        /* ส่วนหัวข้อ */
        .page-title {
            text-align: center;
            padding: 60px 20px 40px;
        }

        .page-title h1 {
            font-size: 2.2rem;
            font-weight: 400;
            margin: 0;
            color: #444;
        }

        .page-title p { color: #888; margin-top: 10px; }

        /* การจัดวางกล่อง (Grid Layout) ตามรูปตัวอย่าง */
        .container {
            max-width: 1100px;
            margin: 0 auto;
            padding: 0 20px 60px;
        }

        .class-grid {
            display: grid;
            /* เรียง 3 กล่องต่อแถวสวยๆ */
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .class-card {
            background: var(--card-bg);
            border-radius: 30px; /* ความโค้งมนสูงตามรูป */
            padding: 40px 20px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.04);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            border: 1px solid rgba(255,255,255,0.6);
        }

        .class-card:hover {
            transform: translateY(-12px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.08);
            background: linear-gradient(to bottom right, #ffffff, var(--soft-blue));
        }

        .class-card h3 {
            font-size: 1.5rem;
            margin-bottom: 25px;
            color: #333;
            font-weight: 500;
        }

        /* ปุ่มกดที่ดูนุ่มนวล */
        .submit-btn {
            background-color: var(--accent-pink);
            color: #7a5a5a;
            border: none;
            padding: 12px 35px;
            border-radius: 50px;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.3s;
            box-shadow: 0 4px 15px rgba(255, 193, 204, 0.4);
        }

        .submit-btn:hover {
            background-color: #ffadb9;
            box-shadow: 0 6px 20px rgba(255, 193, 204, 0.6);
        }

        /* ส่วนของ Footer */
        footer {
            text-align: center;
            padding-bottom: 40px;
            color: #aaa;
            font-size: 0.85rem;
        }

        input[type="file"] { display: none; }
    </style>
</head>
<body>

    <nav class="navbar">
        <div class="logo">CLASSROOM HUB</div>
        <div class="user-controls">
            <button class="submit-btn" style="padding: 8px 20px; font-size: 0.9rem; background: var(--accent-blue); color: white; box-shadow: none;">Teacher Login</button>
            <img src="https://cdn-icons-png.flaticon.com/512/1144/1144760.png" class="profile-btn" id="profile-display" onclick="document.getElementById('avatar-input').click()">
            <input type="file" id="avatar-input" accept="image/*" onchange="updateProfile(event)">
        </div>
    </nav>

    <div class="page-title">
        <h1>ห้องเรียน ม.2</h1>
        <p>เลือกห้องเรียนเพื่อเข้าสู่ระบบการส่งงาน</p>
    </div>

    <div class="container">
        <div class="class-grid">
            <script>
                const rooms = ['2/1', '2/2', '2/3', '2/4', '2/5', '2/6', '2/7', '2/8', '2/9'];
                rooms.forEach(room => {
                    document.write(`
                        <div class="class-card">
                            <h3>ห้อง ม.${room}</h3>
                            <input type="file" id="file-${room}" accept=".pdf,.doc,.docx,.jpg,.png,.ppt,.pptx">
                            <button class="submit-btn" onclick="document.getElementById('file-${room}').click()">ส่งงาน</button>
                        </div>
                    `);
                });
            </script>
        </div>
    </div>

    <footer>
        Designed by Mart & Jaymi © 2026
    </footer>

    <script>
        // ฟังก์ชันเปลี่ยนรูปโปรไฟล์
        function updateProfile(event) {
            const reader = new FileReader();
            reader.onload = function() {
                document.getElementById('profile-display').src = reader.result;
            }
            reader.readAsDataURL(event.target.files[0]);
        }
    </script>
</body>
</html>
