<script setup>


const props = defineProps({
    time: {
        type: String,
        required: true,
    },
})

</script>

<template>
  <div class="circle">
    <h1 class="clockTime">{{ time }}</h1>
  </div>
</template>

<style lang="scss" scoped>
.circle {
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
  //border: solid 1px #252f68;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 300px;
  height: 300px;
  border-radius: 50%;
  background: linear-gradient(135deg, #9caafd, #3e4eaa);
  background-size: 200% 200%;
  animation: gradientAnimation 5s ease-in-out infinite;
}

.clockTime {
  color: white;
  font-family: "Montserrat Alternates";
  font-size: 3.5rem;
}

@keyframes gradientAnimation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>