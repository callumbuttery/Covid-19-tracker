<template>
  <header class="text-center bg-blue-800 text-white p-4 mb-10">
    <div class="text-3xl font-bold md:text-5xl pb-5">Covid-19 tracker <i class="fa fa-virus pl-2"></i></div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: {
    msg: String
  }
}
</script>