<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบส่งการบ้าน - Classroom Hub</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@200;400;600&display=swap" rel="stylesheet">

    <style>
        /* --- ตั้งค่าพื้นฐาน --- */
        :root {
            --bg-gradient: linear-gradient(135deg, #e0c3fc 0%, #8ec5fc 100%);
            --glass-bg: rgba(255, 255, 255, 0.85);
            --text-primary: #2c3e50;
            --accent-pink: #ffafbd;
            --accent-blue: #2193b0;
        }

        * {
            box-sizing: border-box;
            font-family: 'Kanit', sans-serif;
        }

        body {
            /* พื้นหลังเป็นสี Gradient นุ่มๆ */
            background: var(--bg-gradient);
            background-attachment: fixed;
            margin: 0;
            color: var(--text-primary);
            min-height: 100vh;
        }

        /* --- Navbar ดีไซน์โปร่งแสง --- */
        .navbar {
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(10px);
            padding: 15px 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            border-bottom: 1px solid rgba(255, 255, 255, 0.3);
        }

        .logo {
            font-size: 1.6rem;
            font-weight: 600;
            background: linear-gradient(to right, #2193b0, #6dd5ed);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* --- ส่วนหัวข้อกลางหน้าเว็บ --- */
        .hero {
            text-align: center;
            padding: 60px 20px;
        }

        .hero h1 {
            font-size: 2.8rem;
            font-weight: 600;
            margin: 0;
            letter-spacing: 1px;
            color: #fff;
            text-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .hero p {
            font-size: 1.1rem;
            color: #f8f9fa;
            font-weight: 200;
        }

        /* --- การจัดวางกล่องห้องเรียน --- */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px 50px 20px;
        }

        .class-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 30px;
        }

        .class-card {
            background: var(--glass-bg);
            backdrop-filter: blur(5px);
            border-radius: 30px;
            padding: 40px 30px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.5);
            box-shadow: 0 10px 30px rgba(0,0,0,0.05);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .class-card:hover {
            transform: translateY(-15px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            background: white;
        }

        .class-card h3 {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: var(--accent-blue);
        }

        /* --- พื้นที่ QR Code --- */
        .qr-box {
            width: 160px;
            height: 160px;
            margin: 0 auto 25px;
            background: #fdfbfb;
            border-radius: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px dashed var(--accent-pink);
            color: #ce93d8;
        }

        /* --- ปุ่มกดสไตล์นุ่มนวล --- */
        .btn-submit {
            background: linear-gradient(to right, #ffafbd, #ffc3a0);
            color: white;
            border: none;
            padding: 12px 35px;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 400;
            cursor: pointer;
            width: 100%;
            transition: 0.3s;
            box-shadow: 0 5px 15px rgba(255, 175, 189, 0.4);
        }

        .btn-submit:hover {
            transform: scale(1.03);
            box-shadow: 0 8px 20px rgba(255, 175, 189, 0.6);
        }

        /* โปรไฟล์นักเรียน */
        .profile-img {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            border: 2px solid white;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            cursor: pointer;
        }
    </style>
</head>
<body>

    <nav class="navbar">
        <div class="logo">Classroom 2026</div>
        <div style="display: flex; align-items: center; gap: 15px;">
            <span style="font-weight: 200;">ครูมาร์ท</span>
            <img src="https://via.placeholder.com/45" class="profile-img" alt="Profile">
        </div>
    </nav>

    <div class="hero">
        <h1>พื้นที่ส่งงานออนไลน์</h1>
        <p>ยกระดับการเรียนรู้ด้วยระบบจัดการที่ง่ายและสวยงาม</p>
    </div>

    <div class="container">
        <div class="class-grid">
            <script>
                for(let i=1; i<=9; i++) {
                    document.write(`
                        <div class="class-card">
                            <h3>ห้อง ม.2/${i}</h3>
                            <div class="qr-box">
                                <span style="font-size: 0.8rem;">[ Scan QR Code ]</span>
                            </div>
                            <button class="btn-submit" onclick="alert('ระบบกำลังเปิดรับไฟล์ห้อง 2/${i}')">ส่งงานที่นี่</button>
                            <p style="font-size: 0.8rem; color: #999; margin-top: 15px;">ส่งได้ทั้ง PDF, Word และรูปภาพ</p>
                        </div>
                    `);
                }
            </script>
        </div>
    </div>

    <footer style="text-align: center; padding: 30px; color: white; font-weight: 200;">
        © 2026 Designed for Education by Mart & Jaymi
    </footer>

</body>
</html>
