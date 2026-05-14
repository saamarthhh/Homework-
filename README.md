<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบส่งการบ้าน - Classroom Hub</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500&display=swap" rel="stylesheet">

    <style>
        /* --- ส่วนของการตกแต่ง (CSS) --- */
        :root {
            --soft-blue: #e3f2fd;    /* สีน้ำเงินอ่อนละมุน */
            --pastel-pink: #fce4ec;  /* สีชมพูอ่อนสบายตา */
            --deep-blue: #5c9ead;
            --accent-pink: #f06292;
            --white: #ffffff;
            --text-color: #4a4a4a;
        }

        * {
            box-sizing: border-box;
            font-family: 'Kanit', sans-serif;
        }

        body {
            background-color: var(--soft-blue);
            color: var(--text-color);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }

        /* ส่วนหัวด้านบน */
        .navbar {
            background-color: var(--white);
            padding: 1rem 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 500;
            color: var(--deep-blue);
        }

        /* ส่วนแนะนำตัว */
        .hero-section {
            text-align: center;
            padding: 4rem 1rem;
            background: linear-gradient(135deg, var(--soft-blue) 0%, var(--pastel-pink) 100%);
        }

        .hero-section h1 {
            margin-bottom: 10px;
            color: var(--deep-blue);
        }

        /* จัดระเบียบห้องเรียน */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }

        .class-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
        }

        .class-card {
            background: var(--white);
            border-radius: 20px;
            padding: 30px;
            text-align: center;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            box-shadow: 0 4px 6px rgba(0,0,0,0.02);
        }

        .class-card:hover {
            transform: translateY(-10px);
            border-color: var(--pastel-pink);
            box-shadow: 0 15px 30px rgba(0,0,0,0.08);
        }

        .class-card h3 {
            margin-top: 0;
            color: var(--deep-blue);
        }

        /* ปุ่มต่างๆ */
        .btn-primary {
            background-color: var(--accent-pink);
            color: white;
            border: none;
            padding: 10px 25px;
            border-radius: 30px;
            cursor: pointer;
            font-size: 1rem;
            transition: background 0.3s;
        }

        .btn-primary:hover {
            background-color: #ec407a;
        }

        .btn-upload {
            background-color: var(--soft-blue);
            color: var(--deep-blue);
            border: 1px solid var(--deep-blue);
            padding: 8px 20px;
            border-radius: 20px;
            cursor: pointer;
            margin-top: 15px;
            width: 100%;
        }

        .btn-upload:hover {
            background-color: var(--deep-blue);
            color: white;
        }

        /* พื้นที่ QR Code จำลอง */
        .qr-area {
            width: 140px;
            height: 140px;
            margin: 20px auto;
            background-color: #f8f9fa;
            border: 2px dashed #ddd;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 10px;
            font-size: 0.8rem;
            color: #999;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .profile-img {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            object-fit: cover;
            border: 2px solid var(--pastel-pink);
        }
    </style>
</head>
<body>

    <nav class="navbar">
        <div class="logo">Classroom Hub 📚</div>
        <div class="user-profile">
            <span>นักเรียน มาร์ท</span>
            <img src="https://via.placeholder.com/40" class="profile-img" alt="User Profile">
            <button class="btn-primary" style="margin-left:10px;">Login with Gmail</button>
        </div>
    </nav>

    <header class="hero-section">
        <h1>ส่งการบ้านออนไลน์</h1>
        <p>เลือกห้องเรียนของคุณเพื่อส่งไฟล์งาน (PDF, Word, รูปภาพ, PPT)</p>
    </header>

    <main class="container">
        <section class="class-grid">
            <script>
                // ใช้ JavaScript ช่วยสร้างการ์ดห้องเรียนเพื่อประหยัดบรรทัดโค้ดครับ
                for(let i=1; i<=9; i++) {
                    document.write(`
                        <div class="class-card">
                            <h3>ห้อง ม.2/${i}</h3>
                            <div class="qr-area">สแกน QR Code<br>ที่นี่เพื่อส่งงาน</div>
                            <p style="font-size: 0.9rem;">หรือเลือกไฟล์จากเครื่อง</p>
                            <input type="file" id="file-2-${i}" hidden>
                            <button onclick="document.getElementById('file-2-${i}').click()" class="btn-upload">อัปโหลดไฟล์งาน</button>
                        </div>
                    `);
                }
            </script>
        </section>

        <section id="teacher-section" style="margin-top: 50px; text-align: center; padding: 40px; background: white; border-radius: 20px;">
            <h2 style="color: var(--accent-pink);">แผงควบคุมสำหรับคุณครู</h2>
            <p>กรุณาล็อกอินด้วยบัญชี Gmail ครูเพื่อจัดการห้องเรียนและให้คะแนน</p>
            <button class="btn-primary">เข้าสู่ระบบสำหรับครู</button>
        </section>
    </main>

    <footer style="text-align: center; padding: 2rem; color: #888; font-size: 0.8rem;">
        &copy; 2026 ระบบจัดการห้องเรียน - มาร์ท
    </footer>

</body>
</html>
