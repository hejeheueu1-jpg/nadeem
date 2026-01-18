<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WhatsApp Store</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: #f8f9fa;
            color: #333;
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            min-height: 44px;
            transition: all 0.3s;
        }

        .btn-primary {
            background: #25D366;
            color: white;
        }

        .btn-primary:hover {
            background: #1fa855;
        }

        .btn-secondary {
            background: #075E54;
            color: white;
        }

        .btn-danger {
            background: #dc3545;
            color: white;
        }

        .card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .input-group {
            margin-bottom: 15px;
        }

        .input-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #555;
        }

        .input-group input,
        .input-group select,
        .input-group textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            min-height: 44px;
        }

        .input-group input:focus,
        .input-group select:focus,
        .input-group textarea:focus {
            outline: none;
            border-color: #25D366;
        }

        .hidden {
            display: none !important;
        }

        /* Store Header */
        .store-header {
            background: #075E54;
            color: white;
            padding: 20px;
            text-align: center;
        }

        .store-header h1 {
            margin-bottom: 10px;
        }

        .category-filter {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding: 15px;
            background: white;
            margin-bottom: 20px;
            border-radius: 12px;
        }

        .category-btn {
            padding: 10px 20px;
            background: #e0e0e0;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            white-space: nowrap;
            min-height: 44px;
            transition: all 0.3s;
        }

        .category-btn.active {
            background: #25D366;
            color: white;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 80px;
        }

        .product-card {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            transition: transform 0.3s;
        }

        .product-card:hover {
            transform: translateY(-5px);
        }

        .product-card img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }

        .product-card .product-info {
            padding: 15px;
        }

        .product-card h3 {
            margin-bottom: 10px;
            color: #333;
        }

        .product-card .price {
            font-size: 24px;
            font-weight: bold;
            color: #25D366;
            margin-bottom: 10px;
        }

        .product-card .stock {
            font-size: 14px;
            margin-bottom: 10px;
        }

        .stock.in-stock {
            color: #25D366;
        }

        .stock.out-of-stock {
            color: #dc3545;
        }

        .quantity-control {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 10px;
        }

        .quantity-control button {
            width: 44px;
            height: 44px;
            border: none;
            background: #e0e0e0;
            border-radius: 6px;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
        }

        .quantity-control input {
            width: 60px;
            text-align: center;
            border: 2px solid #e0e0e0;
            border-radius: 6px;
            padding: 8px;
            font-size: 16px;
        }

        /* Floating Cart */
        .floating-cart {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: #25D366;
            color: white;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
            font-size: 24px;
            z-index: 1000;
        }

        .cart-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background: #dc3545;
            color: white;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            font-weight: bold;
        }

        /* Cart Panel */
        .cart-panel {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: white;
            border-radius: 20px 20px 0 0;
            box-shadow: 0 -4px 20px rgba(0,0,0,0.2);
            max-height: 80vh;
            overflow-y: auto;
            transform: translateY(100%);
            transition: transform 0.3s;
            z-index: 1001;
            padding: 20px;
        }

        .cart-panel.open {
            transform: translateY(0);
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            border-bottom: 1px solid #e0e0e0;
        }

        /* Modal */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            padding: 20px;
        }

        .modal-content {
            background: white;
            border-radius: 16px;
            padding: 30px;
            max-width: 500px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            padding: 0;
            width: 44px;
            height: 44px;
        }

        /* Notifications */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #25D366;
            color: white;
            padding: 15px 20px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
            z-index: 3000;
            animation: slideIn 0.3s;
        }

        @keyframes slideIn {
            from {
                transform: translateX(400px);
            }
            to {
                transform: translateX(0);
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .products-grid {
                grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
                gap: 15px;
            }

            .product-card img {
                height: 150px;
            }
        }
    </style>
</head>
<body>
    <!-- Customer Store -->
    <div class="store-header">
        <h1 id="storeTitle">🛍️ My WhatsApp Store</h1>
        <p id="storeTagline">Quality Products at Your Doorstep</p>
        <button class="btn btn-primary" style="margin-top: 10px;" onclick="contactWhatsApp()">📱 Contact Us</button>
    </div>

    <div class="container">
        <div class="card">
            <div class="category-filter" id="categoryFilter"></div>
        </div>

        <div class="products-grid" id="storeProducts"></div>
    </div>

    <!-- Floating Cart -->
    <div class="floating-cart" onclick="toggleCart()">
        🛒
        <div class="cart-badge" id="cartBadge">0</div>
    </div>

    <!-- Cart Panel -->
    <div class="cart-panel" id="cartPanel">
        <div class="cart-header">
            <h2>Shopping Cart</h2>
            <button class="close-btn" onclick="toggleCart()">✕</button>
        </div>
        <div id="cartItems"></div>
        <div class="card" style="margin-top: 20px;">
            <h3>Payment Method</h3>
            <div class="input-group">
                <select id="paymentMethod" onchange="updateCartTotal()">
                    <option value="cod">Cash on Delivery</option>
                    <option value="pickup">Pick Up (Free)</option>
                </select>
            </div>
            <div style="margin-top: 15px;">
                <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                    <span>Subtotal:</span>
                    <strong id="cartSubtotal">Rs 0</strong>
                </div>
                <div style="display: flex; justify-content: space-between; margin-bottom: 10px;">
                    <span>Delivery:</span>
                    <strong id="cartDelivery">Rs 0</strong>
                </div>
                <div style="display: flex; justify-content: space-between; font-size: 20px; color: #25D366;">
                    <span>Total:</span>
                    <strong id="cartTotal">Rs 0</strong>
                </div>
            </div>
            <button class="btn btn-primary" style="width: 100%; margin-top: 15px;" onclick="showCheckoutModal()">Checkout via WhatsApp</button>
        </div>
    </div>

    <!-- Checkout Modal -->
    <div id="checkoutModal" class="modal hidden">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Checkout</h2>
                <button class="close-btn" onclick="closeCheckoutModal()">✕</button>
            </div>
            <div class="input-group">
                <label>Your Name *</label>
                <input type="text" id="customerName" required>
            </div>
            <div class="input-group">
                <label>Phone Number *</label>
                <input type="tel" id="customerPhone" required>
            </div>
            <div class="input-group">
                <label>Delivery Address *</label>
                <textarea id="customerAddress" rows="3" required></textarea>
            </div>
            <button class="btn btn-primary" style="width: 100%;" onclick="submitOrder()">Send Order to WhatsApp</button>
        </div>
    </div>

    <script>
        // Load data from localStorage
        let products = [];
        let categories = [];
        let settings = {};
        let orders = [];
        let cart = [];

        // Load store data on page load
        function loadStoreData() {
            products = JSON.parse(localStorage.getItem('products')) || [];
            categories = JSON.parse(localStorage.getItem('categories')) || ['Electronics', 'Clothing', 'Food', 'Accessories'];
            settings = JSON.parse(localStorage.getItem('settings')) || {
                storeName: 'My WhatsApp Store',
                storePhone: '03079915847',
                storeAddress: 'Shop Address',
                deliveryCharges: 100,
                whatsappNumber: '03079915847'
            };
            orders = JSON.parse(localStorage.getItem('orders')) || [];
            
            document.getElementById('storeTitle').textContent = '🛍️ ' + settings.storeName;
            loadCategoryFilters();
            loadStoreProducts();
        }

        function loadCategoryFilters() {
            const container = document.getElementById('categoryFilter');
            container.innerHTML = `
                <button class="category-btn active" onclick="filterCategory('all')">All</button>
                ${categories.map(cat => `<button class="category-btn" onclick="filterCategory('${cat}')">${cat}</button>`).join('')}
            `;
        }

        function filterCategory(category) {
            document.querySelectorAll('.category-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            loadStoreProducts(category);
        }

        function loadStoreProducts(filterCat = 'all') {
            const container = document.getElementById('storeProducts');
            let displayProducts = filterCat === 'all' ? products : products.filter(p => p.category === filterCat);
            displayProducts.sort((a, b) => b.stock - a.stock);

            if (displayProducts.length === 0) {
                container.innerHTML = '<div class="card"><p style="text-align: center; color: #666;">No products available in this category.</p></div>';
                return;
            }

            container.innerHTML = displayProducts.map(p => `
                <div class="product-card">
                    <img src="${p.image}" alt="${p.name}">
                    <div class="product-info">
                        <h3>${p.name}</h3>
                        <div class="price">Rs ${p.price}</div>
                        <div class="stock ${p.stock > 0 ? 'in-stock' : 'out-of-stock'}">
                            ${p.stock > 0 ? `✓ In Stock (${p.stock})` : '✗ Out of Stock'}
                        </div>
                        ${p.stock > 0 ? `
                            <div class="quantity-control">
                                <button onclick="changeQuantity(${p.id}, -1)">-</button>
                                <input type="number" id="qty-${p.id}" value="1" min="1" max="${p.stock}" readonly>
                                <button onclick="changeQuantity(${p.id}, 1)">+</button>
                            </div>
                            <button class="btn btn-primary" style="width: 100%;" onclick="addToCart(${p.id})">Add to Cart</button>
                        ` : `
                            <button class="btn btn-secondary" style="width: 100%;" disabled>Out of Stock</button>
                        `}
                    </div>
                </div>
            `).join('');
        }

        function changeQuantity(productId, change) {
            const input = document.getElementById(`qty-${productId}`);
            const product = products.find(p => p.id === productId);
            let newValue = parseInt(input.value) + change;
            
            if (newValue < 1) newValue = 1;
            if (newValue > product.stock) newValue = product.stock;
            
            input.value = newValue;
        }

        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const quantity = parseInt(document.getElementById(`qty-${productId}`).value);
            
            const existingItem = cart.find(item => item.id === productId);
            if (existingItem) {
                existingItem.quantity += quantity;
            } else {
                cart.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    quantity: quantity
                });
            }
            
            updateCartBadge();
            showNotification('Added to cart!');
        }

        function updateCartBadge() {
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            document.getElementById('cartBadge').textContent = totalItems;
        }

        function toggleCart() {
            const panel = document.getElementById('cartPanel');
            panel.classList.toggle('open');
            if (panel.classList.contains('open')) {
                renderCart();
            }
        }

        function renderCart() {
            const container = document.getElementById('cartItems');
            if (cart.length === 0) {
                container.innerHTML = '<p>Your cart is empty</p>';
                updateCartTotal();
                return;
            }

            container.innerHTML = cart.map(item => `
                <div class="cart-item">
                    <div>
                        <strong>${item.name}</strong><br>
                        Rs ${item.price} x ${item.quantity}
                    </div>
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <div class="quantity-control">
                            <button onclick="updateCartQuantity(${item.id}, -1)">-</button>
                            <input type="number" value="${item.quantity}" readonly style="width: 50px;">
                            <button onclick="updateCartQuantity(${item.id}, 1)">+</button>
                        </div>
                        <button class="btn btn-danger" style="padding: 8px 16px;" onclick="removeFromCart(${item.id})">Remove</button>
                    </div>
                </div>
            `).join('');

            updateCartTotal();
        }

        function updateCartQuantity(productId, change) {
            const item = cart.find(i => i.id === productId);
            const product = products.find(p => p.id === productId);
            
            item.quantity += change;
            
            if (item.quantity < 1) {
                removeFromCart(productId);
                return;
            }
            
            if (item.quantity > product.stock) {
                item.quantity = product.stock;
                showNotification('Maximum stock reached!', 'error');
            }
            
            updateCartBadge();
            renderCart();
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartBadge();
            renderCart();
        }

        function updateCartTotal() {
            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const paymentMethod = document.getElementById('paymentMethod').value;
            const delivery = paymentMethod === 'cod' ? settings.deliveryCharges : 0;
            const total = subtotal + delivery;

            document.getElementById('cartSubtotal').textContent = 'Rs ' + subtotal;
            document.getElementById('cartDelivery').textContent = 'Rs ' + delivery;
            document.getElementById('cartTotal').textContent = 'Rs ' + total;
        }

        function showCheckoutModal() {
            if (cart.length === 0) {
                showNotification('Your cart is empty!', 'error');
                return;
            }
            document.getElementById('checkoutModal').classList.remove('hidden');
        }

        function closeCheckoutModal() {
            document.getElementById('checkoutModal').classList.add('hidden');
        }

        function submitOrder() {
            const name = document.getElementById('customerName').value.trim();
            const phone = document.getElementById('customerPhone').value.trim();
            const address = document.getElementById('customerAddress').value.trim();

            if (!name || !phone || !address) {
                showNotification('Please fill all fields!', 'error');
                return;
            }

            const paymentMethod = document.getElementById('paymentMethod').value;
            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const delivery = paymentMethod === 'cod' ? settings.deliveryCharges : 0;
            const total = subtotal + delivery;

            // Create WhatsApp message
            let message = `🛍️ *NEW ORDER - ${settings.storeName}*\n\n`;
            message += `👤 *Customer:* ${name}\n`;
            message += `📞 *Phone:* ${phone}\n`;
            message += `📍 *Address:* ${address}\n\n`;
            message += `📦 *Order Details:*\n`;
            
            cart.forEach(item => {
                message += `• ${item.name} x ${item.quantity} = Rs ${item.price * item.quantity}\n`;
            });
            
            message += `\n💵 *Subtotal:* Rs ${subtotal}\n`;
            if (delivery > 0) {
                message += `🚚 *Delivery:* Rs ${delivery}\n`;
            }
            message += `💰 *Total:* Rs ${total}\n\n`;
            message += `💳 *Payment:* ${paymentMethod === 'cod' ? 'Cash on Delivery' : 'Pick Up'}\n`;
            message += `📅 *Order Date:* ${new Date().toLocaleString()}`;

            // Save order
            const order = {
                id: Date.now(),
                customerName: name,
                customerPhone: phone,
                customerAddress: address,
                items: cart.map(item => ({
                    ...item,
                    total: item.price * item.quantity
                })),
                subtotal,
                delivery,
                total,
                paymentMethod,
                date: new Date().toLocaleString()
            };

            orders.push(order);
            localStorage.setItem('orders', JSON.stringify(orders));

            // Update stock
            cart.forEach(item => {
                const product = products.find(p => p.id === item.id);
                if (product) {
                    product.stock -= item.quantity;
                }
            });
            localStorage.setItem('products', JSON.stringify(products));

            // Send to WhatsApp
            const encodedMessage = encodeURIComponent(message);
            const whatsappUrl = `https://wa.me/${settings.whatsappNumber}?text=${encodedMessage}`;
            window.open(whatsappUrl, '_blank');

            // Clear cart
            cart = [];
            updateCartBadge();
            closeCheckoutModal();
            toggleCart();
            showNotification('Order sent to WhatsApp!');
            
            // Clear form
            document.getElementById('customerName').value = '';
            document.getElementById('customerPhone').value = '';
            document.getElementById('customerAddress').value = '';
            
            // Reload products
            loadStoreData();
        }

        function contactWhatsApp() {
            const message = encodeURIComponent(`Hi! I'm interested in your products.`);
            window.open(`https://wa.me/${settings.whatsappNumber}?text=${message}`, '_blank');
        }

        // Notification
        function showNotification(message, type = 'success') {
            const notif = document.createElement('div');
            notif.className = 'notification';
            notif.textContent = message;
            if (type === 'error') {
                notif.style.background = '#dc3545';
            }
            document.body.appendChild(notif);
            
            setTimeout(() => {
                notif.remove();
            }, 3000);
        }

        // Auto-refresh products every 5 seconds to sync with admin updates
        setInterval(() => {
            const currentFilterBtn = document.querySelector('.category-btn.active');
            if (currentFilterBtn) {
                const currentFilter = currentFilterBtn.textContent;
                const newProducts = JSON.parse(localStorage.getItem('products')) || [];
                if (JSON.stringify(newProducts) !== JSON.stringify(products)) {
                    products = newProducts;
                    if (currentFilter === 'All') {
                        loadStoreProducts('all');
                    } else {
                        loadStoreProducts(currentFilter);
                    }
                }
            }
        }, 5000);

        // Initialize store on page load
        window.addEventListener('DOMContentLoaded', loadStoreData);
    </script>
</body>
</html>
