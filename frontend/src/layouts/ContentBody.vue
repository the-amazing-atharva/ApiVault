<template>
  
  <div class="flex-adjust container p-4">
    <div class="hero container">
      <div class="row">
        <div class="col-12 col-lg-12 col-md-12">
          <slot name="heroAreaContent"></slot>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-12 mb-5">
        <slot name="topAreaContent"></slot>
      </div>
    </div>
    <h1 class="text-wrapper mb-3">{{ props.title }}</h1>
    <h5 class="text-wrapper" v-if="isNullCategory">
      No Api's found for this category.. Sorry!!
    </h5>
    <slot name="cardAreaContent"></slot>
    <div class="container mt-5">
      <hr />
      <slot name="footerArea"></slot>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  title: {
    type: String,
    required: false,
    default: "RANDOM",
  },
  isNullCategory: {
    type: Boolean,
    required: false,
    default: false,
  },
});
</script>

<style scoped>
.hero {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.flex-child {
  flex-direction: column;
  flex-grow: 1;
  top: 25%;
  left: 25%;
}

.flex-adjust {
  margin-left: 22vw;
  margin-top: 7vw;
}

.sidebar {
  width: 25vw;
}

.body-wrap {
  left: 25%;
}

@media only screen and (max-width: 600px) {
  .mobile-first {
    display: none;
  }
  .flex-adjust {
    margin-left: 0vw;
    margin-top: 8vh;
  }
}

@media (min-width: 1581px) {
  .flex-adjust {
    margin-left: 26vw;
    margin-right: 8vw;
    margin-top: 7vw;
  }
}
</style>
