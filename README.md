fallxyz-store/
├── index.html      (Tampilan utama)
├── styles.css     (Desain/UI)
└── script.js      (Logika & interaksi)
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fallxyz Store - Top Up & Shop</title>
    <link rel="stylesheet" href="styles.css">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
</head>
<body>
    <!-- Navbar -->
    <nav class="navbar">
        <div class="logo">
            <i class="fas fa-gamepad"></i>
            <span>Fallxyz</span> Store
        </div>
        <ul class="nav-menu">
            <li><a href="#" onclick="showPage('home')" class="active"><i class="fas fa-home"></i> Home</a></li>
            <li><a href="#" onclick="showPage('products')"><i class="fas fa-shopping-bag"></i> Produk</a></li>
            <li><a href="#" onclick="showPage('orders')"><i class="fas fa-box"></i> Pesanan</a></li>
            <li><a href="#" onclick="showPage('admin')"><i class="fas fa-cog"></i> Admin</a></li>
        </ul>
        <div class="hamburger">
            <span></span>
            <span></span>
            <span></span>
        </div>
    </nav>

    <!-- Main Content -->
    <main id="app">
        <!-- HOME PAGE -->
        <section id="home" class="page active">
            <div class="hero">
                <div class="hero-content">
                    <h1>Welcome to <span class="highlight">Fallxyz Store</span></h1>
                    <p>Top up game favoritmu dan beli produk eksklusif hanya di sini!</p>
                    <div class="hero-buttons">
                        <button class="btn-primary" onclick="showPage('products')">
                            <i class="fas fa-shopping-cart"></i> Belanja Sekarang
                        </button>
                        <button class="btn-secondary" onclick="showPage('admin')">
                            <i class="fas fa-user-cog"></i> Panel Admin
                        </button>
                    </div>
                </div>
                <div class="hero-image">
                    <i class="fas fa-ghost"></i>
                </div>
            </div>
            
            <div class="features">
                <div class="feature-card">
                    <i class="fas fa-bolt"></i>
                    <h3>Proses Cepat</h3>
                    <p>Top up dalam hitungan menit</p>
                </div>
                <div class="feature-card">
                    <i class="fas fa-shield-alt"></i>
                    <h3>Aman Terpercaya</h3>
                    <p>Transaksi terjamin aman</p>
                </div>
                <div class="feature-card">
                    <i class="fas fa-headset"></i>
                    <h3>Support 24/7</h3>
                    <p>Siap membantu kapan saja</p>
                </div>
            </div>
        </section>

        <!-- PRODUCTS PAGE -->
        <section id="products" class="page">
            <div class="page-header">
                <h2><i class="fas fa-shopping-bag"></i> Produk Kami</h2>
                <div class="filter">
                    <select id="categoryFilter" onchange="filterProducts()">
                        <option value="all">Semua Kategori</option>
                        <option value="topup">Top Up Game</option>
                        <option value="akun">Akun Game</option>
                        <option value="voucher">Voucher</option>
                    </select>
                </div>
            </div>
            <div id="productsGrid" class="products-grid">
                <!-- Produk akan di-generate oleh JS -->
            </div>
        </section>

        <!-- ORDERS PAGE -->
        <section id="orders" class="page">
            <div class="page-header">
                <h2><i class="fas fa-box"></i> Pesanan Masuk</h2>
                <button class="btn-refresh" onclick="loadOrders()">
                    <i class="fas fa-sync-alt"></i> Refresh
                </button>
            </div>
            <div id="ordersList" class="orders-list">
                <!-- Pesanan akan di-generate oleh JS -->
            </div>
        </section>

        <!-- ADMIN PAGE -->
        <section id="admin" class="page">
            <div class="page-header">
                <h2><i class="fas fa-cog"></i> Panel Admin</h2>
                <button class="btn-primary" onclick="toggleAddProduct()">
                    <i class="fas fa-plus"></i> Tambah Produk
                </button>
            </div>

            <!-- Add Product Form -->
            <div id="addProductForm" class="admin-form hidden">
                <h3>Tambah Produk Baru</h3>
                <form onsubmit="addProduct(event)">
                    <div class="form-group">
                        <label>Nama Produk</label>
                        <input type="text" id="productName" required placeholder="Contoh: MLBB 86 Diamonds">
                    </div>
                    <div class="form-group">
                        <label>Kategori</label>
                        <select id="productCategory" required>
                            <option value="topup">Top Up Game</option>
                            <option value="akun">Akun Game</option>
                            <option value="voucher">Voucher</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Harga (Rp)</label>
                        <input type="number" id="productPrice" required placeholder="Contoh: 50000">
                    </div>
                    <div class="form-group">
                        <label>Deskripsi</label>
                        <textarea id="productDesc" required placeholder="Deskripsi produk..."></textarea>
                    </div>
                    <div class="form-group">
                        <label>Icon/Emoji</label>
                        <input type="text" id="productIcon" required placeholder="🎮" maxlength="5">
                    </div>
                    <div class="form-buttons">
                        <button type="submit" class="btn-success">
                            <i class="fas fa-check"></i> Simpan
                        </button>
                        <button type="button" class="btn-danger" onclick="toggleAddProduct()">
                            <i class="fas fa-times"></i> Batal
                        </button>
                    </div>
                </form>
            </div>

            <!-- Stats -->
            <div class="admin-stats">
                <div class="stat-card">
                    <i class="fas fa-box-open"></i>
                    <div class="stat-info">
                        <span class="stat-number" id="totalProducts">0</span>
                        <span class="stat-label">Total Produk</span>
                    </div>
                </div>
                <div class="stat-card">
                    <i class="fas fa-shopping-cart"></i>
                    <div class="stat-info">
                        <span class="stat-number" id="totalOrders">0</span>
                        <span class="stat-label">Pesanan</span>
                    </div>
                </div>
                <div class="stat-card">
                    <i class="fas fa-wallet"></i>
                    <div class="stat-info">
                        <span class="stat-number" id="totalSales">Rp 0</span>
                        <span class="stat-label">Total Penjualan</span>
                    </div>
                </div>
            </div>

            <!-- Edit Products Table -->
            <div class="admin-products">
                <h3>Kelola Produk</h3>
                <table id="productsTable">
                    <thead>
                        <tr>
                            <th>Icon</th>
                            <th>Nama</th>
                            <th>Kategori</th>
                            <th>Harga</th>
                            <th>Aksi</th>
                        </tr>
                    </thead>
                    <tbody id="productsTableBody">
                        <!-- Data produk -->
                    </tbody>
                </table>
            </div>

            <!-- Payment Settings -->
            <div class="admin-payment">
                <h3>Pengaturan Pembayaran</h3>
                <form onsubmit="savePaymentSettings(event)">
                    <div class="form-group">
                        <label>Nomor Dana</label>
                        <input type="text" id="danaNumber" placeholder="0812xxxxx">
                    </div>
                    <div class="form-group">
                        <label>QRIS Link (atau generate dari qris.io)</label>
                        <textarea id="qrisLink" placeholder="Masukkan link QRIS..."></textarea>
                    </div>
                    <button type="submit" class="btn-success">
                        <i class="fas fa-save"></i> Simpan Pengaturan
                    </button>
                </form>
            </div>
        </section>

        <!-- CHECKOUT MODAL -->
        <div id="checkoutModal" class="modal hidden">
            <div class="modal-content">
                <span class="close-modal" onclick="closeCheckout()">&times;</span>
                <h2><i class="fas fa-shopping-cart"></i> Checkout</h2>
                <div id="checkoutProduct" class="checkout-product">
                    <!-- Info produk -->
                </div>
                
                <div class="payment-methods">
                    <h3>Pilih Metode Pembayaran</h3>
                    <div class="payment-options">
                        <label class="payment-option" onclick="selectPayment('qris')">
                            <input type="radio" name="payment" value="qris">
                            <div class="payment-card">
                                <i class="fas fa-qrcode"></i>
                                <span>QRIS</span>
                            </div>
                        </label>
                        <label class="payment-option" onclick="selectPayment('dana')">
                            <input type="radio" name="payment" value="dana">
                            <div class="payment-card">
                                <i class="fas fa-wallet"></i>
                                <span>DANA</span>
                            </div>
                        </label>
                    </div>
                </div>

                <div id="paymentDetails" class="payment-details hidden">
                    <!-- QRIS or Dana details -->
                </div>

                <div class="customer-form">
                    <h3>Data Pembeli</h3>
                    <div class="form-group">
                        <label>Nama</label>
                        <input type="text" id="buyerName" required placeholder="Nama Lengkap">
                    </div>
                    <div class="form-group">
                        <label>No. WhatsApp</label>
                        <input type="text" id="buyerPhone" required placeholder="0812xxxxx">
                    </div>
                    <div class="form-group">
                        <label>ID Game / Email</label>
                        <input type="text" id="buyerId" required placeholder="ID game atau email">
                    </div>
                </div>

                <button class="btn-primary btn-block" onclick="processOrder()">
                    <i class="fas fa-paper-plane"></i> Kirim Pesanan
                </button>
            </div>
        </div>

        <!-- SUCCESS MODAL -->
        <div id="successModal" class="modal hidden">
            <div class="modal-content success-content">
                <i class="fas fa-check-circle"></i>
                <h2>Pesanan Berhasil!</h2>
                <p>Silakan lakukan pembayaran sesuai instruksi.</p>
                <p class="order-id">Order ID: <span id="successOrderId"></span></p>
                <button class="btn-primary" onclick="closeSuccess()">Tutup</button>
            </div>
        </div>
    </main>

    <!-- Footer -->
    <footer>
        <div class="footer-content">
            <div class="footer-logo">
                <i class="fas fa-gamepad"></i>
                <span>Fallxyz</span> Store
            </div>
            <p>Top up game & produk digital terpercaya</p>
            <div class="social-links">
                <a href="#"><i class="fab fa-whatsapp"></i></a>
                <a href="#"><i class="fab fa-instagram"></i></a>
                <a href="#"><i class="fab fa-tiktok"></i></a>
                <a href="#"><i class="fab fa-discord"></i></a>
            </div>
            <p class="copyright">© 2024 Fallxyz Store. All rights reserved.</p>
        </div>
    </footer>

    <script src="script.js"></script>
</body>
</html>
