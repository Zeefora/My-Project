# My-Project
-import React, { useState, useMemo } from 'react';
import { 
  ShoppingBag, 
  User, 
  Lock, 
  Store, 
  CheckCircle, 
  Calculator, 
  LogOut, 
  CreditCard, 
  Banknote,
  AlertCircle,
  Plus,
  Minus,
  Trash2
} from 'lucide-react';

/**
 * KOMPONEN: Login
 * Menampilkan form masuk dengan pesan pengingat amanah.
 */
const Login = ({ onNavigate }) => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  const handleLogin = (e) => {
    e.preventDefault();
    onNavigate('pos');
  };

  return (
    <div className="min-h-screen flex items-center justify-center bg-[#f8fafc] p-4">
      <div className="max-w-md w-full bg-white rounded-3xl shadow-2xl overflow-hidden border border-emerald-50">
        <div className="bg-emerald-700 p-8 text-white text-center">
          <div className="bg-white/20 w-16 h-16 rounded-2xl flex items-center justify-center mx-auto mb-4 backdrop-blur-sm">
            <Store size={32} />
          </div>
          <h2 className="text-2xl font-bold">POS Syariah</h2>
          <p className="text-emerald-100 text-sm mt-1">Sistem Kasir Berkah & Amanah</p>
        </div>
        
        <div className="p-8">
          <div className="mb-8 p-4 bg-emerald-50 rounded-xl border-l-4 border-emerald-500 italic text-sm text-emerald-800">
            "Wahai orang-orang yang beriman! Janganlah kamu mengkhianati Allah dan Rasul dan (juga) janganlah kamu mengkhianati amanat yang dipercayakan kepadamu, sedang kamu mengetahui." (QS. Al-Anfal: 27)
          </div>

          <form onSubmit={handleLogin} className="space-y-5">
            <div>
              <label className="block text-xs font-semibold text-gray-500 uppercase tracking-wider mb-1">Email / Username</label>
              <div className="relative">
                <User className="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400" size={18} />
                <input 
                  type="email" 
                  className="w-full pl-10 pr-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:border-transparent outline-none transition"
                  placeholder="admin@syariahpos.com"
                  value={email}
                  onChange={(e) => setEmail(e.target.value)}
                  required
                />
              </div>
            </div>

            <div>
              <label className="block text-xs font-semibold text-gray-500 uppercase tracking-wider mb-1">Kata Sandi</label>
              <div className="relative">
                <Lock className="absolute left-3 top-1/2 -translate-y-1/2 text-gray-400" size={18} />
                <input 
                  type="password" 
                  className="w-full pl-10 pr-4 py-3 bg-gray-50 border border-gray-200 rounded-xl focus:ring-2 focus:ring-emerald-500 focus:border-transparent outline-none transition"
                  placeholder="••••••••"
                  value={password}
                  onChange={(e) => setPassword(e.target.value)}
                  required
                />
              </div>
            </div>

            <button 
              type="submit"
              className="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold py-3 rounded-xl shadow-lg shadow-emerald-200 transition transform active:scale-95"
            >
              Masuk dengan Amanah
            </button>
          </form>

          <div className="mt-6 text-center">
            <button 
              onClick={() => onNavigate('register')}
              className="text-emerald-600 hover:text-emerald-800 text-sm font-medium"
            >
              Belum punya akun? Daftar Vendor Baru
            </button>
          </div>
        </div>
      </div>
    </div>
  );
};

/**
 * KOMPONEN: Register
 * Halaman pendaftaran vendor dengan validasi data.
 */
const Register = ({ onNavigate }) => {
  const [formData, setFormData] = useState({
    shopName: '',
    ownerName: '',
    email: '',
    password: '',
    terms: false
  });
  const [errors, setErrors] = useState({});
  const [showSuccess, setShowSuccess] = useState(false);

  const validate = () => {
    let newErrors = {};
    if (!formData.shopName) newErrors.shopName = 'Nama toko wajib diisi';
    if (!formData.ownerName) newErrors.ownerName = 'Nama pemilik wajib diisi';
    if (!formData.email.includes('@')) newErrors.email = 'Email tidak valid';
    if (formData.password.length < 6) newErrors.password = 'Sandi minimal 6 karakter';
    if (!formData.terms) newErrors.terms = 'Anda harus menyetujui komitmen syariah';
    
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (validate()) {
      setShowSuccess(true);
      setTimeout(() => onNavigate('login'), 2000);
    }
  };

  return (
    <div className="min-h-screen bg-[#f1f5f9] flex items-center justify-center p-4">
      <div className="max-w-xl w-full bg-white rounded-3xl shadow-xl p-8 border border-emerald-100">
        <div className="flex justify-between items-center mb-8">
          <div>
            <h2 className="text-3xl font-extrabold text-gray-800">Daftar Vendor</h2>
            <p className="text-gray-500">Bergabung dalam ekosistem perniagaan halal</p>
          </div>
          <button onClick={() => onNavigate('login')} className="text-gray-400 hover:text-gray-600">
            <LogOut size={24} />
          </button>
        </div>

        {showSuccess ? (
          <div className="bg-emerald-50 text-emerald-800 p-8 rounded-2xl text-center animate-bounce">
            <CheckCircle size={48} className="mx-auto mb-4" />
            <h3 className="text-xl font-bold">Pendaftaran Berhasil!</h3>
            <p>Mengarahkan Anda ke halaman masuk...</p>
          </div>
        ) : (
          <form onSubmit={handleSubmit} className="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div className="md:col-span-2">
              <label className="block text-sm font-semibold text-gray-700 mb-1">Nama Toko / Usaha</label>
              <input 
                type="text" 
                className={`w-full px-4 py-3 rounded-xl border ${errors.shopName ? 'border-red-500' : 'border-gray-200'} focus:ring-2 focus:ring-emerald-500 outline-none`}
                onChange={(e) => setFormData({...formData, shopName: e.target.value})}
              />
              {errors.shopName && <p className="text-red-500 text-xs mt-1">{errors.shopName}</p>}
            </div>

            <div>
              <label className="block text-sm font-semibold text-gray-700 mb-1">Nama Lengkap Pemilik</label>
              <input 
                type="text" 
                className={`w-full px-4 py-3 rounded-xl border ${errors.ownerName ? 'border-red-500' : 'border-gray-200'} focus:ring-2 focus:ring-emerald-500 outline-none`}
                onChange={(e) => setFormData({...formData, ownerName: e.target.value})}
              />
              {errors.ownerName && <p className="text-red-500 text-xs mt-1">{errors.ownerName}</p>}
            </div>

            <div>
              <label className="block text-sm font-semibold text-gray-700 mb-1">Alamat Email</label>
              <input 
                type="email" 
                className={`w-full px-4 py-3 rounded-xl border ${errors.email ? 'border-red-500' : 'border-gray-200'} focus:ring-2 focus:ring-emerald-500 outline-none`}
                onChange={(e) => setFormData({...formData, email: e.target.value})}
              />
              {errors.email && <p className="text-red-500 text-xs mt-1">{errors.email}</p>}
            </div>

            <div className="md:col-span-2">
              <label className="block text-sm font-semibold text-gray-700 mb-1">Kata Sandi</label>
              <input 
                type="password" 
                className={`w-full px-4 py-3 rounded-xl border ${errors.password ? 'border-red-500' : 'border-gray-200'} focus:ring-2 focus:ring-emerald-500 outline-none`}
                onChange={(e) => setFormData({...formData, password: e.target.value})}
              />
              {errors.password && <p className="text-red-500 text-xs mt-1">{errors.password}</p>}
            </div>

            <div className="md:col-span-2">
              <label className="flex items-center space-x-3 cursor-pointer p-3 bg-gray-50 rounded-xl">
                <input 
                  type="checkbox" 
                  className="w-5 h-5 accent-emerald-600"
                  checked={formData.terms}
                  onChange={(e) => setFormData({...formData, terms: e.target.checked})}
                />
                <span className="text-sm text-gray-600">Saya berkomitmen untuk menjalankan usaha dengan jujur, transparan, dan sesuai prinsip syariah.</span>
              </label>
              {errors.terms && <p className="text-red-500 text-xs mt-1">{errors.terms}</p>}
            </div>

            <button 
              type="submit"
              className="md:col-span-2 bg-emerald-600 text-white font-bold py-4 rounded-xl hover:bg-emerald-700 transition shadow-lg"
            >
              Daftar Sekarang
            </button>
          </form>
        )}
      </div>
    </div>
  );
};

/**
 * KOMPONEN: POSDashboard
 * Inti aplikasi dengan grid produk, ringkasan transaksi, dan kalkulator zakat.
 */
const POSDashboard = ({ onLogout }) => {
  const [cart, setCart] = useState([]);
  const [includeZakat, setIncludeZakat] = useState(false);
  const [paymentMethod, setPaymentMethod] = useState('Tunai');

  const products = [
    { id: 1, name: 'Kurma Ajwa Super', price: 150000, category: 'Makanan' },
    { id: 2, name: 'Madu Sidr Yaman', price: 450000, category: 'Kesehatan' },
    { id: 3, name: 'Habbatussauda Oil', price: 85000, category: 'Kesehatan' },
    { id: 4, name: 'Gamis Ikhwan', price: 225000, category: 'Fashion' },
    { id: 5, name: 'Air Zamzam 5L', price: 350000, category: 'Minuman' },
    { id: 6, name: 'Siwak Al-Khair', price: 15000, category: 'Kesehatan' },
  ];

  const addToCart = (product) => {
    const existing = cart.find(item => item.id === product.id);
    if (existing) {
      setCart(cart.map(item => item.id === product.id ? {...item, qty: item.qty + 1} : item));
    } else {
      setCart([...cart, {...product, qty: 1}]);
    }
  };

  const removeFromCart = (id) => {
    setCart(cart.filter(item => item.id !== id));
  };

  const updateQty = (id, delta) => {
    setCart(cart.map(item => {
      if (item.id === id) {
        const newQty = Math.max(1, item.qty + delta);
        return {...item, qty: newQty};
      }
      return item;
    }));
  };

  const subtotal = useMemo(() => cart.reduce((acc, item) => acc + (item.price * item.qty), 0), [cart]);
  const zakatValue = useMemo(() => includeZakat ? subtotal * 0.025 : 0, [subtotal, includeZakat]);
  const total = subtotal + zakatValue;

  return (
    <div className="flex flex-col h-screen bg-gray-50 overflow-hidden lg:flex-row">
      {/* Sidebar Nav (Desktop) / Header (Mobile) */}
      <div className="w-full lg:w-20 bg-emerald-900 flex lg:flex-col items-center justify-between p-4 text-white">
        <div className="p-2 bg-emerald-700 rounded-xl">
          <Store size={28} />
        </div>
        <div className="flex lg:flex-col gap-6">
          <button className="p-3 bg-emerald-700 rounded-xl shadow-inner"><ShoppingBag size={24} /></button>
          <button className="p-3 hover:bg-emerald-800 transition rounded-xl text-emerald-300"><Calculator size={24} /></button>
        </div>
        <button onClick={onLogout} className="p-3 hover:bg-red-800 transition rounded-xl text-emerald-300">
          <LogOut size={24} />
        </button>
      </div>

      {/* Main Grid Produk */}
      <div className="flex-1 flex flex-col min-w-0">
        <header className="bg-white border-b px-8 py-6 flex justify-between items-center">
          <div>
            <h1 className="text-2xl font-bold text-gray-800">Menu Produk</h1>
            <p className="text-gray-500 text-sm">Pilih produk untuk ditambahkan ke keranjang</p>
          </div>
          <div className="flex items-center space-x-3 bg-blue-50 px-4 py-2 rounded-full border border-blue-100">
            <CheckCircle className="text-blue-600" size={18} />
            <span className="text-blue-800 text-xs font-bold tracking-tight uppercase">Sistem Audit Syariah Aktif</span>
          </div>
        </header>

        <main className="flex-1 overflow-y-auto p-8 grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-3 gap-6">
          {products.map(product => (
            <div 
              key={product.id}
              onClick={() => addToCart(product)}
              className="bg-white p-6 rounded-2xl shadow-sm border border-gray-100 hover:border-emerald-500 hover:shadow-md transition-all cursor-pointer group"
            >
              <div className="w-full h-40 bg-gray-50 rounded-xl mb-4 flex items-center justify-center text-gray-300">
                <ShoppingBag size={48} />
              </div>
              <div className="flex justify-between items-start">
                <div>
                  <span className="text-[10px] font-bold text-emerald-600 bg-emerald-50 px-2 py-1 rounded uppercase mb-2 inline-block">
                    {product.category}
                  </span>
                  <h3 className="font-bold text-gray-800">{product.name}</h3>
                  <p className="text-lg font-black text-gray-900 mt-1">Rp {product.price.toLocaleString('id-ID')}</p>
                </div>
                <div className="bg-emerald-600 text-white p-2 rounded-lg opacity-0 group-hover:opacity-100 transition">
                  <Plus size={20} />
                </div>
              </div>
            </div>
          ))}
        </main>
      </div>

      {/* Cart & Checkout Panel */}
      <div className="w-full lg:w-[450px] bg-white border-l shadow-2xl flex flex-col">
        <div className="p-6 border-b">
          <h2 className="text-xl font-bold text-gray-800 flex items-center">
            <ShoppingBag className="mr-2 text-emerald-600" /> Keranjang Belanja
          </h2>
        </div>

        <div className="flex-1 overflow-y-auto p-6 space-y-4">
          {cart.length === 0 ? (
            <div className="h-full flex flex-col items-center justify-center text-gray-400">
              <AlertCircle size={48} className="mb-2 opacity-20" />
              <p>Belum ada transaksi</p>
            </div>
          ) : (
            cart.map(item => (
              <div key={item.id} className="flex items-center justify-between p-3 bg-gray-50 rounded-2xl">
                <div className="flex-1">
                  <h4 className="font-bold text-gray-800 text-sm">{item.name}</h4>
                  <p className="text-emerald-600 text-xs font-semibold">Rp {item.price.toLocaleString('id-ID')}</p>
                </div>
                <div className="flex items-center space-x-3">
                  <div className="flex items-center bg-white rounded-lg border px-2 py-1">
                    <button onClick={() => updateQty(item.id, -1)} className="text-gray-400 hover:text-emerald-600"><Minus size={14}/></button>
                    <span className="mx-3 text-sm font-bold min-w-[20px] text-center">{item.qty}</span>
                    <button onClick={() => updateQty(item.id, 1)} className="text-gray-400 hover:text-emerald-600"><Plus size={14}/></button>
                  </div>
                  <button 
                    onClick={() => removeFromCart(item.id)}
                    className="text-red-400 hover:text-red-600 p-1"
                  >
                    <Trash2 size={18} />
                  </button>
                </div>
              </div>
            ))
          )}
        </div>

        {/* Ringkasan & Kalkulator Zakat */}
        <div className="p-6 bg-emerald-50/50 border-t space-y-4">
          <div className="flex items-center justify-between bg-white p-4 rounded-2xl border border-emerald-100">
            <div className="flex items-center">
              <div className="bg-emerald-100 p-2 rounded-lg mr-3">
                <Calculator className="text-emerald-700" size={20} />
              </div>
              <div>
                <p className="text-xs font-bold text-gray-500 uppercase">Kalkulator Zakat Maal</p>
                <p className="text-[10px] text-emerald-600 font-medium">Auto 2.5% dari Transaksi</p>
              </div>
            </div>
            <label className="relative inline-flex items-center cursor-pointer">
              <input 
                type="checkbox" 
                className="sr-only peer" 
                checked={includeZakat} 
                onChange={() => setIncludeZakat(!includeZakat)}
              />
              <div className="w-11 h-6 bg-gray-200 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-emerald-600"></div>
            </label>
          </div>

          <div className="space-y-2">
            <div className="flex justify-between text-gray-500 text-sm">
              <span>Subtotal</span>
              <span>Rp {subtotal.toLocaleString('id-ID')}</span>
            </div>
            {includeZakat && (
              <div className="flex justify-between text-emerald-700 text-sm font-medium animate-fade-in">
                <span>Zakat/Infaq (2.5%)</span>
                <span>+ Rp {zakatValue.toLocaleString('id-ID')}</span>
              </div>
            )}
            <div className="flex justify-between text-xl font-black text-gray-900 pt-2 border-t border-dashed border-gray-300">
              <span>Total Tagihan</span>
              <span>Rp {total.toLocaleString('id-ID')}</span>
            </div>
          </div>

          <div className="grid grid-cols-2 gap-3">
            <button 
              onClick={() => setPaymentMethod('Kredit')}
              className={`flex flex-col items-center justify-center p-3 rounded-2xl border transition-all ${paymentMethod === 'Kredit' ? 'border-emerald-600 bg-emerald-50 text-emerald-700 ring-2 ring-emerald-100' : 'border-gray-200 bg-white'}`}
            >
              <CreditCard size={20} className="mb-1" />
              <span className="text-[10px] font-bold uppercase">Kartu/Debit</span>
            </button>
            <button 
              onClick={() => setPaymentMethod('Tunai')}
              className={`flex flex-col items-center justify-center p-3 rounded-2xl border transition-all ${paymentMethod === 'Tunai' ? 'border-emerald-600 bg-emerald-50 text-emerald-700 ring-2 ring-emerald-100' : 'border-gray-200 bg-white'}`}
            >
              <Banknote size={20} className="mb-1" />
              <span className="text-[10px] font-bold uppercase">Tunai/Cash</span>
            </button>
          </div>

          <button 
            disabled={cart.length === 0}
            className="w-full bg-emerald-600 disabled:bg-gray-300 text-white font-black py-4 rounded-2xl shadow-lg shadow-emerald-200 transition-all hover:bg-emerald-700 active:scale-[0.98] mt-2"
          >
            SELESAIKAN TRANSAKSI
          </button>
        </div>
      </div>
    </div>
  );
};

/**
 * KOMPONEN UTAMA: App
 * Mengelola navigasi antar halaman.
 */
export default function App() {
  const [currentPage, setCurrentPage] = useState('login');

  return (
    <div className="font-sans antialiased text-gray-900">
      {currentPage === 'login' && <Login onNavigate={setCurrentPage} />}
      {currentPage === 'register' && <Register onNavigate={setCurrentPage} />}
      {currentPage === 'pos' && <POSDashboard onLogout={() => setCurrentPage('login')} />}
    </div>
  );
}
