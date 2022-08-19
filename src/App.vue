<template>
   <div class="container">
        <div class="list-blog">
            <p><strong>*</strong> Nếu bạn thấy CÔ ĐƠN, hãy mua hoa về trồng. Nếu bạn thấy GỤC NGÃ, hãy diện lên <strong>chiếc áo này</strong> và tiếp tục đi tiếp!</p>
        </div>
        <div id="app">
            <div class="cart">Giỏ hàng ({{ cardNumber}})</div>
            <div class="product">
                <div class="product-image">
                    <div class="image">
                        <img :src="getProduct.image" alt=""> <!--hiển thị hình ảnh-->
                    </div>
                </div>
                <div class="product-content">
                    <h3 class="title">
                    <a href="">{{title}}</a>
                    </h3>
                    <p class="brand">Thương hiệu: No brand</p>
                    <p class="quantity" v-if="getProduct.quantity > 0">Còn lại: {{ getProduct.quantity}} Sản phẩm</p> <!--điều kiện hiển thị-->
                    <p class="quantity" v-if="getProduct.quantity <= 0"><strong style="color:red">SẢN PHẨM ĐÃ HẾT HÀNG!</strong></p> <!--điều kiện hiển thị-->

                    <div class="wrapper-price">
                        <div class="final-price">{{ formatPriceSale }}</div>        <!--hàm format dưới computed-->
                        <div class="origin-price">{{ formatPriceOriginal }}</div>    <!--hàm format dưới computed-->
                        <div class="sale-price">-{{sale * 100}}%</div>          <!--Hiển thị % sale-->
                    </div>
                    <div class="wrapper-color">
                        <div class="text">Màu sắc</div>
                        <div class="list-color">
                            <p class="color-text">{{getProduct.textColor}}</p>
                            <ul>
                                <li v-for="(item, index) in infoProducts" :key="index" @click="handleChangeColor(index)" :class="{ active: selectedProduct == index}"> <!--bind class-->
                                  <img v-bind:src="item.image" v-bind:alt="item.textColor"/> <!---hiển thị hình ảnh-->
                                </li>
                            </ul>
                        </div>
                    </div>
                    <button 
                        @click="handleAddToCart"
                        class="add-to-cart">Add to cart</button>
                </div>
                
            </div>
            <!--Render ra html - description-->
            <div class="description" v-for="(des, index) in listDesc" :key="index">
                <li>{{des}}</li>
            </div>
                
        </div>
    </div>
</template>

<script>
//import image
import red from './assets/images/red.jpg'
import blue from './assets/images/blue.jpg'
import black from './assets/images/black.jpg'

export default {
  name: 'App',
  data() {
    return {
      title: 'Áo thun nam thể thao hàng VNXK vải dày mịn - Vải Đốm',
      url: 'https://www.lazada.vn/products/ao-thun-nam-the-thao-hang-vnxk-vai-day-min-vai-dom-i265780948-s382816279.html',
      target: '_blank',
      price: 20000,
      sale: 0.1,
      selectedProduct: 0,
      cardNumber: 0,

      infoProducts: [
        {
          image: red, //dùng
          quantity: 0,
          textColor: 'Màu Đỏ'
        },
        {
          image: blue,
          quantity: 5,
          textColor: 'Màu Xanh'
        },
        {
          image: black,
          quantity: 2,
          textColor: 'Màu Đen'
        }
      ],

       listDesc: [
            'Chất liệu: polyester và thun',
            'Thoát mồ hôi tốt',
            'Áo thun cổ tròn thể thao Hiye chuyên được may từ chất liệu nilon thoáng mát',
            'Kết hợp thêm sợi thun tạo độ co giãn giúp người tiêu dùng thoải mái khi mặc',
            'Chất liệu: polyester và thun'
        ],
    }
  },

  methods: {
    handleChangeColor(index){
        // console.log("index", index);
        this.selectedProduct = index
    },
    handleAddToCart(){
        if (this.cardNumber + 1 > this.getProduct) {
            alert('meo du hang')
        } else {
            this.cardNumber = this.cardNumber + 1
        }
    }
  },

  computed: {
    // Giá gốc
    formatPriceOriginal() {
      var number = this.price
      return new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'VND' }).format(number); // Hàm format giá tiền
    },

    // Giá sale
    formatPriceSale() {
      var number  = this.price - this.sale * this.price // giá hiện tại - sale * giá hiện tại
      return new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'VND' }).format(number); // Hàm format giá tiền
    },

    // Select hình ảnh theo selectedProduct
    getProduct() {
      var index = this.selectedProduct
      return this.infoProducts[index]
    }
  }
}
</script>

<style>
body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
}
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 30px;
}
.list-blog {
    font-size: 22px;
}
.cart {
    border-radius: 5px;
    background-color: #ffb916;
    font-weight: 700;
}
img {
    max-width: 100%;
}
.product {
    max-width: 700px;
    display: flex;
    margin-top: 20px;
    position: relative;
}
.product .product-image {
    flex-basis: 40%;
    max-width: 40%;
    padding-right: 30px;
}
.product .product-content {
    flex-basis: 60%;
}
.product-image .image {
    width: 100%;
    border: 1px solid #ccc;
}
.product-image .image img {
    display: block;
}
.title {
    margin-top: 0;
}
.title a {
    color: #333;
    text-decoration: none;
}
.cart {
    display: inline-block;
    padding: 15px 10px;
    border: 1px solid #ccc;
}
.wrapper-price .final-price {
    color: #f57224;
    font-weight: 700;
    font-size: 22px;
    margin-bottom: 5px;
}
.wrapper-price .origin-price,
.wrapper-price .sale-price {
    display: inline-block;
    font-size: 14px;
    color: #ccc;
    vertical-align: middle;
}
.wrapper-price .sale-price {
    color: #333;
    margin-left: 5px;
    padding: 3px;
    font-size: 10px;
    border-radius: 5px;
    border: 1px solid #f57224;
}

.wrapper-color {
    display: flex;
    margin-top: 15px;
    padding-top: 15px;
    border-top: 1px solid #eee;
}
.wrapper-color .text {
    width: 100px;
    min-width: 100px;
}
.wrapper-color p {
    margin-top: 0;
    margin-bottom: 10px;
}
.list-color ul {
    list-style-type: none;
    display: flex;
    margin: 0;
    padding: 0;
}
.list-color ul li {
    width: 40px;
    height: 40px;
    border: 1px solid #ccc;
    margin-right: 20px;
}
.list-color ul li:hover,
.list-color ul li.active {
    border-color: #f57224;
    cursor: pointer;
}

.description {
    max-width: 700px;
}
.description .extra-info {
    padding-left: 0;
    list-style-position: inside;
}
.add-to-cart {
    border: 1px solid #ffb916;
    background: #ffb916;
    color: #fff;
    display: block;
    padding: 12px 30px;
    margin-top: 30px;
    text-transform: uppercase;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
}


</style>