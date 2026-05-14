<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Classroom Hub - ระบบส่งงานอัจฉริยะ</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@200;300;400;500;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        :root {
            --primary-gradient: linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%);
            --accent-pink: #ff9a9e;
            --accent-blue: #4facfe;
            --glass: rgba(255, 255, 255, 0.9);
            --shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.15);
        }

        * {
            box-sizing: border-box;
            font-family: 'Kanit', sans-serif;
        }

        body {
            margin: 0;
            padding: 0;
            background: #f0f4f8;
            color: #444;
            min-height: 100vh;
        }

        /* --- พื้นหลังส่วนบน --- */
        .top-banner {
            background: var(--primary-gradient);
            height: 300px;
            width: 100%;
            position: absolute;
            top: 0;
            z-index: -1;
            border-radius: 0 0 50px 50px;
        }

        /* --- Navbar --- */
        .navbar {
            padding: 20px 8%;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 600;
            color: white;
            text-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .auth-box {
            display: flex;
            align-items: center;
            gap: 15px;
            background: var(--glass);
            padding: 8px 15px;
            border-radius: 50px;
            box-shadow: var(--shadow);
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: 2px solid var(--accent-pink);
            cursor: pointer;
            object-fit: cover;
        }

        /* --- Hero Section --- */
        .hero {
            text-align: center;
            padding: 40px 20px;
            color: white;
        }

        .hero h1 { font-size: 3rem; margin: 0; font-weight: 500; }
        .hero p { font-size: 1.2rem; opacity: 0.9; font-weight: 200; }

        /* --- Main Container --- */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* --- Grid การจัดวาง --- */
        .class-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 30px;
            margin-top: -50px; /* ให้กล่องลอยขึ้นไปทับพื้นหลังสีฟ้า */
        }

        .class-card {
            background: var(--glass);
            border-radius: 35px;
            padding: 35px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.3);
            box-shadow: var(--shadow);
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
        }

        .class-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 8px;
            background: linear-gradient(to right, var(--accent-blue), var(--accent-pink));
        }

        .class-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 45px rgba(0,0,0,0.1);
        }

        .class-card h3 {
            font-size: 1.8rem;
            color: #333;
            margin-bottom: 20px;
        }

        /* --- QR Code & Upload --- */
        .upload-zone {
            background: #f8fbff;
            border: 2px dashed #d1e3ff;
            border-radius: 25px;
            padding: 30px;
            margin-bottom: 20px;
            transition: 0.3s;
        }

        .upload-zone:hover {
            background: #fff;
            border-color: var(--accent-blue);
        }

        .qr-icon {
            font-size: 3rem;
            color: var(--accent-blue);
            margin-bottom: 10px;
        }

        .btn-upload {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 15px;
            font-size: 1rem;
            cursor: pointer;
            width: 100%;
            box-shadow: 0 4px 15px rgba(118, 75, 162, 0.3);
            transition: 0.3s;
        }

        .btn-upload:hover {
            filter: brightness(1.1);
            transform: scale(1.02);
        }

        /* --- Teacher Section --- */
        .teacher-panel {
            margin-top: 80px;
            background: white;
            border-radius: 40px;
            padding: 50px;
            text-align: center;
            box-shadow: var(--shadow);
        }

        .badge {
            background: var(--accent-pink);
            color: white;
            padding: 5px 15px;
            border-radius: 50px;
            font-size: 0.8rem;
            margin-bottom: 15px;
            display: inline-block;
        }

        footer {
            text-align: center;
            padding: 50px;
            color: #aaa;
            font-weight: 200;
        }
    </style>
</head>
<body>

    <div class="top-banner"></div>

    <nav class="navbar">
        <div class="logo"><i class="fas fa-graduation-cap"></i> Classroom Hub</div>
        <div class="auth-box">
            <span style="font-size: 0.9rem;">มาร์ท (ครูผู้สอน)</span>
            <input type="file" id="avatar-input" hidden onchange="updateAvatar(event)">
            <img src="https://via.placeholder.com/40" class="user-avatar" id="display-avatar" onclick="document.getElementById('avatar-input').click()">
            <button style="border:none; background:none; color:var(--accent-blue); cursor:pointer;"><i class="fas fa-sign-out-alt"></i></button>
        </div>
    </nav>

    <div class="hero">
        <h1>ส่งการบ้านออนไลน์</h1>
        <p>จัดการไฟล์งานได้ง่ายๆ สำหรับนักเรียนชั้นมัธยมศึกษาปีที่ 2</p>
    </div>

    <div class="container">
        <div class="class-grid">
            <script>
                for(let i=1; i<=9; i++) {
                    document.write(`
                        <div class="class-card">
                            <span class="badge">Active</span>
                            <h3>ห้อง ม.2/${i}</h3>
                            <div class="upload-zone">
                                <i class="fas fa-qrcode qr-icon"></i>
                                <p style="font-size:0.8rem; color:#888;">สแกนเพื่อส่งงาน หรือลากไฟล์มาวางที่นี่</p>
                            </div>
                            <input type="file" id="file-${i}" hidden multiple>
                            <button class="btn-upload" onclick="document.getElementById('file-${i}').click()">
                                <i class="fas fa-cloud-upload-alt"></i> อัปโหลดไฟล์งาน
                            </button>
                        </div>
                    `);
                }
            </script>
        </div>

        <div class="teacher-panel">
            <h2 style="color: #333;"><i class="fas fa-user-shield"></i> ระบบจัดการสำหรับคุณครู</h2>
            <p>แก้ไขโฟลเดอร์ ตรวจงาน และลงคะแนนแบบ Real-time</p>
            <div style="display: flex; gap: 15px; justify-content: center; margin-top: 25px;">
                <button class="btn-upload" style="background: var(--accent-blue); width: auto;">เข้าสู่ระบบจัดการ (Gmail)</button>
                <button class="btn-upload" style="background: #fff; color: #777; border: 1px solid #ddd; width: auto; box
