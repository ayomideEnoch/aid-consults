<template>
  <div class="overflow-y-auto mb-12">
    <!-- Top Bar -->
    <section class="bg-green-100 h-48 top-nav-radius">
      <div class="flex justify-between mx-6 py-2">
        <div>
          <img src="./assets/logo.png" alt="logo" class="h-12" />
        </div>
        <div class="bg-gray-100 rounded-full shadow-md w-1/3 flex justify-center">
          <input
            placeholder="Search"
            class="p-1.5 pl-5 bg-transparent focus:outline-none w-full"
            type="text"
          />
        </div>
        <div class="flex items-center">
          <button
            class="py-2 flex items-center text-white hover:text-green-900 bg-green-600 lg:px-5 px-2 rounded-2xl focus:outline-none"
          >
            <i class="fas fa-user pr-2"></i>
            <p>Login</p>
          </button>
          <div
            class="relative h-10 w-10 bg-white rounded-full shadow-md mx-3 flex items-center justify-center cursor-pointer"
          >
            <i class="fas fa-shopping-cart text-green-700"></i>
            <p
              v-if="cartCheckout.length !== 0"
              class="absolute -top-1 -right-2 bg-red-500 text-white rounded-full py-0.5 px-1 text-xs"
            >
              {{ cartCheckout.length }}
            </p>
          </div>
        </div>
      </div>
    </section>
    <!-- slider -->
    <section class="flex justify-center w-full">
      <div class="w-10/12 -mt-28 rounded-3xl bg-green-400 h-72 relative">
        <i
          class="fas fa-chevron-left bg-green-200 hover:bg-green-100 cursor-pointer p-4 shadow-lg top-32 -left-3 absolute"
        ></i>
        <i
          class="fas fa-chevron-right bg-green-200 hover:bg-green-100 p-4 cursor-pointer shadow-lg top-32 -right-3 absolute"
        ></i>
      </div>
    </section>
    <!-- filter -->
    <section class="mt-2 flex justify-center w-full">
      <div class="w-10/12 flex lg:justify-end justify-center">
        <div class="flex">
          <button
            @click="filterAll"
            class="py-2 flex items-center font-medium lg:px-5 px-2 rounded-md focus:outline-none hover:bg-green-100"
          >
            <p>All</p>
          </button>

          <button
            @click="filterFemale"
            class="py-2 flex items-center font-medium lg:px-5 px-2 rounded-md focus:outline-none hover:bg-green-100"
          >
            <i class="fas fa-female pr-2"></i>
            <p>Women</p>
          </button>

          <button
            @click="filterMale"
            class="py-2 flex items-center font-medium lg:px-5 px-2 rounded-md focus:outline-none hover:bg-green-100"
          >
            <i class="fas fa-male pr-2"></i>
            <p>Men</p>
          </button>
        </div>
      </div>
    </section>
    <!-- products -->
    <section class="mt-2 w-full flex justify-center">
      <div class="flex flex-wrap w-10/12">
        <div
          v-for="(product, index) in filter"
          :key="product.index"
          class="w-full md:w-2/3 lg:w-1/3 p-6"
        >
          <div class="relative overflow-hidden h-56 bg-green-400 rounded-t-2xl">
            <img
              :src="product.img"
              alt="product image"
              class="inset-0 h-full w-full object-cover z-10"
            />
            <div
              @click="cart(index)"
              class="z-20 absolute top-2 right-1 h-10 w-10 bg-white rounded-full shadow-md mx-3 flex items-center justify-center cursor-pointer"
            >
              <i class="fas fa-shopping-cart text-green-700"></i>
            </div>
          </div>
          <div class="text-center bg-green-400 rounded-b-2xl">
            <p class="font-normal text-2xl pt-1">{{ product.name }}</p>
            <p class="font-normal text-lg pb-2">{{ product.price }}</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      all: true,
      male: false,
      female: false,
      filter: [],
      cartCheckout: [],
      products: [
        {
          name: "Coperate gown",
          img:
            "https://images.unsplash.com/photo-1541664341-b4fa5ce5af36?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N15,000",
          type: "female",
          id: "1",
        },
        {
          name: "Bagpack",
          img:
            "https://images.unsplash.com/photo-1576160964124-4dc82a54a889?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N11,500",
          type: "male",
          id: "2",
        },
        {
          name: "Ring",
          img:
            "https://images.unsplash.com/photo-1605084192554-c4819b9df088?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N32,750",
          type: "female",
          id: "3",
        },
        {
          name: "Towel",
          img:
            "https://images.unsplash.com/photo-1607983512825-c915b95e5126?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N2,500",
          type: "female",
          id: "4",
        },
        {
          name: "Peruvian hair",
          img:
            "https://images.unsplash.com/photo-1565357419076-6acd4a10094e?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N45,000",
          type: "female",
          id: "5",
        },
        {
          name: "Belt",
          img:
            "https://images.unsplash.com/photo-1608461864721-b8f50c91c147?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N6,000",
          type: "female",
          id: "6",
        },
        {
          name: "Lingerie",
          img:
            "https://images.unsplash.com/photo-1590397041404-a0cfb285a2a6?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N3,500",
          type: "female",
          id: "7",
        },
        {
          name: "Night gown",
          img:
            "https://images.unsplash.com/photo-1610372081846-c7c558355e0a?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N4,500",
          type: "female",
          id: "8",
        },
        {
          name: "Coperate shoes",
          img:
            "https://images.unsplash.com/photo-1557870187-4304e2c2b357?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N35,000",
          type: "male",
          id: "9",
        },
        {
          name: "Necklace",
          img:
            "https://images.unsplash.com/photo-1609245340409-cad2474ab1d5?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N3,000",
          type: "female",
          id: "10",
        },
        {
          name: "Sneakers",
          img:
            "https://images.unsplash.com/photo-1550399865-ec7d23b18e8e?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N25,000",
          type: "male",
          id: "11",
        },
        {
          name: "Face cap",
          img:
            "https://images.unsplash.com/photo-1569466896818-335b1bedfcce?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N3,000",
          type: "male",
          id: "12",
        },
        {
          name: "Nose mask",
          img:
            "https://images.unsplash.com/photo-1597926575726-57f359453262?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N1,000",
          type: "male",
          id: "13",
        },
        {
          name: "Coperate shirt",
          img:
            "https://images.unsplash.com/photo-1593467685675-5c0c123331c6?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N9,000",
          type: "male",
          id: "14",
        },
        {
          name: "Polo shirt",
          img:
            "https://images.unsplash.com/photo-1542776575-f1623249ce85?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N5,500",
          type: "male",
          id: "15",
        },
        {
          name: "Pant trouser",
          img:
            "https://images.unsplash.com/photo-1599505043552-fa95de5548ac?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N7,500",
          type: "female",
          id: "16",
        },
        {
          name: "Jean trouser",
          img:
            "https://images.unsplash.com/photo-1454720503269-3a35c21bebc6?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N8,000",
          type: "female",
          id: "17",
        },
        {
          name: "Sweatshirt",
          img:
            "https://images.unsplash.com/photo-1596404129310-1ba3abeaed1e?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N15,000",
          type: "female",
          id: "18",
        },
        {
          name: "Sunglass",
          img:
            "https://images.unsplash.com/photo-1508296695146-257a814070b4?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N18,000",
          type: "female",
          id: "19",
        },
        {
          name: "Wristwatch",
          img:
            "https://images.unsplash.com/photo-1444076295597-e246c794dc5f?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N15,000",
          type: "male",
          id: "20",
        },
        {
          name: "Hand Bag",
          img:
            "https://images.unsplash.com/photo-1596149615678-8488f200b301?ixid=MXwxMjA3fDB8MHxzZWFyY2h8N3x8ZmFzaGlvbiUyMGxvb2t8ZW58MHx8MHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          price: "N45,000",
          type: "female",
          id: "21",
        },
      ],
    };
  },
  methods: {
    cart(index) {
      let i = index;
      this.cartCheckout.push(i);
    },
    filterAll() {
      this.male = false;
      this.female = false;
      this.all = true;
      this.filteredProduct();
    },

    filterMale() {
      this.all = false;
      this.female = false;
      this.male = true;
      this.filteredProduct();
    },

    filterFemale() {
      this.all = false;
      this.male = false;
      this.female = true;
      this.filteredProduct();
    },

    filteredProduct() {
      if (this.all === true) {
        this.filter = this.products;
      }
      if (this.male === true) {
        let result = this.products;
        let filter = result.filter(function (type) {
          return type.type === "male";
        });
        this.filter = filter;
      }

      if (this.female === true) {
        let result = this.products;
        let filter = result.filter(function (type) {
          return type.type === "female";
        });
        this.filter = filter;
      }
    },
  },
  mounted() {
    this.filteredProduct();
  },
};
</script>

<style></style>
