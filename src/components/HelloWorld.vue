<script setup>
import { ref } from 'vue'

const bookingList = ref([])

const shop = ref('กรุณาเลือกร้าน')
const bookingName = ref()
const bookingTime = ref('12:00')
const bookingTel = ref()
const bookingDate = ref()
const bookingTable = ref(1)

const setShop = (name) => {
  shop.value = name
}

const formErrorMessage = ref();

const bookShop = (name) => {
  if (shop.value != "กรุณาเลือกร้าน") {
    bookingList.value.push({
      shopName: name,
      customerName: bookingName.value,
      time: bookingTime.value,
      tel: bookingTel.value,
      date: bookingDate.value,
      tableCount: bookingTable.value
    })

    bookingName.value = ''
    bookingTime.value = ''
    bookingTel.value = ''
    bookingDate.value = ''
    bookingTable.value = ''
  } else {
    formErrorMessage.value = 'กรุณาเลือกร้านที่ต้องการ'
  }
}

const travelList = ref([
  {
    name: "Mingmitr Coffee",
    price: 4.4,
    imgUrl: "https://lh3.googleusercontent.com/p/AF1QipOFj5Lc1dIgI8TV8OKtQKb1c24d4nm1D6kfP-kv=s680-w680-h510",
  },
  {
    name: "SELF",
    price: 4.6,
    imgUrl: "https://lh3.googleusercontent.com/p/AF1QipMnckFQ-iOLnch0Kb7qvzq1j_-Vd-VPdB-gm9M1=s680-w680-h510",
  },
  {
    name: "Gateway Coffee Roaster",
    price: 4.4,
    imgUrl: "https://lh3.googleusercontent.com/p/AF1QipNJoJLm1pudYm2kFjWBaA_Yl8YZaEN_qEZjghxG=s680-w680-h510",
  },
  {
    name: "Still.Coffee&Life",
    price: 4.5,
    imgUrl: "https://lh3.googleusercontent.com/p/AF1QipNzqqu6fP1M07yJ1bBIb1m7_a2xDrXgZzeIhoUD=s680-w680-h510",
  },
  {
    name: "Pacamara Coffee Roasters",
    price: 4.5,
    imgUrl: "https://lh3.googleusercontent.com/p/AF1QipMG6N_lefYacSCaPFDUS_cFQN6juOXpYI7w5g3j=s680-w680-h510",
  },
])

</script>

<template>
  <div class="flex flex-col divide-y w-full lg:w-1024 mx-auto items-center divide-slate-800">
    <div class="py-8 px-4">
      <p class="text-sky-400 text-base font-bold">รายชื่อร้าน</p>
      <p class="text-white text-3xl font-extrabold">เลือกร้านที่ต้องการจอง</p>
      <div
        class="mt-5 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-y-8 gap-x-16 justify-items-center place-content-center">
        <div v-for="item in travelList">
          <div class="text-white bg-slate-800 w-full md:w-96 lg:w-80 rounded-md">
            <img :src="item.imgUrl" class="object-cover rounded-t-md">
            <div class="px-4 py-4">
              <p class="font-medium text-base">{{ item.name }}</p>
              <p>{{ item.price }}</p>
              <button @click="setShop(item.name)"
                class="mt-5 inline-flex w-full items-center justify-center p-2 active:bg-sky-800 bg-sky-500 rounded-md shadow-lg">
                เลือกร้าน
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="py-8 px-4 text-white w-full">
      <p class="text-base text-sky-400 font-bold">รายละเอียดการจอง</p>
      <p class="text-3xl font-bold">ชื่อร้าน {{ shop }}</p>
      <form @submit.prevent="bookShop(shop)" class="mt-5 gap-4 grid grid-col-1 md:grid-cols-2 lg:grid-cols-4">
        <div class="flex flex-col md:col-span-2">
          <label>ชื่อผู้จอง</label>
          <input maxlength="50" required v-model="bookingName" class="rounded-md text-gray-950 block border-gray-300"
            type="text">
        </div>
        <div class="flex flex-col md:col-span-1">
          <label>เบอร์โทรศัพท์</label>
          <input maxlength="10" required v-model="bookingTel" pattern="[0-9]*"
            class="rounded-md text-gray-950 block border-gray-300" type="text">
        </div>
        <div class="flex flex-col md:col-span-1">
          <label>วันที่</label>
          <input required v-model="bookingDate" class="rounded-md text-gray-950 block border-gray-300" type="date">
        </div>
        <div class="flex flex-col md:col-span-1">
          <label>เวลา</label>
          <input required v-model="bookingTime" class="rounded-md text-gray-950 block border-gray-300" type="time">
        </div>
        <div class="flex flex-col md:col-span-1">
          <label>จำนวนโต้ะ</label>
          <input min="1" required v-model="bookingTable" class="rounded-md text-gray-950 block border-gray-300"
            type="number">
        </div>
        <p class="text-red-500">{{ formErrorMessage }}</p>
        <button
          class="mt-5 md:col-span-2 lg:col-span-4 inline-flex w-full items-center justify-center p-2 active:bg-sky-800 bg-sky-500 rounded-md shadow-lg"
          type="submit">จองโต้ะ</button>
      </form>
    </div>

    <div class="mt-5 py-8 px-4 w-full">
      <p class="text-sky-400 text-base font-bold">ตารางการจอง</p>
      <p class="text-white text-3xl font-extrabold">รายละเอียด</p>
      <div class="bg-slate-800 flex flex-col">
        <div class="grid h-12 grid-rows-1 grid-cols-7 place-items-center text-white">
          <div class="col-span-1">ลำดับ</div>
          <div class="col-span-2">ชื่อร้าน</div>
          <div class="col-span-1">เบอร์โทรศัพท์</div>
          <div class="col-span-1">วันที่</div>
          <div class="col-span-1">เวลา</div>
          <div class="col-span-1">จำนวนโต้ะ</div>
        </div>
      </div>
      <div v-for="(list, index) in bookingList" class="bg-slate-800 flex flex-col">
        <div class="grid h-12 grid-rows-1 grid-cols-7 place-items-center text-white">
          <div class="col-span-1">{{ index + 1 }}</div>
          <div class="col-span-2">{{ list.shopName }}</div>
          <div class="col-span-1">{{ list.tel }}</div>
          <div class="col-span-1">{{ list.date }}</div>
          <div class="col-span-1">{{ list.time }}</div>
          <div class="col-span-1">{{ list.tableCount }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
