<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Truy xuất nguồn gốc BAF - Ba Rọi Heo</title>
    <style>
        :root {
            --gold-text: #B48500;
            --blue-text: #0066CC;
            --gray-label: #888888;
            --border-gold: #D4A017;
            --bg-pattern: #FDF7E7;
            --success-green: #2e7d32;
            --baf-green: #4db6ac;
            --timeline-line: #e0e0e0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
            margin: 0; padding: 0; background-color: #f4f6f9; color: #333;
        }

        /* Header Cục Chăn Nuôi */
        .header {
            background-color: var(--bg-pattern);
            background-image: url('https://www.transparenttextures.com/patterns/natural-paper.png');
            padding: 12px 15px; display: flex; align-items: center; justify-content: space-between;
            border-bottom: 2px solid var(--border-gold); position: sticky; top: 0; z-index: 100;
        }
        .header-left { display: flex; align-items: center; }
        .logo { width: 45px; height: 45px; margin-right: 10px; }
        .header-titles h1 { font-size: 9px; margin: 0; color: var(--gold-text); text-transform: uppercase; font-weight: 700; }
        .header-titles h2 { font-size: 13px; margin: 2px 0 0 0; color: var(--gold-text); font-weight: 800; text-transform: uppercase; }

        .container { max-width: 600px; margin: 0 auto; background: #fff; min-height: 100vh; box-shadow: 0 0 10px rgba(0,0,0,0.05); padding-bottom: 40px; }

        /* --- PRODUCT HERO SECTION --- */
        .product-hero {
            padding: 30px 20px; background: #fff; text-align: center; border-bottom: 1px solid #f0f0f0;
        }
        .product-name { font-size: 32px; font-weight: 900; color: #000; margin: 0; text-transform: uppercase; letter-spacing: 1px; }
        
        .product-image-box {
            width: 100%; max-width: 450px; margin: 15px auto; border-radius: 16px; overflow: hidden;
            display: flex; align-items: center; justify-content: center; position: relative;
            background-color: #fcfcfc; min-height: 250px;
        }
        
        .product-image-box img {
            width: 100%; height: auto; display: block;
            filter: drop-shadow(0 8px 15px rgba(0,0,0,0.1));
            transition: transform 0.4s ease;
        }

        .product-weight { font-size: 18px; color: var(--gray-label); margin: 0 0 25px 0; font-weight: 500; }
        
        .label-summary {
            display: grid; grid-template-columns: 1fr 1fr; gap: 12px;
        }
        .summary-card {
            background: #fff; padding: 15px 10px; border-radius: 12px; border: 1px solid #f0f0f0; text-align: center;
            box-shadow: 0 2px 6px rgba(0,0,0,0.02);
        }
        .s-label { font-size: 11px; color: var(--gray-label); text-transform: uppercase; margin-bottom: 6px; display: block; }
        .s-value { font-size: 15px; font-weight: 800; color: #333; display: block; }

        /* --- ACCORDION SECTIONS --- */
        .trace-card {
            margin: 20px 15px; border-radius: 16px; border: 1px solid #eee; background: #fff; overflow: hidden;
            box-shadow: 0 4px 12px rgba(0,0,0,0.03);
        }
        .card-header {
            padding: 20px; display: flex; align-items: center; justify-content: space-between; cursor: pointer;
        }
        .card-title-box { display: flex; align-items: center; gap: 15px; }
        .card-icon {
            width: 48px; height: 48px; background: var(--blue-text); border-radius: 12px;
            display: flex; align-items: center; justify-content: center;
        }
        .card-icon.orange { background: #fb8c00; }
        .card-icon.green { background: #43a047; }
        .card-icon svg { fill: white; width: 24px; }

        .card-text h3 { margin: 0; font-size: 17px; font-weight: 800; color: #000; }
        .card-text p { margin: 4px 0 0 0; font-size: 13px; color: var(--gray-label); }

        .btn-expand {
            color: var(--blue-text); font-size: 13px; font-weight: 700; display: flex; align-items: center; gap: 4px;
        }
        .btn-expand::after { content: '▾'; font-size: 14px; transition: transform 0.3s; }
        .open-header .btn-expand::after { transform: rotate(180deg); }

        .card-dropdown {
            max-height: 0; overflow: hidden; transition: max-height 0.4s ease-out; background: #fafafa;
        }
        .card-dropdown.active { max-height: 600px; border-top: 1px solid #f0f0f0; }
        .list-info { padding: 20px; }
        .list-row { margin-bottom: 15px; }
        .l-label { font-size: 12px; color: var(--gray-label); display: block; margin-bottom: 3px; }
        .l-value { font-size: 15px; color: #333; font-weight: 600; line-height: 1.4; }

        /* --- TIMELINE (LOGIC REVERSED: 24/04/2026) --- */
        .timeline-box { padding: 10px 15px 30px 20px; }
        .timeline-item { position: relative; padding-left: 55px; margin-bottom: 35px; }
        .timeline-item::before {
            content: ""; position: absolute; left: 24px; top: 48px; bottom: -35px; border-left: 2px solid var(--timeline-line);
        }
        .timeline-item:last-child::before { display: none; }
        .time-icon {
            position: absolute; left: 0; top: 0; width: 48px; height: 48px; border: 2px solid #e0f2f1; border-radius: 50%;
            display: flex; align-items: center; justify-content: center; background: white; z-index: 2;
        }
        .time-icon img { width: 26px; }
        .item-head { display: flex; justify-content: space-between; align-items: center; }
        .item-cat { font-size: 11px; color: var(--gray-label); font-weight: 700; text-transform: uppercase; }
        .btn-modal { background: var(--baf-green); color: white; border: none; padding: 4px 12px; border-radius: 6px; font-size: 11px; font-weight: 700; cursor: pointer; }
        .item-title { font-size: 15px; font-weight: 700; color: #000; margin: 6px 0; line-height: 1.4; }
        .item-time-label { font-size: 12px; color: #999; font-style: italic; }

        /* Modal Style */
        .modal {
            display: none; position: fixed; z-index: 1000; left: 0; top: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.75); backdrop-filter: blur(4px);
        }
        .modal-content {
            background: #fff; margin: 12% auto; border-radius: 20px; width: 90%; max-width: 480px; overflow: hidden; animation: slideUp 0.3s ease-out;
        }
        @keyframes slideUp { from { transform: translateY(80px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        .modal-header { background: var(--bg-pattern); padding: 18px 20px; border-bottom: 2px solid var(--border-gold); display: flex; justify-content: space-between; align-items: center; }
        .modal-header h3 { margin: 0; font-size: 14px; color: var(--gold-text); font-weight: 800; text-transform: uppercase; }
        .close-modal { font-size: 30px; cursor: pointer; color: #999; }
        .modal-body { padding: 25px; max-height: 60vh; overflow-y: auto; }
        .m-row { margin-bottom: 15px; border-bottom: 1px solid #f5f5f5; padding-bottom: 8px; }
        .m-label { font-size: 11px; color: var(--gray-label); display: block; margin-bottom: 4px; }
        .m-val { font-size: 14px; color: #333; font-weight: 600; line-height: 1.5; }

        .hotline { background: #fdf2f2; padding: 16px; margin: 20px 15px; border-radius: 12px; display: flex; align-items: center; justify-content: center; color: #c62828; font-weight: 800; text-decoration: none; font-size: 15px; }
        footer { text-align: center; padding: 30px; color: #bbb; font-size: 11px; border-top: 1px solid #eee; }
    </style>
</head>
<body>

    <header class="header">
        <div class="header-left">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a1/Emblem_of_Vietnam.svg/2048px-Emblem_of_Vietnam.svg.png" class="logo" alt="Quốc huy">
            <div class="header-titles">
                <h1>Bộ Nông nghiệp và Phát triển nông thôn - Cục chăn nuôi và thú y</h1>
                <h2>CƠ SỞ DỮ LIỆU QUỐC GIA VỀ CHĂN NUÔI</h2>
            </div>
        </div>
        <div class="menu-btn">☰</div>
    </header>

    <div class="container">
        <!-- HERO SECTION -->
        <section class="product-hero">
            <h1 class="product-name">Ba Rọi Heo</h1>
            
            <div class="product-image-box">
                <!-- Cập nhật Link ảnh mới & Cơ chế Fallback tối ưu cho Mr. Hiệp -->
                <img id="productImage" 
                     src="https://baf.vn/wp-content/uploads/2022/02/BA-ROI-1-1-scaled.png" 
                     alt="Ba Rọi Heo BAF Meat"
                     onerror="this.onerror=null; this.src='https://sibafood.vn/wp-content/uploads/2022/11/Ba-roi-heo-an-chay-BAF-2.png'; this.parentElement.style.backgroundColor='#fff';">
            </div>

            <p class="product-weight">Khối lượng tịnh: 300 g | Heo Ăn Chay</p>
            
            <div class="label-summary">
                <div class="summary-card"><span class="s-label">Ngày sản xuất</span><span class="s-value">24/04/2026</span></div>
                <div class="summary-card"><span class="s-label">Hạn sử dụng</span><span class="s-value">27/04/2026</span></div>
                <div class="summary-card"><span class="s-label">Lô sản xuất</span><span class="s-value">DN26032101</span></div>
                <div class="summary-card"><span class="s-label">Số VSTY</span><span class="s-value">45.02.24</span></div>
            </div>
        </section>

        <!-- MỤC LỚN 1: ĐỊNH DANH (Accordion) -->
        <div class="trace-card">
            <div class="card-header" onclick="toggleAccordion('id-info', this)">
                <div class="card-title-box">
                    <div class="card-icon"><svg viewBox="0 0 24 24"><path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/></svg></div>
                    <div class="card-text"><h3>Thông tin định danh</h3><p>Sản phẩm & Đơn vị sản xuất</p></div>
                </div>
                <span class="btn-expand">Xem thêm</span>
            </div>
            <div id="id-info" class="card-dropdown">
                <div class="list-info">
                    <div class="list-row"><span class="l-label">Tên thương hiệu</span><span class="l-value">BAF MEAT - ĂN SẠCH SỐNG KHỎE</span></div>
                    <div class="list-row"><span class="l-label">Đơn vị chủ quản</span><span class="l-value">CÔNG TY CỔ PHẦN NÔNG NGHIỆP BAF VIỆT NAM</span></div>
                    <div class="list-row"><span class="l-label">Thông điệp 3F</span><span class="l-value" style="color: var(--blue-text); font-style: italic;">"Heo ăn chay - Đảm bảo nguồn đạm thực vật, không chất tăng trọng."</span></div>
                </div>
            </div>
        </div>

        <!-- MỤC LỚN 2: NHẬT KÝ CHUỖI CUNG ỨNG (Timeline -> Modal) -->
        <div class="trace-card" style="border: none; background: transparent; box-shadow: none;">
            <div class="card-header" style="border-radius: 16px; border: 1px solid #eee; background: #fff; cursor: default;">
                <div class="card-title-box">
                    <div class="card-icon orange"><svg viewBox="0 0 24 24"><path d="M13 3H6v18h12V8l-5-5zM12 18H8v-2h4v2zm0-4H8v-2h4v2zm0-4H8V8h4v2z"/></svg></div>
                    <div class="card-text"><h3>Nhật ký chuỗi cung ứng</h3><p>Hành trình từ bàn ăn về chuồng trại (Xác thực SAP)</p></div>
                </div>
            </div>
            
            <div class="timeline-box">
                <div class="timeline-item">
                    <div class="time-icon"><img src="https://cdn-icons-png.flaticon.com/512/1162/1162456.png" alt="Shop"></div>
                    <div class="item-head"><p class="item-cat">Điểm bán lẻ</p><button class="btn-modal" onclick="showModal('retail')">Xem thêm</button></div>
                    <h4 class="item-title">Siba Food Quận 7 - TP. Hồ Chí Minh</h4>
                    <span class="item-time-label">Cập nhật: 24/04/2026 16:30 PM</span>
                </div>

                <div class="timeline-item">
                    <div class="time-icon"><img src="https://cdn-icons-png.flaticon.com/512/2554/2554978.png" alt="Log"></div>
                    <div class="item-head"><p class="item-cat">Vận chuyển lạnh</p><button class="btn-modal" onclick="showModal('logistics')">Xem thêm</button></div>
                    <h4 class="item-title">BAF Logistics Miền Nam - Xe 29C-888.68</h4>
                    <span class="item-time-label">Khởi hành: 24/04/2026 11:00 AM</span>
                </div>

                <div class="timeline-item">
                    <div class="time-icon"><img src="https://cdn-icons-png.flaticon.com/512/2855/2855519.png" alt="Pro"></div>
                    <div class="item-head"><p class="item-cat">Chế biến / Đóng gói</p><button class="btn-modal" onclick="showModal('processing')">Xem thêm</button></div>
                    <h4 class="item-title">Nhà máy thực phẩm sạch BAF Long An</h4>
                    <span class="item-time-label">NSX: 24/04/2026 07:30 AM</span>
                </div>

                <div class="timeline-item">
                    <div class="time-icon"><img src="https://cdn-icons-png.flaticon.com/512/2122/2122394.png" alt="Slaughter"></div>
                    <div class="item-head"><p class="item-cat">Cơ sở giết mổ</p><button class="btn-modal" onclick="showModal('slaughter')">Xem thêm</button></div>
                    <h4 class="item-title">Phân xưởng giết mổ công nghệ mát BAF</h4>
                    <span class="item-time-label">Thời điểm: 24/04/2026 01:15 AM</span>
                </div>

                <div class="timeline-item">
                    <div class="time-icon"><img src="https://cdn-icons-png.flaticon.com/512/2164/2164327.png" alt="Farm"></div>
                    <div class="item-head"><p class="item-cat">Trang trại (Farm)</p><button class="btn-modal" onclick="showModal('farm')">Xem thêm</button></div>
                    <h4 class="item-title">Trại lợn thịt BAF Thanh Hóa 08</h4>
                    <span class="item-time-label">Xuất chuồng: 23/04/2026 14:00 PM</span>
                </div>

                <div class="timeline-item">
                    <div class="time-icon"><img src="https://cdn-icons-png.flaticon.com/512/2111/2111531.png" alt="Feed"></div>
                    <div class="item-head"><p class="item-cat">Nhà máy Cám (Feed)</p><button class="btn-modal" onclick="showModal('feed')">Xem thêm</button></div>
                    <h4 class="item-title">Cám Chay Factory - Tây Ninh</h4>
                    <span class="item-time-label">Lô cám SAP: SLM-2025-10-20</span>
                </div>
            </div>
        </div>

        <!-- MỤC LỚN 3: TIÊU CHUẨN (Accordion) -->
        <div class="trace-card">
            <div class="card-header" onclick="toggleAccordion('std-info', this)">
                <div class="card-title-box">
                    <div class="card-icon green"><svg viewBox="0 0 24 24"><path d="M12 1L3 5v6c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V5l-9-4zm-2 16l-4-4 1.41-1.41L10 14.17l6.59-6.59L18 9l-8 8z"/></svg></div>
                    <div class="card-text"><h3>Tiêu chuẩn & Kiểm định</h3><p>Xác thực chất lượng & Cam kết SAP</p></div>
                </div>
                <span class="btn-expand">Xem thêm</span>
            </div>
            <div id="std-info" class="card-dropdown">
                <div class="list-info">
                    <div class="list-row"><span class="l-label">Chứng nhận hệ thống</span><span class="l-value">VietGAP, ISO 22000, FSSC 22000 (Chứng nhận quốc tế).</span></div>
                    <div class="list-row"><span class="l-label">Kiểm dịch thú y</span><span class="l-value" style="color: var(--success-green); font-weight: bold;">✓ ĐẠT CHUẨN (Số VSTY: 45.02.24)</span></div>
                    <div class="list-row"><span class="l-label">Xác thực hệ thống</span><span class="l-value">Dữ liệu được bảo chứng bởi SAP S/4HANA Cloud toàn cầu.</span></div>
                </div>
            </div>
        </div>

        <a href="tel:18003360" class="hotline">📞 Hotline hỗ trợ: 1800 3360</a>
        <footer>Vận hành bởi SAP S/4HANA Cloud<br>CƠ SỞ DỮ LIỆU QUỐC GIA VỀ CHĂN NUÔI © 2026</footer>
    </div>

    <!-- MODAL POPUP -->
    <div id="detailModal" class="modal">
        <div class="modal-content">
            <div class="modal-header"><h3 id="mTitle">Hồ sơ chi tiết</h3><span class="close-modal" onclick="closeModal()">&times;</span></div>
            <div id="mBody" class="modal-body"></div>
        </div>
    </div>

    <script>
        function toggleAccordion(id, header) {
            const content = document.getElementById(id);
            const isOpen = content.classList.contains('active');
            if (!isOpen) {
                content.classList.add('active');
                header.classList.add('open-header');
            } else {
                content.classList.remove('active');
                header.classList.remove('open-header');
            }
        }

        const modalData = {
            retail: `<div class="m-row"><span class="m-label">Cửa hàng:</span><span class="m-val">Siba Food Quận 7 - Sài Gòn</span></div><div class="m-row"><span class="m-label">Thời điểm lên kệ:</span><span class="m-val">24/04/2026 16:30 PM (Cùng ngày NSX)</span></div>`,
            logistics: `<div class="m-row"><span class="m-label">Vận chuyển:</span><span class="m-val">BAF Express - Xe lạnh chuyên dụng</span></div><div class="m-row"><span class="m-label">Biển số:</span><span class="m-val">29C-888.68 (Tài xế: Nguyễn Văn Thành)</span></div>`,
            processing: `<div class="m-row"><span class="m-label">Cơ sở:</span><span class="m-val">Nhà máy thực phẩm BAF Long An</span></div><div class="m-row"><span class="m-label">NSX:</span><span class="m-val">24/04/2026</span></div><div class="m-row"><span class="m-label">Công nghệ:</span><span class="m-val">Làm mát pha lóc, giữ trọn dinh dưỡng thớ thịt.</span></div>`,
            slaughter: `<div class="m-row"><span class="m-label">Cơ sở:</span><span class="m-val">Phân xưởng giết mổ công nghệ mát</span></div><div class="m-row"><span class="m-label">Nghiệp vụ:</span><span class="m-val">Heo nghỉ ngơi 4h trước pha lóc. Không Stress.</span></div>`,
            farm: `<div class="m-row"><span class="m-label">Trang trại:</span><span class="m-val">BAF Thanh Hóa 08 (Global GAP)</span></div><div class="m-row"><span class="m-label">Mã heo:</span><span class="m-val">BAF-PIG-9921 (Định danh riêng lẻ)</span></div>`,
            feed: `<div class="m-row"><span class="m-label">Loại cám:</span><span class="m-val">100% Cám Chay Factory</span></div><div class="m-row"><span class="m-label">Lợi ích:</span><span class="m-val">Giảm 80% mùi hôi trại xanh, thịt thơm tự nhiên.</span></div>`
        };

        const mTitles = { retail: "HỒ SƠ ĐIỂM BÁN", logistics: "HỒ SƠ VẬN CHUYỂN", processing: "HỒ SƠ CHẾ BIẾN", slaughter: "HỒ SƠ GIẾT MỔ", farm: "HỒ SƠ TRANG TRẠI", feed: "HỒ SƠ CÁM CHAY" };

        function showModal(type) {
            document.getElementById('mTitle').innerText = mTitles[type];
            document.getElementById('mBody').innerHTML = modalData[type];
            document.getElementById('detailModal').style.display = 'block';
        }
        function closeModal() { document.getElementById('detailModal').style.display = 'none'; }
        window.onclick = e => { if(e.target == document.getElementById('detailModal')) closeModal(); }
    </script>
</body>
</html>
