<template>
  <div
    class="container bg-white w-full h-full m-auto"
    style="width: 100%; height: 100%"
  >
    <!-- //////////// -->
    <!-- task 1 -->
    <!-- //////////// -->
    <div class="task-1 row justify-center items-center">
      <UDivider label="Task 1" />
      <UButton label="Open popup modal" @click="isOpen = true" />
      <!-- //////////// -->
      <!-- popup dialog -->
      <!-- //////////// -->
      <UModal v-model="isOpen">
        <ModalContent @closeDialog="isOpen = false" />
      </UModal>
    </div>
  </div>
</template>

<script setup lang="ts">
// iterface
interface Order {
  name: string;
  price: number;
  taxable: boolean;
}
//
import { ref } from "vue";
import ModalContent from "../components/modal-content.vue";
// import { Order } from "../components/model-interfaces.ts";
const isOpen = ref<boolean>(false);
// ////////
// task 2
///////////
const names = ref([
  "Kareem",
  "Ahmed",
  "Eslam",
  "Mohamed",
  "Ali",
  "Helmy",
  "Sobhy",
  "Yousef",
  "Salma",
  "Housein",
  "Momen",
]);
const filterAndPrintNames = (names: string[]): void => {
  const uniqueNames = [...new Set(names)]; // Remove duplicates
  const result: string[] = [];
  uniqueNames.forEach((el) => {
    if (el.length > 255) {
      return console.log("Name exceeds 255 characters. Stopping the process.");
    } else if (el.includes("a")) {
      //   console.log(name);
      result.push(el);
    }
  });
  const sortedNames = result.sort(); // Sort names in alphabetical order
  console.log("//////////task 2/////////////");
  console.log("Sorted Names:", sortedNames);
};
const firstLoad = () => {
  setTimeout(() => {
    isOpen.value = true;
  }, 2000);
};
// ////////
// task 3
///////////
const orders = ref<Order[]>([
  {
    name: "order 1",
    price: 125,
    taxable: true,
  },
  {
    name: "Order 2",
    price: 75,
    taxable: true,
  },
]);
const discountPercentage = 10;
const formatCurrency = (amount: number): string => {
  const roundedAmount = Math.round(amount * 20) / 20; // Round to nearest 5 cents
  return `EGP ${roundedAmount.toFixed(2)}`;
};
const calculateOrderTotals = (
  discountPercentage: number,
  orders: Order[]
): void => {
  let totalAmountBeforeTax = 0;
  let totalDiscountAmount = 0;
  let totalAmountAfterDiscount = 0;
  let totalSST = 0;
  let totalServiceTax = 0;

  for (const order of orders) {
    const originalPrice = order.price;
    let discountedPrice = originalPrice;
    let taxRate = 0;

    if (order.taxable) {
      // calc discount Price
      const discountAmount = (originalPrice * discountPercentage) / 100;
      discountedPrice -= discountAmount;
      // calc SST
      taxRate = 0.06; // 6% SST for taxable orders
      const sst = discountedPrice * taxRate;
      totalSST += sst;
      // calc Service TaxRate
      const serviceTaxRate = 0.1; // 10% service tax for taxable orders
      const serviceTax = discountedPrice * serviceTaxRate;
      totalServiceTax += serviceTax;
    }

    totalAmountBeforeTax += originalPrice;
    totalDiscountAmount += originalPrice - discountedPrice;
    totalAmountAfterDiscount += discountedPrice;
  }
  console.log("//////////task 3/////////////");
  console.log("Total Amount Before Tax:", formatCurrency(totalAmountBeforeTax));
  console.log("Total Discount Amount:", formatCurrency(totalDiscountAmount));
  console.log(
    "Total Amount After Discount:",
    formatCurrency(totalAmountAfterDiscount)
  );
  console.log("Total SST (6%):", formatCurrency(totalSST));
  console.log("Total Service Tax (10%):", formatCurrency(totalServiceTax));
};
onMounted(() => {
  filterAndPrintNames(names.value);
  calculateOrderTotals(discountPercentage, orders.value);
  firstLoad();
});
</script>

<style>
</style>