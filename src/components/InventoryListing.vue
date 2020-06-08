<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <p>
      จำนวนรายการสินค้าทั้งหมด: {{ totalProductList }} รายการ
      <br />
      <small class="red">** สินค้าแต่ละชนิดจัดเก็บได้ไม่เกิน 20 ชิ้น</small>
    </p>

    <ul v-for="product in products" :key="product.id">
      ชื่อสินค้า:
      <span class="blod">{{ product.name }}</span>
      <br />คงเหลือ:
      <span v-if="product.quantity <= 0" class="outofstock">OUT OF STOCK</span>
      <span v-else class="blod">{{ product.quantity }}</span>
      <br />

      <button @click="limitStockEvent(product)">
        เพิ่มจำนวนครั้งละ 1 ชิ้น
      </button>
      <button @click="checkOutOfStockEvent(product)">
        ลดจำนวนครั้งละ 1 ชิ้น
      </button>
      <br />กำหนดจำนวนตามต้องการ:
      <input
        type="number"
        min="0"
        class="qty"
        oninput="this.value = Math.abs(this.value)"
        v-model="product.quantity"
      />
    </ul>
    <p>จำนวนสินค้าทั้งหมดในคลังสินค้า: {{ totalProductsQyt }} ชิ้น</p>
  </div>
</template>

<script>
export default {
  name: "InventoryListing",
  props: {
    title: String,
  },
  data: function() {
    return {
      products: [
        {
          id: 1,
          quantity: 10,
          name: "นาฬิกา",
        },
        {
          id: 2,
          quantity: 5,
          name: "แว่นตา",
        },
        {
          id: 3,
          quantity: 9,
          name: "แล็ปท็อป",
        },
        {
          id: 4,
          quantity: 0,
          name: "ถุงเท้า",
        },
        {
          id: 5,
          quantity: 5,
          name: "เสื้อยืด",
        },
      ],
    };
  },
  computed: {
    totalProductList() {
      return this.products.length;
    },
    totalProductsQyt() {
      return this.products.reduce((sum, product) => {
        return sum += Math.abs(product.quantity)
      }, 0)
    }
  },
  methods: {
    limitStockEvent: function(product) {
      product.quantity += 1;

      if (product.quantity > 20) {
        product.quantity = 20
      }
    },
    checkOutOfStockEvent: function(product) {
      product.quantity -= 1

      if (product.quantity < 0) {
        product.quantity = 0
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.blod {
  font-weight: bold;
}
.red {
  color: gray;
}
.outofstock {
  color: red;
  font-weight: 900;
}
.qty {
  max-width: 3rem;
}
</style>
