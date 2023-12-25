// src/App.js
import React, { useState } from 'react';
import './App.css';

const initialProduct = {
  id: '',
  name: '',
  price: '',
  category: '',
};

const categories = ['skincare', 'electronics', 'food', 'medical'];

const App = () => {
  const [products, setProducts] = useState([]);
  const [newProduct, setNewProduct] = useState(initialProduct);
  const [showCategoryMenu, setShowCategoryMenu] = useState(false);

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setNewProduct((prevProduct) => ({
      ...prevProduct,
      [name]: value,
    }));
  };

  const handleCategoryClick = () => {
    setShowCategoryMenu(!showCategoryMenu);
  };

  const handleCategorySelect = (category) => {
    setNewProduct((prevProduct) => ({
      ...prevProduct,
      category,
    }));
    setShowCategoryMenu(false);
  };

  const handleAddProduct = () => {
    setProducts((prevProducts) => [...prevProducts, newProduct]);
    setNewProduct(initialProduct);
  };

  return (
    <div className="app">
      <h1>E-commerce Website</h1>
      <div className="product-grid">
        <div className="product-header">
          <div>Product ID</div>
          <div>Selling Price</div>
          <div>Product Name</div>
          <div>
            <div className="category-header" onClick={handleCategoryClick}>
              <span>Category</span>
              <button>Choose Category</button>
            </div>
            {showCategoryMenu && (
              <div className="category-menu">
                {categories.map((category) => (
                  <div
                    key={category}
                    className="category-item"
                    onClick={() => handleCategorySelect(category)}
                  >
                    {category}
                  </div>
                ))}
              </div>
            )}
          </div>
          <div>Action</div>
        </div>
        {products.map((product, index) => (
          <div key={index} className="product-row">
            <div>{product.id}</div>
            <div>${product.price}</div>
            <div>{product.name}</div>
            <div>{product.category}</div>
            <div></div>
          </div>
        ))}
        <div className="product-row">
          <input
            type="text"
            name="id"
            placeholder="Product ID"
            value={newProduct.id}
            onChange={handleInputChange}
          />
          <input
            type="text"
            name="price"
            placeholder="Selling Price"
            value={newProduct.price}
            onChange={handleInputChange}
          />
          <input
            type="text"
            name="name"
            placeholder="Product Name"
            value={newProduct.name}
            onChange={handleInputChange}
          />
          <div className="category-cell">
            <span>{newProduct.category}</span>
          </div>
          <button onClick={handleAddProduct}>Add Product</button>
        </div>
      </div>
    </div>
  );
};

export default App;
