<template>
  <div class="md:flex p-5">
    <div class="md:flex-shrink-0"></div>
    <div class="mt-4 md:mt-0 md:ml-6">
      <div class="flex justify-between">
        <div class="col uppercase tracking-wide text-lg text-black font-bold">
          Marketing
        </div>
        <div class="col">
          <UButton
            color="gray"
            variant="ghost"
            icon="i-heroicons-x-mark-20-solid"
            class="-my-1"
            @click="closeDialog"
          />
        </div>
      </div>
      <p
        href="/get-started"
        class="block mt-1 text-lg leading-tight font-semibold text-gray-900 hover:underline"
      >
        Finding customers for your new business
      </p>
      <p class="mt-2 text-gray-600">
        Getting a new business off the ground is a lot of hard work. Here are
        five ideas you can use to find your first customers.
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
const emits = defineEmits(["closeDialog"]);
const closeDialog = () => {
  return emits("closeDialog");
};
</script>

<style>
</style>