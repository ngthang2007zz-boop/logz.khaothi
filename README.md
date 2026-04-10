<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LogZ TSA - Hệ thống thi thử Tư duy 2026</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <script>
        window.MathJax = { tex: { inlineMath: [['$', '$']], displayMath: [['$$', '$$']] } };
    </script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #f1f5f9; }
        .page { display: none; }
        .page.active { display: block; animation: fadeIn 0.3s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: scale(0.98); } to { opacity: 1; transform: scale(1); } }
        .glass { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(8px); }
    </style>
</head>
<body>

    <div id="page-login" class="page active min-h-screen flex items-center justify-center bg-slate-900 p-4">
        <div class="max-w-md w-full glass p-8 rounded-[2rem] shadow-2xl border border-white/20">
            <div class="text-center mb-8">
                <h1 class="text-4xl font-black text-red-600 tracking-tighter uppercase italic underline underline-offset-8">LogZ TSA</h1>
                <p class="text-slate-500 font-bold text-xs mt-4 uppercase tracking-[0.2em]">Hệ thống luyện thi tư duy bách khoa</p>
            </div>

            <div class="flex p-1 bg-slate-100 rounded-2xl mb-6">
                <button onclick="switchLogin('stu')" id="btn-stu" class="flex-1 py-2 rounded-xl text-sm font-bold bg-white text-blue-600 shadow-sm transition-all">THÍ SINH</button>
                <button onclick="switchLogin('adm')" id="btn-adm" class="flex-1 py-2 rounded-xl text-sm font-bold text-slate-500 transition-all">ADMIN</button>
            </div>

            <div id="form-stu" class="space-y-4">
                <input type="text" id="stu-name" placeholder="Họ và tên thí sinh" class="w-full p-4 border-2 border-slate-100 rounded-2xl outline-none focus:border-blue-500 transition-all">
                <input type="text" id="stu-code" placeholder="Mã phòng thi (VD: TSA2026)" class="w-full p-4 border-2 border-slate-100 rounded-2xl outline-none focus:border-blue-500 font-mono tracking-widest uppercase">
                <button onclick="verifyStudent()" class="w-full bg-blue-600 text-white font-bold py-4 rounded-2xl shadow-xl hover:bg-blue-700 transition-all active:scale-95">VÀO PHÒNG THI</button>
            </div>

            <div id="form-adm" class="space-y-4 hidden">
                <input type="email" id="adm-email" placeholder="Email quản trị" class="w-full p-4 border-2 border-slate-100 rounded-2xl outline-none focus:border-indigo-500">
                <input type="password" id="adm-pass" placeholder="Mật khẩu" class="w-full p-4 border-2 border-slate-100 rounded-2xl outline-none focus:border-indigo-500">
                <button onclick="verifyAdmin()" class="w-full bg-slate-800 text-white font-bold py-4 rounded-2xl hover:bg-black shadow-xl transition-all">ĐĂNG NHẬP ADMIN</button>
            </div>
        </div>
    </div>

    <div id="page-exam" class="page min-h-screen bg-white">
        <header class="border-b px-6 py-4 flex justify-between items-center sticky top-0 bg-white/80 backdrop-blur-md z-50">
            <div class="flex items-center gap-4">
                <div class="w-10 h-10 bg-red-600 text-white flex items-center justify-center rounded-xl font-bold">LZ</div>
                <div><p class="text-[10px] text-slate-400 font-bold uppercase tracking-wider">Thí sinh dự thi</p><p id="disp-name" class="font-bold text-slate-800 uppercase">---</p></div>
            </div>
            <div class="px-6 py-2 bg-red-50 rounded-2xl border border-red-100">
                <span id="timer" class="text-2xl font-mono font-black text-red-600">60:00</span>
            </div>
            <button onclick="confirmSubmit()" class="bg-slate-900 text-white px-8 py-2 rounded-xl font-bold hover:bg-red-600 transition-all">NỘP BÀI</button>
        </header>

        <main class="max-w-7xl mx-auto p-6 grid grid-cols-12 gap-8">
            <div class="col-span-12 lg:col-span-8">
                <div class="bg-slate-50 p-10 rounded-[2.5rem] border border-slate-100 shadow-inner">
                    <span class="bg-blue-600 text-white px-4 py-1 rounded-full text-[10px] font-bold uppercase tracking-widest">Câu hỏi 01</span>
                    <div class="mt-8 text-2xl font-bold text-slate-800 leading-snug">
                        Cho tích phân $I = \int_{0}^{\pi} e^x \sin x dx$. Giá trị của $I$ bằng:
                    </div>
                    <div class="mt-12 space-y-4">
                        <label class="flex items-center p-6 bg-white border-2 border-transparent rounded-3xl hover:border-blue-500 cursor-pointer shadow-sm transition-all group">
                            <input type="radio" name="q" class="w-6 h-6 accent-blue-600">
                            <span class="ml-4 font-bold text-slate-600 group-hover:text-blue-600 text-lg">A. $\frac{e^\pi + 1}{2}$</span>
                        </label>
                        <label class="flex items-center p-6 bg-white border-2 border-transparent rounded-3xl hover:border-blue-500 cursor-pointer shadow-sm transition-all group">
                            <input type="radio" name="q" class="w-6 h-6 accent-blue-600">
                            <span class="ml-4 font-bold text-slate-600 group-hover:text-blue-600 text-lg">B. $e^\pi - 1$</span>
                        </label>
                    </div>
                </div>
            </div>
            <aside class="col-span-12 lg:col-span-4 space-y-6">
                <div class="bg-white p-6 rounded-[2rem] border shadow-sm">
                    <h3 class="font-black text-slate-800 mb-4 flex justify-between">PHIẾU TRẢ LỜI <span class="text-blue-600">0/40</span></h3>
                    <div class="grid grid-cols-5 gap-3" id="exam-nav"></div>
                </div>
                <div class="p-5 bg-amber-50 rounded-2xl border border-amber-100 text-[11px] text-amber-700 font-medium leading-relaxed italic">
                    <i class="fa-solid fa-triangle-exclamation mr-1"></i> CẢNH BÁO: Hệ thống đang giám sát. Việc rời khỏi tab hoặc thu nhỏ trình duyệt sẽ dẫn đến việc <b>NỘP BÀI TỰ ĐỘNG</b> ngay lập tức.
                </div>
            </aside>
        </main>
    </div>

    <div id="page-result" class="page min-h-screen bg-slate-50 p-4 md:p-10">
        <div class="max-w-5xl mx-auto">
            <div class="flex items-center gap-4 mb-8">
                <button onclick="location.reload()" class="bg-white p-3 rounded-xl border shadow-sm hover:bg-slate-50"><i class="fa-solid fa-house"></i></button>
                <h1 class="text-2xl font-black text-red-600 uppercase tracking-widest flex-1 text-center">Kết quả bài thi hệ thống thi thử LOGZ</h1>
            </div>

            <div class="bg-white rounded-[2rem] shadow-sm border p-8 grid md:grid-cols-2 gap-10 relative overflow-hidden mb-6">
                <div class="space-y-5">
                    <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                        <span class="text-slate-400 italic text-sm">Người dự thi - <small>Candidate name:</small></span>
                        <span id="res-name" class="font-black bg-slate-100 px-4 py-1 rounded-lg uppercase text-slate-700 tracking-wider">---</span>
                    </div>
                    <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                        <span class="text-slate-400 italic text-sm">Ngày thi - <small>Test date:</small></span>
                        <span class="font-bold text-slate-700">10/04/2026</span>
                    </div>
                    <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                        <span class="text-slate-400 italic text-sm">Số báo danh - <small>Candidate ID:</small></span>
                        <span class="font-bold text-blue-600 bg-blue-50 px-3 py-1 rounded-lg">ntgguh7157@gmail.com</span>
                    </div>
                </div>
                <div class="flex flex-col items-center justify-center bg-red-50/50 rounded-[2rem] border border-red-100 p-8">
                    <p class="text-slate-500 font-black text-xs uppercase tracking-widest mb-2">Điểm TSA <small class="lowercase italic text-slate-400">Overall score</small></p>
                    <p class="text-[7rem] font-black text-red-600 leading-none">8.5</p>
                    <p class="text-slate-400 font-bold mt-4 uppercase text-[10px] tracking-[0.3em]">/ 100 Câu</p>
                </div>
            </div>

            <div class="bg-white rounded-[2rem] shadow-sm border p-8 mb-6">
                <h3 class="font-black text-slate-800 mb-6 flex items-center gap-2 uppercase tracking-widest">Số câu đúng:</h3>
                <div class="space-y-4 font-bold text-slate-600">
                    <div class="flex justify-between items-center p-4 bg-slate-50 rounded-2xl border border-slate-100">
                        <span>Tư duy Toán học:</span> <span class="text-blue-600 text-xl">35 <small class="text-slate-300">/ 40</small></span>
                    </div>
                    <div class="flex justify-between items-center p-4 bg-slate-50 rounded-2xl border border-slate-100">
                        <span>Tư duy Đọc hiểu:</span> <span class="text-blue-600 text-xl">18 <small class="text-slate-300">/ 20</small></span>
                    </div>
                    <div class="flex justify-between items-center p-4 bg-slate-50 rounded-2xl border border-slate-100">
                        <span>Tư duy Khoa học / Giải quyết vấn đề:</span> <span class="text-blue-600 text-xl">32 <small class="text-slate-300">/ 40</small></span>
                    </div>
                </div>
            </div>

            <div class="flex flex-col md:flex-row items-center justify-end gap-4 mb-6">
                <span class="font-black text-slate-400 italic text-sm">Xem đáp án:</span>
                <select onchange="toggleAIBox()" id="ai-select" class="bg-white border-2 border-slate-200 p-3 rounded-2xl font-bold text-slate-700 focus:border-blue-500 outline-none min-w-[200px]">
                    <option value="">Chọn môn thi...</option>
                    <option value="math">Tư duy Toán học</option>
                </select>
            </div>

            <div id="ai-sol-box" class="hidden bg-indigo-900 text-white p-10 rounded-[2.5rem] shadow-2xl animate-fadeIn border-4 border-indigo-500/30">
                <div class="flex items-center gap-3 mb-6 font-black text-indigo-300 italic"><i class="fa-solid fa-robot text-2xl"></i> LOGZ AI TUTORING</div>
                <div class="prose prose-invert max-w-none">
                    <h4 class="text-xl font-bold mb-4">Câu 01: Lời giải chi tiết</h4>
                    <p class="text-indigo-100 leading-relaxed">
                        Sử dụng phương pháp tích phân từng phần hai lần cho hàm $e^x \sin x$. <br>
                        Đặt $u = \sin x, dv = e^x dx...$ <br>
                        Kết quả cuối cùng ta thu được công thức tổng quát: $\int e^x \sin x dx = \frac{e^x(\sin x - \cos x)}{2}$. <br>
                        Thế cận từ $0 \to \pi$, ta có: $I = \frac{e^\pi(0 - (-1))}{2} - \frac{e^0(0 - 1)}{2} = \frac{e^\pi + 1}{2}$. <br>
                        $\Rightarrow$ <b>Đáp án đúng là A.</b>
                    </p>
                </div>
            </div>
        </div>
    </div>

    <div id="page-admin" class="page min-h-screen bg-slate-50 flex">
        <nav class="w-72 bg-slate-900 p-8 flex flex-col h-screen sticky top-0 hidden md:flex">
            <h2 class="text-2xl font-black italic underline text-blue-400 mb-12">LogZ Admin</h2>
            <div class="space-y-4 flex-1">
                <a href="#" class="block p-4 bg-blue-600 rounded-2xl font-bold text-white shadow-lg shadow-blue-500/30"><i class="fa-solid fa-folder-open mr-2"></i> Kho đề thi</a>
                <a href="#" class="block p-4 text-slate-400 hover:text-white font-bold transition-all"><i class="fa-solid fa-chart-line mr-2"></i> Thống kê</a>
            </div>
            <button onclick="location.reload()" class="text-red-500 font-bold flex items-center gap-2 hover:translate-x-1 transition-all">Đăng xuất <i class="fa-solid fa-right-from-bracket"></i></button>
        </nav>

        <main class="flex-1 p-10 overflow-y-auto">
            <h1 class="text-4xl font-black text-slate-800 mb-2 tracking-tight">KHO QUẢN LÝ ĐỀ THI</h1>
            <p class="text-slate-400 font-bold mb-10 italic">Hệ thống xử lý mã nguồn LaTeX tự động</p>

            <div class="grid lg:grid-cols-2 gap-8">
                <div class="bg-white p-8 rounded-[2.5rem] border shadow-sm space-y-6">
                    <h3 class="font-black text-blue-600 text-lg flex items-center gap-2 uppercase"><i class="fa-solid fa-plus-circle"></i> Đăng đề mới</h3>
                    
                    <div class="space-y-4">
                        <div>
                            <label class="block text-[10px] font-black text-slate-400 uppercase tracking-widest mb-2">1. Upload file (.tex)</label>
                            <div class="border-4 border-dashed border-slate-100 rounded-[2rem] p-10 text-center hover:bg-slate-50 transition-all cursor-pointer group">
                                <i class="fa-solid fa-file-code text-4xl text-slate-200 group-hover:text-blue-500 mb-3"></i>
                                <p class="text-sm font-bold text-slate-400">Chọn file đề LaTeX từ máy tính</p>
                            </div>
                        </div>
                        
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-[10px] font-black text-slate-400 uppercase tracking-widest mb-2">2. Tạo mã đề</label>
                                <input type="text" placeholder="VD: TSA-0426" class="w-full p-4 bg-slate-50 border-none rounded-2xl font-mono text-sm focus:ring-2 focus:ring-blue-500 outline-none">
                            </div>
                            <div>
                                <label class="block text-[10px] font-black text-slate-400 uppercase tracking-widest mb-2">3. Thời gian (phút)</label>
                                <input type="number" value="60" class="w-full p-4 bg-slate-50 border-none rounded-2xl font-bold focus:ring-2 focus:ring-blue-500 outline-none">
                            </div>
                        </div>

                        <div>
                            <label class="block text-[10px] font-black text-slate-400 uppercase tracking-widest mb-2">4. Nhập đáp án</label>
                            <textarea placeholder="1A, 2B, 3D, 4C..." class="w-full p-4 bg-slate-50 border-none rounded-2xl font-mono text-xs h-24 focus:ring-2 focus:ring-blue-500 outline-none"></textarea>
                        </div>

                        <button onclick="alert('Đề thi đã được đăng thành công lên logztoanli.com!')" class="w-full bg-blue-600 text-white font-black py-5 rounded-[1.5rem] shadow-xl shadow-blue-600/20 hover:bg-blue-700 transition-all uppercase tracking-widest">Đăng đề lên hệ thống</button>
                    </div>
                </div>

                <div class="bg-white p-8 rounded-[2.5rem] border shadow-sm">
                    <h3 class="font-black text-slate-800 text-lg mb-6 uppercase tracking-widest">Đề thi đang vận hành</h3>
                    <div class="space-y-3">
                        <div class="p-5 bg-slate-50 rounded-2xl flex justify-between items-center border border-slate-100">
                            <div><p class="font-black text-slate-700">TSA-2026-CHINH-THUC</p><p class="text-[10px] text-slate-400 font-bold uppercase">40 Câu - 60 Phút</p></div>
                            <span class="bg-green-100 text-green-700 px-3 py-1 rounded-full text-[10px] font-black">ACTIVE</span>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <script>
        // Switch Login Tabs
        function switchLogin(type) {
            const bStu = document.getElementById('btn-stu');
            const bAdm = document.getElementById('btn-adm');
            const fStu = document.getElementById('form-stu');
            const fAdm = document.getElementById('form-adm');

            if(type === 'stu') {
                bStu.className = "flex-1 py-2 rounded-xl text-sm font-bold bg-white text-blue-600 shadow-sm transition-all";
                bAdm.className = "flex-1 py-2 rounded-xl text-sm font-bold text-slate-500 transition-all";
                fStu.classList.remove('hidden'); fAdm.classList.add('hidden');
            } else {
                bAdm.className = "flex-1 py-2 rounded-xl text-sm font-bold bg-white text-indigo-600 shadow-sm transition-all";
                bStu.className = "flex-1 py-2 rounded-xl text-sm font-bold text-slate-500 transition-all";
                fAdm.classList.remove('hidden'); fStu.classList.add('hidden');
            }
        }

        function showPage(id) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo(0,0);
        }

        // Đăng nhập Admin (yuunohuy@gmail.com / Cnmeo123)
        function verifyAdmin() {
            const email = document.getElementById('adm-email').value;
            const pass = document.getElementById('adm-pass').value;
            if(email === "yuunohuy@gmail.com" && pass === "Cnmeo123") {
                showPage('page-admin');
            } else { alert("Sai thông tin đăng nhập Admin!"); }
        }

        // Đăng nhập học sinh
        function verifyStudent() {
            const name = document.getElementById('stu-name').value;
            const code = document.getElementById('stu-code').value;
            if(name && code.toUpperCase() === "TSA2026") {
                document.getElementById('disp-name').innerText = name;
                document.getElementById('res-name').innerText = name;
                if(confirm("XÁC NHẬN VÀO THI?\nLưu ý: Thoát tab = Tự nộp bài!")) startExam();
            } else { alert("Vui lòng điền đủ thông tin & Mã TSA2026"); }
        }

        // Phòng thi & Anti-Cheat
        function startExam() {
            showPage('page-exam');
            initNav();
            startTimer(3600);

            // LOGIC CHẶN THOÁT TAB (Cực nghiêm)
            document.addEventListener('visibilitychange', () => {
                if (document.visibilityState === 'hidden') {
                    alert("CẢNH BÁO: PHÁT HIỆN THOÁT TAB. HỆ THỐNG ĐÃ TỰ ĐỘNG NỘP BÀI!");
                    submitExam();
                }
            });

            window.onbeforeunload = () => { return "Bạn có chắc muốn thoát? Bài thi sẽ bị nộp ngay!"; };
        }

        function startTimer(duration) {
            let t = duration;
            const display = document.getElementById('timer');
            const interval = setInterval(() => {
                let m = Math.floor(t / 60);
                let s = t % 60;
                display.innerText = `${m}:${s < 10 ? '0'+s : s}`;
                if (t <= 0) { clearInterval(interval); submitExam(); }
                t--;
            }, 1000);
        }

        function initNav() {
            const nav = document.getElementById('exam-nav');
            for(let i=1; i<=40; i++) {
                const b = document.createElement('button');
                b.className = "h-11 border-2 border-slate-100 rounded-xl font-black text-xs hover:border-blue-500 transition-all text-slate-400";
                b.innerText = i < 10 ? '0'+i : i;
                nav.appendChild(b);
            }
        }

        function confirmSubmit() { if(confirm("Nộp bài ngay bây giờ?")) submitExam(); }

        function submitExam() {
            window.onbeforeunload = null;
            showPage('page-result');
        }

        function toggleAIBox() {
            const sel = document.getElementById('ai-select');
            const box = document.getElementById('ai-sol-box');
            if(sel.value !== "") box.classList.remove('hidden');
            else box.classList.add('hidden');
        }
    </script>
</body>
</html>
