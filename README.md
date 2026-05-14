<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบส่งการบ้าน - Classroom Hub</title>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500&display=swap" rel="stylesheet">

    <style>
        :root {
            --soft-blue: #eef5ff;   /* น้ำเงินสว่างละมุน */
            --soft-pink: #fff0f5;   /* ชมพูอ่อนหวาน */
            --accent-blue: #7fb3d5; /* น้ำเงินเข้มขึ้นนิดนึงสำหรับขอบ */
            --accent-pink: #ffb6c1; /* ชมพูสำหรับปุ่ม */
            --white: #ffffff;
            --text: #555;
        }

        body {
            font-family: 'Kanit', sans-serif;
            background-color: var(--soft-blue);
            margin: 0;
            color: var(--text);
        }

        /* ส่วน Navbar */
        .navbar {
            background: var(--white);
            padding: 15px 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo { font-size: 1.4rem; font-weight: 500; color: var(--accent-blue); }

        /* ส่วนโปรไฟล์นักเรียน */
        .profile-section {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .avatar-wrapper {
            position: relative;
            cursor: pointer;
        }

        #profile-img {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            border: 2px solid var(--accent-pink);
            object-fit: cover;
        }

        /* ส่วนหัวข้อเว็บ */
        .header-content {
            text-align: center;
            padding: 50px 20px;
            background: linear-gradient(to bottom, var(--white), var(--soft-blue));
        }

        /* จัดระเบียบการวางกล่องห้องเรียน (Grid) */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .class-grid {
            display: grid;
            /* ปรับตรงนี้ให้เรียง 3 กล่องต่อแถวในจอปกติ และ 1 กล่องในมือถือ */
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
        }

        .class-card {
            background: var(--white);
            border-radius: 25px;
            padding: 25px;
            text-align: center;
            border: 1px solid var(--soft-pink);
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.02);
        }

        .class-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 12px 25px rgba(255, 182, 193, 0.3);
            border-color: var(--accent-pink);
        }

        .class-card h3 { color: var(--accent-blue); margin-bottom: 15px; }

        .qr-placeholder {
            width: 130px;
            height: 130px;
            margin: 0 auto 15px;
            background: var(--soft-pink);
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px dashed var(--accent-pink);
            color: #d1929c;
            font-size: 0.8rem;
        }

        /* ปุ่มต่างๆ */
        .btn {
            background: var(--accent-pink);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 50px;
            cursor: pointer;
            width: 100%;
            font-size: 1rem;
            transition: 0.3s;
        }

        .btn:hover { background: #ff99aa; }

        .login-btn { width: auto; background: var(--accent-blue); }

        /* ซ่อน Input File */
        input[type="file"] { display: none; }
    </style>
</head>
<body>

    <nav class="navbar">
        <div class="logo">Classroom Hub 🍎</div>
        <div class="profile-section">
            <button class="btn login-btn">Login Gmail</button>
            <div class="avatar-wrapper" onclick="document.getElementById('upload-avatar').click()">
                <img src="https://cdn-icons-png.flaticon.com/512/1144/1144760.png" id="profile-img" title="เปลี่ยนรูปโปรไฟล์">
                <input type="file" id="upload-avatar" accept="image/*" onchange="previewImage(event)">
            </div>
        </div>
    </nav>

    <div class="header-content">
        <h1>พื้นที่ส่งงานออนไลน์</h1>
        <p>มาร์ทเลือกห้องเรียนแล้วอัปโหลดไฟล์ (PDF, Word, JPG, PPT) ได้เลยครับ</p>
    </div>

    <div class="container">
        <div class="class-grid">
            <script>
                for(let i=1; i<=9; i++) {
                    document.write(`
                        <div class="class-card">
                            <h3>ห้อง ม.2/${i}</h3>
                            <div class="qr-placeholder">สแกนส่งงาน<br>(QR Code)</div>
                            <input type="file" id="file-${i}" accept=".pdf,.doc,.docx,.jpg,.png,.ppt,.pptx">
                            <button class="btn" onclick="document.getElementById('file-${i}').click()">เลือกไฟล์ส่งงาน</button>
                            <p style="font-size:0.75rem; color:#aaa; margin-top:10px;">รองรับ: PDF, Word, รูปภาพ, PPT</p>
                        </div>
                    `);
                }
            </script>
        </div>
    </div>

    <footer style="text-align: center; padding: 40px; color: #bbb; font-size: 0.9rem;">
        ออกแบบระบบโดย มาร์ท & Jaymi © 2026
    </footer>

    <script>
        // ฟังก์ชันเปลี่ยนรูปโปรไฟล์แบบ Real-time
        function previewImage(event) {
            const reader = new FileReader();
            reader.onload = function() {
                const output = document.getElementById('profile-img');
                output.src = reader.result;
            }
            reader.readAsDataURL(event.target.files[0]);
        }
    </script>
</body>
</html>
