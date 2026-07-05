<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>মুক্তিযুদ্ধের পক্ষে প্রোফাইল ফ্রেম</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f7f6;
            text-align: center;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 500px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        h1 { color: #006a4e; }
        p { color: #555; }
        #canvas-container {
            position: relative;
            width: 300px;
            height: 300px;
            margin: 20px auto;
            border: 2px dashed #006a4e;
            border-radius: 10px;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        canvas {
            max-width: 100%;
            max-height: 100%;
            display: none;
        }
        .placeholder-text {
            color: #888;
        }
        input[type="file"] {
            display: none;
        }
        .btn {
            display: inline-block;
            padding: 12px 24px;
            background-color: #f42a41;
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px;
            transition: 0.3s;
        }
        .btn-upload {
            background-color: #006a4e;
        }
        .btn:hover {
            opacity: 0.9;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>চেতনা আমাদের অহংকার</h1>
    <p>আপনার ছবি আপলোড করে মুক্তিযুদ্ধের সপক্ষের ফ্রেম তৈরি করুন</p>
    
    <div id="canvas-container">
        <span class="placeholder-text" id="placeholder">আপনার ছবি এখানে দেখা যাবে</span>
        <canvas id="canvas" width="600" height="600"></canvas>
    </div>

    <input type="file" id="upload" accept="image/*">
    <label for="upload" class="btn btn-upload">📸 ছবি সিলেক্ট করুন</label>
    <br>
    <button class="btn" id="download" style="display: none;">📥 ছবি ডাউনলোড করুন</button>
</div>

<script>
    const upload = document.getElementById('upload');
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const downloadBtn = document.getElementById('download');
    const placeholder = document.getElementById('placeholder');

    let userImage = new Image();

    upload.addEventListener('change', (e) => {
        const file = e.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = function(event) {
                userImage.src = event.target.result;
            }
            reader.readAsDataURL(file);
        }
    });

    userImage.onload = function() {
        placeholder.style.display = 'none';
        canvas.style.display = 'block';
        downloadBtn.style.display = 'inline-block';
        drawCanvas();
    }

    function drawCanvas() {
        // ক্যানভাস পরিষ্কার করা
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        
        // ১. ব্যবহারকারীর ছবি আঁকা (স্কয়ার শেপে ফিট করা)
        ctx.drawImage(userImage, 0, 0, 600, 600);
        
        // ২. মুক্তিযুদ্ধের ফ্রেম ডিজাইন (কোড দিয়ে তৈরি ফ্রেম)
        // নিচের দিকে লাল-সবুজ বর্ডার বা ব্যানার
        ctx.fillStyle = "rgba(0, 106, 78, 0.85)"; // সবুজ ব্যাকগ্রাউন্ড (স্বচ্ছ)
        ctx.fillRect(0, 500, 600, 100);
        
        ctx.fillStyle = "#f42a41"; // লাল বর্ডার
        ctx.fillRect(0, 490, 600, 10);
        
        // ফ্রেমের ওপর লেখা
        ctx.fillStyle = "#ffffff";
        ctx.font = "bold 32px Arial";
        ctx.textAlign = "center";
        ctx.fillText("আমি মুক্তিযুদ্ধের পক্ষে", 300, 560);
    }

    // ডাউনলোড ফাংশন
    downloadBtn.addEventListener('click', () => {
        const link = document.createElement('a');
        link.download = 'muktijuddho_profile.png';
        link.href = canvas.toDataURL();
        link.click();
    });
</script>

</body>
</html>
